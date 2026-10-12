# Technical Backup & Recovery Reference

This directory contains selected configuration exports from a Microsoft Entra ID and ServiceNow SAML 2.0 Single Sign-On (SSO) lab.

**Environment:** ServiceNow Personal Developer Instance (PDI), Zurich Release  
**Original Instance:** `dev356981`  
**Identity Provider (IdP):** Microsoft Entra ID  
**Service Provider (SP):** ServiceNow  
**Backup Date:** October 7, 2026

## Authentication Architecture

The lab demonstrates SAML 2.0 authentication between Microsoft Entra ID and ServiceNow.

The primary user identification mapping is:

`Microsoft Entra user.mail → SAML NameID (Email Address) → ServiceNow email`

Application access was controlled through Microsoft Entra security group assignments. ServiceNow roles and permissions were managed separately within ServiceNow.

## Backup File Index

| File | Record Type | Purpose |
|---|---|---|
| `08_ServiceNow_MultiSSOv2_SAML2_custom.xml` | `sys_script_include` | Export of the ServiceNow SAML 2.0 Script Include `MultiSSOv2_SAML2_custom`. |
| `09_ServiceNow_IdentityProvider_Microsoft-Entra-ID-CloudsDelight.xml` | `saml2_update1_properties` | Export of the configured Microsoft Entra SAML Identity Provider settings, including authentication endpoints and SSO configuration references. |

These files represent selected technical configuration records, not a complete instance backup.

Additional certificates, metadata, user records, and supporting configuration references are maintained separately in the local backup documentation.

## Safe Restoration Guidelines

1. **Do not perform blind XML imports.** Review exported records and dependencies before importing them into another ServiceNow instance.
2. **Update instance-specific URLs.** Replace references to the original PDI with the destination instance URLs where appropriate.
3. **Verify SAML configuration.** Review the Identity Provider settings, certificate references, metadata, and NameID mapping.
4. **Review access permissions.** Confirm Microsoft Entra application assignments and ServiceNow roles before testing.
5. **Test authentication carefully.** Validate SSO with a designated test account before enabling broader access.

## Security Notice

This repository is public and is intended for technical learning and project documentation.

Do not upload passwords, private keys, access tokens, confidential certificates, or personal user exports.

All configuration exports and screenshots should be reviewed for sensitive information before publication.

## Project Scope

This repository documents a successfully tested learning environment. It is not a production deployment, a complete disaster recovery package, or a guaranteed automated restoration solution.
