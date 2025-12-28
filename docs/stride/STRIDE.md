# STRIDE Threat Analysis

## Spoofing (S)

### Threat 1
- **Threat:** User impersonation on HR Portal
- **Affected flow:** External User ↔ HR Portal
- **Description:** An attacker may impersonate a legitimate user or spoof the HR Portal to gain unauthorized access.
- **Impact:** High
- **Mitigation:** Azure AD authentication, MFA, secure session management.

### Threat 2
- **Threat:** Spoofed authentication response from Identity Provider
- **Affected flow:** HR Portal ↔ Azure AD
- **Description:** An attacker could attempt to spoof authentication responses if token validation is insufficient.
- **Impact:** Medium
- **Mitigation:** Token signature validation, issuer/audience checks, TLS.

---

## Tampering (T)

### Threat 1
- **Threat:** SQL Injection
- **Affected flow:** HR Portal → Cloud SQL Database
- **Description:** Malicious input could alter SQL queries, leading to unauthorized data modification.
- **Impact:** High
- **Mitigation:** Parameterized queries, input validation, least privilege.

### Threat 2
- **Threat:** Unauthorized modification of objects in storage
- **Affected flow:** HR Portal → Object Storage
- **Description:** An attacker may modify or replace stored documents if access controls are weak.
- **Impact:** Medium
- **Mitigation:** Strong access control, integrity checks, logging.

---

## Repudiation (R)

### Threat 1
- **Threat:** Lack of user action traceability
- **Affected flow:** User ↔ HR Portal
- **Description:** A user could deny performing sensitive actions due to insufficient logging.
- **Impact:** Medium
- **Mitigation:** Audit logs, centralized logging, timestamps.

### Threat 2
- **Threat:** Missing authentication event logs
- **Affected flow:** HR Portal ↔ Azure AD
- **Description:** Authentication actions may not be traceable if logs are incomplete.
- **Impact:** Medium
- **Mitigation:** Enable Azure AD logs, SIEM integration.

---

## Information Disclosure (I)

### Threat 1
- **Threat:** Data leakage over network
- **Affected flow:** User ↔ HR Portal
- **Description:** Sensitive data could be intercepted if transport security is misconfigured.
- **Impact:** High
- **Mitigation:** TLS, HSTS, secure headers.

### Threat 2
- **Threat:** Exposure of sensitive data in storage
- **Affected flow:** HR Portal → Cloud SQL Database
- **Description:** Sensitive HR data could be exposed due to weak encryption or access control.
- **Impact:** High
- **Mitigation:** Encryption at rest, RBAC.

---

## Denial of Service (D)

### Threat 1
- **Threat:** DoS attack on HR Portal
- **Affected flow:** User ↔ HR Portal
- **Description:** Excessive requests may render the portal unavailable.
- **Impact:** High
- **Mitigation:** Rate limiting, WAF, autoscaling.

### Threat 2
- **Threat:** Resource exhaustion on database
- **Affected flow:** HR Portal → Cloud SQL Database
- **Description:** Heavy queries could impact database availability.
- **Impact:** Medium
- **Mitigation:** Query limits, monitoring, alerts.

---

## Elevation of Privilege (E)

### Threat 1
- **Threat:** Privilege escalation via application flaw
- **Affected flow:** User ↔ HR Portal
- **Description:** An attacker may gain higher privileges due to improper authorization checks.
- **Impact:** High
- **Mitigation:** Role-based access control, authorization checks.

### Threat 2
- **Threat:** Excessive database privileges
- **Affected flow:** HR Portal → Cloud SQL Database
- **Description:** Over-privileged database accounts may allow unauthorized actions.
- **Impact:** High
- **Mitigation:** Least privilege, role separation.
