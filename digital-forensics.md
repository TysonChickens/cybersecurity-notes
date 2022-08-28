---
id: 8ml5picmbrjw3u887mag9dz
title: Digital Forensics
desc: ''
updated: 1656764396687
created: 1653180146923
---

# Forensics Overview

- [ ] What are digital forensics?
- [ ] What types of data do forensics deal with?
- [ ] What is the objective and need for digital forensics?
- [ ] What are the steps to the forensic process?

- [ ] What are the different types of data?
- [ ] What are the three steps of data acquisition?
- [ ] What role does chain of custody have in data collection?
- [ ] What obstacles are faced during examination?

- [ ] Review considerations when conducting an analysis.
- [ ] Learn about the components that make up a forensic report.
---

## What are Forensics?

Digital Forensics
: Also known as computer and network forensics, has many definitions. Generally, it is considered the application of science to the identification, collection, examination, and analysis of data while preserving the integrity of the information and maintaining a strict chain of custody for the data.

### Types of Data

The first step in the forensic process is to identify potential sources of data and acquire data from them. The most obvious and common sources of data are desktop computers, servers, network storage devices, and laptops.

1. CDs/DVDs
2. Internal & External Drives
3. Volatile data
4. Network Activity
5. Application Usage
6. Portable Digital Devices
7. Externally Owned Property
8. Computer at Home Office
9. Alternate Sources of Data
10. Logs
11. Keystroke Monitoring

### Need for Forensics

- Criminal Investigation
- Incident Handling
- Operational Troubleshooting
- Log Monitoring
- Data Recovery
- Data Acquisition
- Due Diligence/Regulatory Compliance

## Objectives of Digital Forensics

- Helps to recover, analyze, and preserve computer and related materials in such a manner that i helps the investigation agency to present them as evidence in a court of law. IT helps to postulate the motive behind the crime and identity of the main culprit.
- Designing procedures at as suspected crime scene which helps you to ensure that the digital evidence obtained is not corrupted.
- Data acquisition and duplication: Recovering deleted files and deleted partitions from digital media to extract the evidence and validate them.
- Helps you to identify the evidence quickly, and also allows you to estimate the potential impact of the malicious activity on the victim.
- Producing a computer forensic report which offers a complete report on the investigation process.
- Preserving the evidence by following the chain of custody.

## Forensic Process

Collection
: Identify, label, record and acquire data from the possible sources, while preserving the integrity of the data.

Examination
: Processing large amounts of collected data to assess and extract data of particular interest.

Analysis
: Analyze the results of the examination, using legally justifiable methods and techniques.

Reporting
: Reporting the results of the analysis.

### Data Collection & Examination - Steps to Collect Data

- Develop a plan to acquire the data.
  - Create a plan that prioritizes the sources, establishing the order in which the data should be acquired.
- Acquire the Data.
  - Use forensic tools to collect the volatile data, duplicate non-volatile data sources, and securing the original data sources.
- Verify the integrity of the data.
  - Forensic tools can create hash values for the original source so the duplicate can be verified as being complete and un-tampered with.

#### Chain of Custody

A clearly defined chain of custody should be followed to avoid allegations of mishandling or tampering of evidence. This involves keeping a log of every person who had physical custody of the evidence, documenting the actions that they performed on the evidence and at what time, storing the evidence in a secure location when it is not being used, making a copy of the evidence and performing examination and analysis using only the copied evidence, and verifying the integrity of the original and copied evidence.

#### Examination

Bypassing Controls
: Operating systems and applications may have data compression, encryption, or ACLs

A Sea of Data
: Hard drives may have hundreds of thousands of files, not all of which are relevant.

Tools
: There are various tools and techniques that exist to help filter and exclude data from searches to expedite the process.

### Analysis & Reporting

The analysis should include identifying people, places, items, and events, and determining how these elements are related so that a conclusion can be reached.

- **Putting the pieces together** - Coordination between multiple sources of data is crucial in making a complete picture of what happened in the incident. NIST provides the example of an IDS log linking an event to a host, the host audit logs linking the event to a specific user account, and the host IDS log indicating what actions that user performed.

#### Solved with Forensics

- **BTK Killer, Dennis Rader** - A floppy disk Rader sent to police revealed his true identity.
- **Dr. Conrad Murray's lethal prescriptions** - Investigators discovered documentation on Dr. Murray's computer showing his authorization of lethal amounts of the drugs.
- **The Craigslist Killer, Phillip Markoff** - Investigators tracked the IP address from the emails used in the Craigslist correspondence.

#### Writing Forensic Report

A case summary is meant to form the basis of opinions. While there are a variety of laws that relate to expert reports, the general rules are:

- If it is not in your report, you cannot testify about it.
- Your report needs to details the basis for your conclusions.
- Details every test conducted, the methods and tools used, and the results.

##### Report Composition

1. Overview/Case Summary
2. Forensic Acquisition & Examination Preparation
3. Findings & Report (Analysis)
4. Conclusion

[Intro to Report Writing for Digital Forensics Example](https://www.sans.org/blog/intro-to-report-writing-for-digital-forensics/)

##### SANS Institute - General Best Practices

1. Take screenshots
2. Bookmark evidence via forensic application of choice
3. Use built-in logging/reporting options within your forensic tool
4. Highlight and exporting data items into .csv or .txt files
5. Use a digital audio recorder vs. handwritten notes when necessary

According to the former director of the Defense Computer Forensics Laboratory, Ken Zatyko, digital forensics includes:

- **Proper search authority**: Investigators cannot commence without the proper legal authority.
- **Chain of custody**: Necessary to keep track of who was holding the evidence at any time.
- **Use of validated tools**: Tools used in digital forensics should be validated to ensure they work correctly.
  - Creating an image of a disk should ensure the forensic image is identical to the data on the disk.
- **Repeatability**: The findings of digital forensics can be reproduced with the proper skills and tools are available.
- **Reporting**: Investigation is concluded with a report that shows the evidence related to the case that was discovered.