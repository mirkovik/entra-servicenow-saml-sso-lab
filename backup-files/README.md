# 📂 Technical Backup & Disaster Recovery Reference

This directory contains the production-ready structural configuration files exported from the ServiceNow Personal Developer Instance (PDI) `dev356981` before environment reclamation. 

---

## 📌 Architectural Synchronization Map

The authentication flow relies on mapping the primary security context between both infrastructure providers:

- **Identity Provider (IdP):** Microsoft Entra ID (`CloudsDelight.net`)
- **Service Provider (SP):** ServiceNow (Zurich Release)
- **Primary Matching Blueprint:** Microsoft Entra `user.mail` ↔ SAML `NameID` (Format: Email address) ↔ ServiceNow `email` field

---

## 🗃️ Backup File Index

| File Name | Component Type | Target Table / Scope | Purpose |
| :--- | :--- | :--- | :--- |
| `08_ServiceNow_MultiSSOv2_SAML2_custom.xml` | Global Property / Metadata | `saml2_update1_properties` | Core configuration for the underlying SAML 2.0 multi-SSO environment wrapper. |
| `09_ServiceNow_IdentityProvider_Microsoft-Entra-ID-CloudsDelight.xml` | Integration Profile | `sys_properties` / `sys_auth_provider` | Active identity provider profile including target endpoints and token signing contexts. |

---

## ⚠️ Safe Restoration Guidelines

When importing these reference records into a newly provisioned sandbox environment:
1. **Never apply blind bulk imports:** ServiceNow XML records retain strict instance-specific dependencies.
2. **Update Destination Endpoints:** Immediately open the imported Identity Provider record and dynamically alter all `dev356981` references to your new PDI identifier.
3. **Verify SSO Key Binding:** Ensure that the generated X.509 certificate reference matches the configuration state specified within the primary metadata properties.
