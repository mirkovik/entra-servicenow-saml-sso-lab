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

### End-to-End Architecture

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

### Troubleshooting & Problems Solved

A major part of this lab was troubleshooting the SAML authentication flow. The integration did not work immediately, and several issues had to be analyzed and resolved.

### 1. Redirect Failed

**Problem:**  
The normal ServiceNow SSO login returned:

`Redirect failed, please contact your administrator.`

**Analysis:**  
The Identity Provider connection test successfully redirected to Microsoft Entra ID and back to ServiceNow, but the normal login flow still failed. The ServiceNow Identity Provider was not active.

**Resolution:**  
The IdP activation was blocked by the mandatory connection-test requirement. The ServiceNow system property:

`glide.authenticate.multisso.test.connection.mandatory`

was temporarily set to `false`, allowing the IdP to be activated. After activation, the property was returned to `true`.

### 2. SSO Certificate Validation Error

**Problem:**  
ServiceNow returned:

`SSO certificate validation error`

**Analysis:**  
Multiple outdated or incorrect X.509 certificate entries were associated with the SAML configuration.

**Resolution:**  
The incorrect certificate entries were removed and the current Microsoft Entra SAML signing certificate was imported into ServiceNow.

### 3. username_invalid_error

**Problem:**  
The SAML communication reached ServiceNow, but authentication failed with:

`username_invalid_error`

**Analysis:**  
The ServiceNow NameID Policy was configured as `transient`, while the lab required a stable identity that could be matched to an existing ServiceNow user.

**Resolution:**  
The NameID format was changed to:

`urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress`

and Microsoft Entra ID was configured to use:

`user.mail`

as the identity source.

### 4. User Not Found

**Problem:**  
Microsoft Entra ID sent the correct email identity, but ServiceNow still returned:

`User not found`

**Analysis:**  
ServiceNow was searching for the authenticated identity in the `user_name` field instead of the `email` field.

**Resolution:**  
The ServiceNow system property:

`glide.authenticate.multisso.login_locate.user_field`

was changed from:

`user_name`

to:

`email`

The Identity Provider **User Field** was also configured as `email`.

After these changes, ServiceNow successfully mapped the SAML identity to the corresponding user record.
