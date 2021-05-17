At Zurich, there is much more to messaging than Exchange and the Outlook client.  Application have a need to connect to the messaging systems in multiple ways.  This document outlines the ways in which these are supported in a secure and consistent matter.

Please note that this document will not cover connections to the on prem Exchange environment, as Zurich has a stated goal of decommissioning that environment by the end of 2021.  



**Application Connectivity**

New application will need to connect to messaging services with protocols that support the Strong Authentication (OAUTH2) protocol.  The MS GRAPH API is preferred to this as it is the currently supported protocol from Microsoft for all O365 interactions.  Exchange Web Services can be used as long as the application has been developed to use OAUTH2 as its authentication method.

Protocols that only support Basic Authentication should be upgraded or retired.  If this is not possible, additional controls (and approval for their exceptions) will need to be implemented around these connections.  Azure AD CA (Conditional Access) would suffice for this purpose, and it can be used to limit connectivity to the source IP of the application.



**IMAP4/POP3 with Legacy Auth:**

Support for POP3 and IMAP access for approved applications will be provided for on premise applications only. Cloud applications that require the support of this protocol will need to seek a GIS security exception and be subject to additional O365 conditional access restrictions.

- Legacy protocols
- Only supports Basic Authentication in O365 (MS to deprecate Q2 2021)
- Must have additional GIS mandated controls in place for approved use

**IMAP4/POP3 with Modern Auth:**

Mailbox access via the POP3 and IMAP protocols  for applications is approved for applications using modern authentication (OAUTH2) protocols.

**SMTP:**
Support for SMTP relay access for approved applications is approved for:

- On Prem ERaaS (Email Relay as a Service)
- Cloud instances separate from Zurich's production O365 tenant
- Through the Zurich O365 tenant **only** where the recipients are internal Zurich employees

Relaying email through Zurich's O365 tenant to external employees is expressly prohibited for the following reasons:

- Passing automated email through our ProofPoint violates our Proofpoint licensing agreement
- Automated email has caused Zurich to be "blacklisted" in the past.  Keeping separate application email streams from the user streams limits the impact when this happens.
- Automated email volumes can trigger sanctions of our tenant via Microsoft policies


**MS GRAPH API (O365):**

- Microsoft API
- Uses Strong Authentication
- Basic Authentication at End of Life 


**EWS (Exchange Web Services):**

- Microsoft API
- Uses Strong Authentication
- Basic Authentication at End of Life 
- EWS is supported but deprecated, please use MS Graph where possible

![Decision Tree Cloud](Decision%20Tree%20Cloud.png) ![Decision Tree On Prem](Decision%20Tree%20On%20Prem.png)
