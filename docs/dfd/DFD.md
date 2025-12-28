## Data Flow Diagram (DFD)

This section presents the initial data flow diagram used for threat modeling.

### Components
- External User
- HR Portal (Web Application)
- Azure Active Directory (Azure AD)

### Data Flows
- User <-> HR Portal (HTTPS)
- User <-> Azure AD (HTTPS)
- HR Portal <-> Azure AD (HTTPS)

### Trust Boundaries
- Internet / Untrusted Network (RH Portal)
- External Identity Provider Boundary (Azure AD)


