# Summary of Changes

{% hint style="info" %}
Please follow the [guide ](1-installation-of-the-bgmconnects-pbx/installation-of-bgmconnects-pbx-v22.3/upgrade-to-the-latest-version-within-v22.x-on-linux.md)to upgrading your PBX to the latest version.
{% endhint %}

## Changes for Release v22.3.21

Date: December 19, 2025

#### New Services and Features

* **Introduced the Data Flow Service**\
  Enables advanced analytics and reporting through real-time data processing.\
  Includes:
  * All-new Call Reports
  * Enhanced CDR with additional filters
  * Redesigned Dashboards and Wallboards for queue and agent metrics
* **CRM Integration** _(initially supports Zoho and HubSpot; more CRMs to follow)_\
  Provides seamless synchronization between PBX and CRM systems:
  * Automatic contact synchronization
  * Call logging and note-taking directly within the CRM
  * Ability to create and edit call notes
  * Unified interaction tracking from both the **PBX** and **BGMconnects App**
* **CRM Contacts Category**\
  Introduced a new _CRM Contacts_ section that categorizes contacts synchronized from connected CRM platforms.
* **AI Transcription Service**
  * Integrated with AWS and Microsoft Azure to provide automatic transcription for calls and voicemails.
  * Transcriptions are viewable in both the PBX Web Portal and the BGMconnects App.

***

#### Administration and Access Control

* **Multiple System Administrators**\
  Support for creating multiple system administrator accounts.
* **New Administrator Roles**\
  Introduced two new predefined roles with limited permissions:
  * Operations Admin
  * Site Admin
* **Customizable Administrator Roles**\
  Administrators can now create custom roles to fine-tune access permissions, enhancing role-based access control and operational flexibility.
* **User Access Limits**\
  System administrators can set per-tenant limits on how many users can access:
  * The BGMconnects App
  * The Teams Phone App

***

#### Security and Compliance Enhancements

* **Recording and Voicemail File Protection**\
  Strengthened access control for recordings and voicemail files:
  * Each file now includes both a Public Link and a Private Link.
  * Private Links require credential verification and role-based permission validation.
  * Tenant admins can choose whether to push Public or Private Links to the CRM.
  * When a CRM user clicks a Private Link, credentials are required to verify access.
  * All accesses to recordings and voicemails are now logged in the Audit Log.
* **Enhanced Audit Logging**\
  Added additional filters and detailed tracking for administrator and user activities.

***

#### Telephony and Call Handling

* **Virtual Receptionist Security**\
  Added the option to block direct extension dialling from the Virtual Receptionist, preventing callers from bypassing menu options.
* **Queue and Ring Group Enhancements**
  * Added support for Night Mode per IVR, Queue, or Ring Group.
  * Introduced Queue Exit Options for callers.
  * Added configurable Agent Wrap-Up Time after each call.
  * Added support for Periodic Announcements during queue waiting.
  * Introduced Agent Pause Codes for more accurate reporting.
* **Trunk Enhancements**
  * Added support for the `tel:` URI scheme in trunk configurations.
  * Added configuration for maximum call duration per trunk.
  * Enhanced outbound rule configuration to support SMS routing.
* **Voicemail Improvements**
  * Minimum PIN length increased to **4 digits** for better security.
* **Call Routing Enhancement**
  * If an extension declines a call, it will now follow the Busy Forwarding Rule.

***

#### Device and App Updates

* **New App Releases**
  * Released the BGMconnects Teams Phone App.
  * Released BGMconnects for macOS.
