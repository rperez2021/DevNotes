---
id: 9dp5ez1p5cy0ib1h1h6luhj
title: STS - Security Token Service
desc: 'Notes on STS'
updated: 1650823311219
created: 1650823191109
---
## General Info

Security token service (STS) is a cross-platform open standard core component of the OASIS group's WS-Trust web services single sign-on infrastructure framework specification. Within that claims-based identity framework, a secure token service is responsible for issuing, validating, renewing and cancelling security tokens. The tokens issued by security token services can then be used to identify the holder of the token to services that adhere to the WS-Trust standard. Security token service provides the same functionality as OpenID, but unlike OpenID is not patent encumbered. Together with the rest of the WS-Trust standard, the security token service specification was initially developed by employees of IBM, Microsoft, Nortel and VeriSign.

In a typical usage scenario involving a web service that employs WS-Trust, when a client requests access to an application, the application does not authenticate the client directly (for instance, by validating the client's login credentials against an internal database). Instead, the application redirects the client to a security token service, which in turn authenticates the client and grants it a security token. The token consists of a set of XML data records that include multiple elements regarding the identity and group membership of the client, as well as information regarding the lifetime of the token and the issuer of the token. The token is protected from manipulation with strong cryptography. The client then presents the token to an application to gain access to the resources provided by the application. This process is illustrated in the Security Assertion Markup Language (SAML) use case, demonstrating how single sign-on can be used to access web services.

Software that provides security token services is available from numerous vendors, including the open-source Apache CXF, as well as closed-source solutions from Oracle (for interfacing with authentication services backed by an Oracle Database) and Microsoft (where STS is a core component of Windows Identity Foundation and Active Directory Federation Services). While security token services are themselves typically offered as web services used in conjunction with other web services, software development kits (SDKs) for native applications (such as cloud-storage clients) also exist.
