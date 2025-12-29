## 1. Project Context

As part of an infrastructure improvement initiative, **CloudLogix** is migrating part of its infrastructure to a public cloud environment (Azure / AWS) in order to host its internal applications.

The target cloud architecture includes the following components:

- **HR Portal**: an internal web application used by employees.
- **Authentication Server**: centralized authentication and identity management using **Azure Active Directory (Azure AD)**.
- **Cloud SQL Database**: a managed SQL database hosted in the cloud.
- **Object Storage**: cloud storage services such as **Amazon S3** or **Azure Blob Storage**.
- **Remote Users**: employees accessing the applications remotely over the Internet via **HTTPS**.


## 2. Threat Modeling Approach

This project follows a structured threat modeling methodology based on:
- Data Flow Diagram (DFD)
- STRIDE threat identification
- DREAD risk prioritization

The analysis was performed using Microsoft Threat Modeling Tool (TMT)


## Data Flow Diagram

The architecture includes:
- External User
- HR Web Portal (central system)
- Azure Active Directory (Identity Provider)
- Cloud SQL Database
- Object Storage (Blob / S3)

Trust boundaries were defined between:
- User and Cloud (Internet)
- External Identity Provider (Azure AD)
- Internal Cloud Services

See detailed diagram in: `docs/dfd/`


## STRIDE Threat Analysis

A STRIDE-based threat analysis was conducted.
For each STRIDE category, two representative threats were identified and mitigated.

See details in: `docs/stride/STRIDE.md`


## Risk Prioritization (DREAD)

The DREAD method was applied to the most critical threats in order to prioritize remediation efforts.

The three priority threats identified are:
1. User impersonation or spoofing of the HR Portal
2. SQL Injection against the Cloud SQL Database
3. Denial of Service attack on the HR Portal