* **Device Support**
  * Added support for [Fanvil ](https://www.fanvil.com)W620W, V50P, V60P, and W series phones.
  * Added support for [Yealink ](https://www.yealink.com)T7x and T8x phones.
  * Added support for [Gigaset ](https://www.gigaset.com)IP and DECT phones.
  * Added support for [Intelbras ](https://www.intelbras.com/en)IP Phones
  * Added support for [SNOM ](https://www.snom.com/en/)headsets in the BGMconnects app.
  * DECT phone handset names can now be automatically set to the Extension Name.
* **Power Optimization**
  * Phones provisioned by the PBX now automatically disable power-saving mode to prevent missed calls.
* **Codec Configuration**
  * Added the ability to enable or disable codecs for IP phones during auto-provisioning.

***

#### Connectivity and System Improvements

* **SMS Integration**
  * Integrated with [SMSGlobal ](https://www.smsglobal.com/)for outbound and inbound SMS support.
  * Integrated with [CM.COM](https://cm.com) for voice calls and SMS support.
  * Integrated with [SIPTRUNK.COM](https://siptrunk.com) for the voice calls and SMS support.
* **IPv6 Support**
  * The system now automatically adapts to IPv6 environments — no manual configuration required.
***

#### Bug Fixes

* Fixed issues related to the **Diversion Header**.
* Other stability and performance enhancements across PBX core services.

***

## Changes for Release v22.2.25

Date: November 21, 2025

#### Enhancements

* If an outbound rule has multiple trunk routes, and a trunk with 486 or 603 rejects the call, the PBX will stop trying the next trunk route.
* Added Fanvil v50P, v60P phones.
* Added Yealink T7x and T8x phones.

#### Bug Fixes

* Fixed a bug where, if an SNOM phone performs the blind transfer to an app extension user who is offline but has activated push notifications(displayed as "push online" in the PBX web portal), it would cause the voice not to work.
* Fixed a bug where the phone BLF label was displayed incorrectly.

#### BGMconnects SBC v11.20

This version fixed a bug where, if the IM service was installed on a separate server, the WebRTC app would fail to connect to the IM server.

***

## Changes for Release v22.2.23

Date: November 6, 2025

#### Enhancements

* Improved trunk configuration handling – When editing a trunk, the system no longer reloads the trunk unless critical parameters (such as IP host, outbound proxy server, domain, or credentials) are modified. This prevents unnecessary deregistration and re-registration events.
* Optimized Twilio SMS response processing to improve reliability and consistency when handling message callbacks.
* Optimized log file management to improve storage efficiency and system stability.
* Enhanced CDR query performance for faster data retrieval and reporting.
* Improved audit log information to improve performance.
* Added new phone templates for the following devices:
  * Polycom 8800 series
  * AudioCodes 420 and 405 models
* Released BGMconnects SBC v11.1.10, which includes the new WebRTC app version.

#### Bug Fixes

* Fixed a routing issue that could occur when modifying the trunk DID pool or inbound/outbound rules, which in some cases prevented calls from being routed through the trunk.
* Corrected a display issue where Snom phones did not show contact names from the phonebook.
* Fixed an inbound message handling issue for VoIP Innovations trunks.
* Fixed an issue where filesystem inodes were not released correctly after file operations in Linux, which could lead to unnecessary disk space consumption over time.

***

## Changes for Release v22.2.22

Date: October 15, 2025

#### Enhancements

* Calls that fail with 486or 603 are now automatically forwarded to voicemail. All other 4xx/5xx failures terminate the call immediately.
* Reduced the size of NOTIFY messages for the dialog-info (BLF) event to help prevent MTU issues when using UDP transport.
* Enabled the **allow\_rtp\_on\_mute** option by default in the Snom phone template.
* Set the extension name for the DECT phone handset.

#### Bug Fixes

* Fixed an issue where the Diversion header was incorrectly set up when sending calls to a SIP trunk.
* Fixed an issue where the voicemail playback date was played incorrectly in English.
* Fixed an issue where the transfer key was configured incorrectly on SNOM and Yealink phones during auto-provisioning.

***

## Changes for Release v22.2.21

Date: September 28, 2025

#### Enhancements

* The SIP **Contact** header no longer includes a display name by default.

#### Bug Fixes

* Fixed an issue where, with multiple extensions registered and **Push Notifications** enabled, active calls could cause the **callmanager** service to crash(only occurs if the PBX is the v22.2.20).
* Resolved two queue-handling issues when a queue has only **one** agent who has **Push Notifications** enabled and whose phone is in the background with the network disabled (e.g., Wi-Fi/Cellular off or Airplane Mode):
  * The agent could remain stuck in **ONCALL** status after the caller timed out in the queue and hung up.
  * The caller might not receive the SIP **BYE** message after the call timed out in the queue and ended.

***

## Changes for Release v22.2.20

Date: September 18, 2025

#### Enhancements

* **Webhook Reimplementation**\
  The webhook has been fully reimplemented for improved stability and reliability.
* **Enhanced BLF Functionality**\
  Resolved an issue where IP phones provisioned via the SBC could not be reprovisioned or rebooted after registration.

***

## Changes for Release v22.2.19

Date: August 21, 2025

#### New Feature Support

* **Virtual Receptionist Action URL**\
  Now supports matching DTMF inputs using the `*`. Each `*` represents a single DTMF digit.
* **Microsoft 365 SSO**\
  The PBX now authenticates Microsoft 365 usernames in a case-insensitive manner, ignoring upper and lower case differences.
* **Mobile App Push Certificates**\
  Optimized the automatic update process for push notification certificates.

***

## Changes for Release v22.2.17 <a href="#changes-for-release-v22.2.17" id="changes-for-release-v22.2.17"></a>

Date: July 28, 2025

**New Features Support**

* Introduced a new _Company Call Session_ permission that enables users to monitor and manage live calls within their tenant’s scope.
* Added support for **German**, **Dutch**, and **Vietnamese** languages, including localized **voice prompts**.

**Bug Fixes**

* Resolved an issue where the iOS push certificate auto-renewal process failed to update correctly.
* Fixed a bug where newly created extension users were unable to connect to the Instant Messaging (IM) service.
* Corrected an issue where call reports for queues were occasionally generated incorrectly under specific edge-case scenarios.
* Fixed a bug where, in deployments using **IPv6**, the app received push notifications for incoming calls but **failed to answer** them.
* Addressed a compatibility issue when configuring the **SMTP server with AWS SES**, which previously caused email delivery failures.
* Corrected a bug where an extension **removed from a chat group** would be **re-added upon signing back into the app**.
* Fixed an issue where queue agents or ring group members could remain in the "ON CALL" status without active calls under certain conditions.
* Resolved a memory leak in the queue server in specific scenarios.
* Fixed a failure in completing Google Workspace integration.

***

## Changes for Release v22.2.14

Date: Jun 12, 2025

{% hint style="danger" %}
If you are upgrading from a version earlier than v22.2.11. You must update the SBC web portal with the new token.
{% endhint %}

### Enhancements

* Improved Recording File Upload Performance: Added new parameters in system.ini to configure the number of threads used for uploading call recordings to AWS S3 or Azure Blob Storage. This enhancement significantly improves upload speed and efficiency.
* Optimized CDR Generation for Declined Queue Calls: Prevent generating excessive Call Detail Records (CDRs) when an agent in the queue declines a call with SIP response 488.

### Bug Fixes

* Fixed an issue where call reports for ring groups were not generated correctly.
* Resolved a problem where importing extension users with IP Phone provisioning, or creating an extension with auto auto-provisioned phone, could cause the provisioning process to fail.
* Fixed an issue where using the same phone number for both WhatsApp and voice calls with different inbound rules could result in WhatsApp messages being delivered to the wrong destination extension.
* Fixed an issue where enabling “Call Recovery” caused incoming calls initiated via the REST API to fail to be answered properly.

***

## Changes for Release v22.2.11

Date: May 15, 2025

{% hint style="danger" %}
After upgrading from a previous version to v22.2.x, the SBC token is automatically regenerated. To ensure continued functionality, you must update the SBC web portal with the new token.
{% endhint %}

### New Features and Enhancements

* Added **night mode support** for Queues, Ring Groups, and Virtual Receptionists. When night mode is active, calls are forwarded to a predefined destination.
* Enabled **BLF key integration for night mode** on supported IP phones, allowing activation and deactivation via BLF key press.
* Added support for **activating/deactivating night mode** directly from the BGMconnects app.
* Added support for **Two-Factor Authentication (2FA)** via email verification code for **web portal login and app login**. Requires proper email server configuration by the administrator.
* Added the ability to **reset passwords by sending a reset link via email** for users who forget their login credentials.
* Introduced **PIN-protected calling**. When dialing a Feature Access Code (FAC) followed by a number, the PBX prompts the user to enter their voicemail PIN before placing the call.
* Added a new FAC to allow users to **set/unset their default outbound caller ID**.
* Enabled **Enhanced Call Park support for SNOM phones**.
* Integrated the SMS API and SIP trunk with the provider [CM.com](https://www.cm.com)
* Added **email notification support** when the **trunk concurrent call limit** is reached.
* Improved agent handling in Queues and Ring Groups: if an agent **declines a call**, it will no longer be offered to that agent again during the same session.
* Updated call decline behavior: when an extension **declines a call**, it is now **routed to voicemail** instead of being disconnected.
* Added support for **joining meetings via URL link**.
* Added **auto-provisioning support for Aastra/Mitel 6xxxi IP phones**.
* Improved transfer handling: the PBX now updates the **caller and callee name and number** using the **PAI header** in re-INVITE after blind or attended transfers.
* **Caller display name delivery behavior**: In the following scenarios, the **caller display name will be replaced with the tenant’s name (company name)**:
  * A queue callback call is sent to the caller after an agent answers.
  * A call is placed from an extension that belongs to a user group, and the group’s caller ID is applied.
  * A call times out, fails, or is forwarded during night mode by the Virtual Receptionist to a trunk number.
  * A call times out or is forwarded during night mode by the Queue to a trunk number.
  * A call times out or is forwarded during night mode by the Ring Group to a trunk number.
* Updated **redirect URI** for Microsoft 365 integration. After upgrading to v22.2, the new URI must be configured in Microsoft 365 settings.
* Extended the **validity period of mobile app push notifications** from 3 to 7 days. This value is now configurable in the `system.ini` file.
* **Default header behavior changes in version 22.2**: Starting from v22.2, the following settings are **disabled by default** for Queues and Ring Groups:
  * Adding ring group or queue information to the `P-Asserted-Identity` header.
  * Adding ring group or queue information to the `Remote-Party-ID` header.
* Added an SRTP policy option in the SBC web portal to control whether SRTP information is included in the SDP.

### Bug Fixes

* Fixed an issue where **emergency calls should not be billed**.
* Fixed a bug where WhatsApp trunks always appeared offline.
* Resolved a problem with inbound WhatsApp messages using an incorrect phone number.
* Fixed an issue where anonymous calls to trunks were missing the required `Privacy` header.
* Corrected the `extension_agent_status` message to use string values for extension ID instead of a numeric value.
* Fixed an issue where webhook thread numbers were incorrectly managed.
* Resolved a bug where, if all queue agents were busy and the call timed out, the "No Answer" destination was not triggered.
* When a user declines a call on one device, the CANCEL message sent to other devices now includes a `Reason` SIP header with cause `200` and text `"Busy"`.
* Fixed a bug where REST API-initiated a call that was not answered on the caller side could cause recording issues on subsequent calls.
* Resolved a problem in Ring Groups where, if the last agent declined the call and "Repeat on No Answer" was enabled, the caller was disconnected.
* Fixed a bug in Advanced Routing logic where only the last configured route would take effect.
* Corrected an issue where calls were still being routed to an outdated IP/port of an Accept Register Trunk after registration refresh.
* Fixed a bug in BGMconnects app where switching between Wi-Fi and mobile networks during a call caused disconnection.

## Changes for Release v22.1.7

Date: Feb 27, 2025

### New Features & Enhancements

* **OAuth Integration with Microsoft 365 and Google Workspace**\
  PBX system administrators and tenants can now authenticate email notifications using OAuth for Gmail and Microsoft 365 accounts.
* **Apply Mail Server Settings to All Tenants**\
  A new feature allows tenants to adopt the system administrator’s mail server settings for email notifications, ensuring consistent configuration across all tenants.
* **SMS and WhatsApp Message Records**\
  The system now supports listing and querying records for both SMS and WhatsApp messages, providing better tracking and management of communications.
* **Trunk Integration with VoIP Innovations, Bandwidth, and Flowroute**\
  Users can now easily configure trunks and integrate with the SMS API for VoIP Innovations, Bandwidth, and Flowroute, simplifying trunk setup and management.
* **New SIP Header – X-Info**\
  A new SIP header, _X-Info_, has been introduced to enhance the transmission of call information for improved troubleshooting and analytics.
* **Removal of X-Trunk-Name SIP Header**\
  The _X-Trunk-Name_ SIP header has been removed. Trunk-related information will now be transmitted via the _X-Info_ header for better standardization.
* **Azure Blob Storage Support**\
  Added support for storing call recordings and voicemail files in Azure Blob Storage, offering flexible and scalable storage options.
* **BLF Subscription for System Extensions**\
  System extensions can now subscribe to other system extensions' BLF status. Previously, only extensions could subscribe to the BLFs of other extensions.
* **Updated Feature Access Code (FAC) Format Rules**\
  The format rules for Feature Access Codes (FAC) have been updated to ensure better compatibility and user experience.
* **Optimized CDR Query Performance**\
  Performance improvements have been made to enhance the efficiency and speed of Call Detail Record (CDR) queries.
* **Increased REST API Rate Limit**\
  The REST API rate limit has been increased to 10,000 requests per minute, improving scalability and performance for high-traffic applications.
* **SMTP Authentication Mode – IP Authentication**\
  A new “None” option has been added to the SMTP Authentication Mode settings for use with SMTP servers that employ IP address-based authentication.
* **Chat Group Member Limit**\
  The maximum number of members allowed in a chat group has been increased to 200, providing greater flexibility for team communication.
* **Handset Language for SNOM DECT M100 Auto-Provisioning**\
  Support has been added for setting the handset language during auto-provisioning of SNOM DECT M100 devices, ensuring smoother user experiences.
* **User and Engineer Passwords for SNOM DECT Auto-Provisioning**\
  Fields for User and Engineer passwords have been added in the auto-provisioning setup for SNOM DECT M300, M400, M700, and M900 devices.
* **Web Portal Optimization**\
  The web portal has been optimized to enhance usability and provide a more intuitive user interface, improving the overall user experience.

### Bug Fixes

1. **Trunk ACK Delay Handling**\
   Fixed a bug where slow ACK responses from the trunk to the PBX prevented calls from being offered to queue agents.

## Changes for Release v22.0.42

Date: Jan 16, 2025

* Fixed an issue where the client app’s username was displayed incorrectly when the app was offline but push notifications were enabled.&#x20;
* Resolved an issue where inbound calls to a queue via a trunk were not routed to an agent if the trunk’s ACK response was delayed.&#x20;
* Corrected a bug where the outbound caller ID specified in a REST API call was not properly recorded in the CDR.

***

## Changes for Release v22.0.39

Date: Jan 2, 2025

* Fixed an issue where inbound rules were not being applied correctly when a holiday was configured.&#x20;
* Resolved a bug with Advanced Routing, where the “all” option was not properly matching year/month parameters.&#x20;
* Corrected an issue where exception forwarding rules failed to match the caller number under certain scenarios.&#x20;
* Fixed a display issue where the caller’s display name was incorrect when calling into a ring group or queue.

***

## Changes for Release v22.0.38

Date: Dec 12, 2024

* Optimized performance: 2 cores, 4GB memory for up to 1,000 online users, supports \~500 simultaneous calls
* BGMconnects app: Available for WebRTC, Windows, iOS, and Android (macOS support coming soon)
* SSO login: Support for Microsoft 365 accounts across WebRTC, Windows, iOS, and Android apps
* Messaging features: Group chat, offline messaging, sync messages across devices, support for SMS and WhatsApp messaging
* Call management: Optimized for blind and attended call transfers, Call Flip and Call Park features within the app, Call Park notifications for easy retrieval, Visual voicemail in the app
* Customization options: Themes and emoji support, customizable caller ID for calls and SMS, manage personal and company contacts, easy import of contacts
* Synchronization across devices and apps: Sync presence and custom status, sync DND status across apps and IP phones, auto-sync extension users and CDR across apps
* VoIP trunk and SMS API integrations: Pre-configured trunks for Vonage, QuestBlue, VoIP.ms, Voxtelesys, Wavix, Twilio, Telnyx, Aire Networks, VoiceMeUp
* Phone support: Support for FANVIL DECT Phones (MODE and V66 models), SNOM phones, Yealink W73B DECT Phones, auto-provisioning for Grandstream GXP2604, HTEK phones
* Security and routing enhancements: STIR/SHAKEN support for enhanced call security, call routing based on extension presence status
* Administrative features: Tenant admins can manage Speed Dial 8 and Speed Dial 100 settings
* Operating system support: Linux (Debian 11/12, Ubuntu 22.04/24.04), Windows (10 1903/19H1 or higher, Windows Server 2022 or higher)
* Language support: Japanese language support

***

