# STRIDE Threat Analysis

This document presents the STRIDE-based threat analysis performed on the CloudLogix cloud architecture using Microsoft Threat Modeling Tool (TMT).  
For each STRIDE category, two representative and critical threats have been identified, analyzed, and mitigated.

---

## Spoofing (S)

### Threat 1
- **Threat:** User impersonation or spoofing of the HR Portal
- **Affected flow:** External User ↔ HR Portal
- **Description:** An external attacker may impersonate a legitimate user or spoof the HR Portal (e.g. via phishing, DNS spoofing, or man-in-the-middle attacks) to gain unauthorized access.
- **Impact:** High – unauthorized access to sensitive HR data.
- **Mitigation:** Azure AD authentication, multi-factor authentication (MFA), strong TLS configuration, secure session management.

### Threat 2
- **Threat:** Spoofed authentication response from Identity Provider
- **Affected flow:** HR Portal ↔ Azure Active Directory (Azure AD)
- **Description:** An attacker could attempt to spoof authentication responses or tokens if identity claims are not properly validated by the HR Portal.
- **Impact:** Medium – unauthorized access through forged authentication responses.
- **Mitigation:** Token signature validation, issuer and audience checks, TLS, strict identity validation.

---

## Tampering (T)

### Threat 1
- **Threat:** SQL Injection against the Cloud SQL Database
- **Affected flow:** HR Portal → Cloud SQL Database
- **Description:** An attacker could inject malicious SQL code through user-controlled inputs processed by the HR Portal, leading to unauthorized modification or deletion of database records.
- **Impact:** High – integrity of sensitive HR data may be compromised.
- **Mitigation:** Parameterized queries, strict input validation, least privilege database accounts, regular security testing.

### Threat 2
- **Threat:** Object Storage data corruption
- **Affected flow:** HR Portal → Object Storage (Blob / S3)
- **Description:** An attacker could modify, replace, or delete stored HR documents if access controls are misconfigured or credentials are compromised.
- **Impact:** Medium to High – integrity of stored HR documents could be compromised.
- **Mitigation:** Strong IAM policies, least privilege, object versioning, integrity checks, audit logging.

---

## Repudiation (R)

### Threat 1
- **Threat:** SQL Database denies data write operations
- **Affected flow:** HR Portal → Cloud SQL Database
- **Description:** The SQL database could deny having written or modified data if sufficient logging and auditing mechanisms are not enabled.
- **Impact:** Medium – lack of traceability and accountability.
- **Mitigation:** Enable database audit logs, timestamps, centralized logging.

### Threat 2
- **Threat:** Object Storage denies write or delete operations
- **Affected flow:** HR Portal → Object Storage (Blob / S3)
- **Description:** The object storage service could deny having written or deleted files in the absence of proper audit logs.
- **Impact:** Medium – inability to attribute file modifications.
- **Mitigation:** Enable object access logging, audit trails, centralized log collection.

---

## Information Disclosure (I)

### Threat 1
- **Threat:** Data disclosure due to misconfigured TLS on database connection
- **Affected flow:** HR Portal ↔ Cloud SQL Database
- **Description:** Sensitive HR data exchanged between the HR Portal and the SQL database could be intercepted if TLS is misconfigured or improperly enforced.
- **Impact:** High – exposure of sensitive HR information.
- **Mitigation:** Enforce TLS with strong cipher suites, certificate validation, encryption in transit, regular configuration reviews.

### Threat 2
- **Threat:** Data sniffing on HTTPS connection between user and HR portal
- **Affected flow:** External User ↔ HR Portal
- **Description:** Data exchanged over HTTPS could be intercepted by an attacker if transport security is weak or misconfigured, leading to information disclosure and compliance violations.
- **Impact:** High – leakage of user and HR-related data.
- **Mitigation:** Strong TLS configuration, HSTS, certificate validation, secure HTTP headers.

---

## Denial of Service (D)

### Threat 1
- **Threat:** Denial of Service attack on HR Portal
- **Affected flow:** External User ↔ HR Portal
- **Description:** An attacker could overwhelm the HR Portal with excessive requests, causing it to crash, slow down, or become unavailable.
- **Impact:** High – HR services become unavailable to employees.
- **Mitigation:** Rate limiting, Web Application Firewall (WAF), autoscaling, monitoring and alerting.

### Threat 2
- **Threat:** Denial of Service on authentication flow
- **Affected flow:** External User ↔ Azure Active Directory
- **Description:** An attacker could disrupt or flood authentication requests across the trust boundary, preventing users from authenticating.
- **Impact:** High – users are unable to log in to the HR Portal.
- **Mitigation:** Azure AD resilience, throttling, redundancy, monitoring.

---

## Elevation of Privilege (E)

### Threat 1
- **Threat:** Cross-Site Request Forgery (CSRF) on HR Portal
- **Affected flow:** External User ↔ HR Portal
- **Description:** An attacker could exploit an authenticated user’s session to perform unauthorized actions by forcing the user’s browser to send forged requests to the HR Portal.
- **Impact:** High – attackers could perform privileged or administrative actions.
- **Mitigation:** CSRF tokens, SameSite cookies, secure session management, server-side validation.

### Threat 2
- **Threat:** Privilege escalation via application flow manipulation
- **Affected flow:** HR Portal ↔ Azure Active Directory
- **Description:** An attacker could manipulate data or identity claims exchanged with the HR Portal to alter authorization logic and gain elevated privileges.
- **Impact:** High – unauthorized access to restricted features or data.
- **Mitigation:** Strict input validation, robust authorization checks, validation of identity claims, defense-in-depth.

---
