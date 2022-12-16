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
