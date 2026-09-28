# Microsoft Entra ID & ServiceNow – SAML 2.0 SSO Lab

## From Challenge to Success

A hands-on Identity & Access Management (IAM) lab project integrating Microsoft Entra ID with ServiceNow through SAML 2.0 Single Sign-On.

The goal of this project was not simply to achieve a successful SSO login, but to understand the complete identity flow: authentication in Microsoft Entra ID, SAML communication, identity mapping in ServiceNow, role-based access, troubleshooting, and the final end-to-end user experience.

### Project Goal

Build, configure, troubleshoot and validate a working SAML 2.0 SSO integration between Microsoft Entra ID and ServiceNow in a personal lab environment.


## What I Built

This lab represents a complete identity and access workflow between Microsoft Entra ID and ServiceNow.

The environment includes:

- Microsoft Entra ID tenant with dedicated lab users
- ServiceNow Personal Developer Instance (PDI)
- Microsoft Entra Enterprise Application for ServiceNow
- SAML 2.0 Single Sign-On configuration
- Multi-Provider SSO in ServiceNow
- User and group-based application access
- X.509 certificate trust between Microsoft Entra ID and ServiceNow
- NameID and attribute mapping
- ServiceNow user mapping using email identities
- Role-Based Access Control (RBAC) with the ITIL role
- Separate End User and IT Support identities
- End-to-end validation through a ServiceNow incident workflow

- ## End-to-End Architecture

The lab validates the complete authentication and service workflow from the end user to IT support:

**End User → Microsoft Entra ID → SAML 2.0 Authentication → ServiceNow → User Mapping → Role-Based Access → Incident → IT Support**

### Authentication and Access Flow

1. The end user starts the ServiceNow sign-in process.
2. Microsoft Entra ID authenticates the user.
3. Entra ID sends the SAML authentication response to ServiceNow.
4. ServiceNow maps the authenticated identity to the corresponding user record using the email identity.
5. ServiceNow roles determine what the authenticated user is authorized to access.
6. The end user accesses the ServiceNow portal and creates an incident.
7. The IT Support user accesses the incident with the appropriate ITIL permissions.
8. The support response becomes visible to the end user in ServiceNow.
