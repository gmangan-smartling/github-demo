Overview
========

Zoom Phone is Zoom's cloud-based telephony service designed to meet the telephony needs for businesses of any size. Featuring an intuitive, web-based admin menu for settings and policies, and a cloud-based service architecture that replaces legacy, on-premises equipment, Zoom Phone makes telephony simple.

This section provides an overview of Zoom Phone's services, architecture, design, network requirements, security standards, supported devices, features, licenses, and more. After reading this section, you can expect to gain a high-level understanding of Zoom Phone's fundamental design elements and functionality.

#### <mark style="color:blue;">Zoom Phone offers three primary service offerings: Native, BYOC Cloud Peering, and BYOC Premises Peering</mark>

Zoom Phone offers businesses three primary service offerings to meet diverse needs across the globe: **Zoom Phone Native** , **Zoom Phone Bring Your Own Carrier with Cloud Peering (BYOC-C)** , and **Zoom Phone Bring Your Own Carrier with Premises Peering (BYOC-P)** . Each of these services are briefly described in the following sections, with a network summary available at the end of each service's description.

{% content-ref url="zoom-phone-native.md" %}
[zoom-phone-native.md](zoom-phone-native.md)
{% endcontent-ref %}

{% content-ref url="bring-your-own-carrier-cloud-peering-byoc-c.md" %}
[bring-your-own-carrier-cloud-peering-byoc-c.md](bring-your-own-carrier-cloud-peering-byoc-c.md)
{% endcontent-ref %}

{% content-ref url="bring-your-own-carrier-premises-peering-byoc-p.md" %}
[bring-your-own-carrier-premises-peering-byoc-p.md](bring-your-own-carrier-premises-peering-byoc-p.md)
{% endcontent-ref %}

#### <mark style="color:blue;">Zoom Phone is designed with an active-active architecture for reliability and resiliency</mark>

Zoom Phone uses a best-in-class, active-active architecture to deliver reliable, enterprise-grade phone service. Details of this design are elaborated in the following sections, with a focus on data center-specific SIP zones and Zoom's data centers at large.

### Zoom Phone Data Center SIP Zones

In an active-active architecture, resiliency and redundancy are key. Each Zoom Phone data center features two identical, interconnected SIP zones equipped with dedicated hardware and services for independent resiliency and sustainability.

During normal operations, a load balancer evenly distributes calls between both SIP zones within a data center. Within each SIP zone, calls are equitably distributed among a cluster of call switches, which are responsible for various functions such as call routing, setup, and teardown. From the call switches, calls connect to a Session Border Controller (SBC) within each zone, which connects to Zoom's underlying network of providers for PSTN routing until the call reaches its final destination.

Within this framework, each integral piece of architecture—i.e., SBCs, load balancers, and call switches—is supplemented with redundant hardware on standby for resiliency. In the event that one SIP zone experiences a service-impacting event, a call's active media, signaling, and registration will failover to the other zone for uninterrupted service.

The following diagram illustrates a SIP zone's active-active architecture design at a high level:
<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXcaXOw7Bu4ZXR75kgEYWSh6IBU4P_G6DOUGuE8OQ1zvgGln0to_91pq8BY9N-2cmzn24uMorcOayjSp2Y_g9_zpCjHBKHWbja2Qh988ncL6TUs8zHh1ZkANbXk3Mr5wB8uZr1zDkhIucgemMtCxngk?key=gORaE6vjeZ6i7Y4PGyLKfw" alt="" width="563"><figcaption><p>Diagram of a SIP zone's active-active architecture.</p></figcaption></figure> 

### Zoom Phone Data Centers At Large

From a physical perspective, Zoom's data centers are located within highly secure colocation facilities with physical security, redundant power and cooling systems, and access to leading carrier-neutral internet service providers (ISPs) and peering partners.

From a technological perspective, Zoom's data centers are built with fault-tolerant architecture, including full redundancy and rapid failover capabilities from a primary data center to a secondary data center, to enhance reliability and minimize downtime.

In the unlikely event of a complete data center outage or service-impacting event, Zoom Phone media, signaling, and registration information may be temporarily lost, requiring a convergence on the standby, secondary data center.

The following diagram illustrates Zoom’s data center redundancy design at a high level:
<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXfRZ-QerC-_7-wr6qOfb5lHUQ9x9bFHPozJutStPSc9ykAroO56EAaipWz2KpDSEHXR9TIinValkP20Rz07ffEUYZTLUF6v09x48u7Jo8DD8xgrIvS_1S1_oimOP_EiSkl7mL7cLxjDCqaPoo-2LQ?key=gORaE6vjeZ6i7Y4PGyLKfw" alt="" width="563"><figcaption><p>Diagram of Zoom's data center redundancy design.</p></figcaption></figure> 

### SIP Zone Service Locations

Zoom Phone offers PSTN connectivity where Zoom provides native telephony services. In addition, customers hosted on Zoom’s United States–based cluster (US01) can benefit from SIP Zone connectivity through Zoom’s global media infrastructure, which includes the following data center locations to optimize call quality and routing based on user location:

{% columns %}
{% column %}
**North America:** 

* U.S. West, California
* U.S. Central, Colorado
* U.S. East, New York
* U.S. East, Virginia

**Latin America:** 

* Brazil, São Paulo
* Mexico, Querétaro {% endcolumn %}

{% column %}
**EMEA:** 

* Netherlands, Amsterdam
* Germany, Frankfurt
* Saudi Arabia, Riyadh
* Saudi Arabia, Jeddah

**APAC:** 

* Australia, Sydney
* Australia, Melbourne
* China, Hong Kong
* Japan, Tokyo
* Japan, Osaka
* Singapore, Singapore {% endcolumn %} {% endcolumns %}

#### <mark style="color:blue;">Region-Specific Connectivity</mark>

For customers that require data localization for compliance purposes and are located in supported regions, Zoom Phone also supports localized PSTN connectivity for region-specific accounts. Customers with a region-specific account are forced to initialize all calls from their region's associated data center and cannot utilize SIP zones outside of their account's region.

The following list details supported regions and region-specific data center locations available with Zoom Phone:

{% columns %}
{% column %}
**Australia** 

* Sydney
* Melbourne

**Canada** 

* Vancouver
* Toronto {% endcolumn %}

{% column %}
**Europe** 

* Germany
* Amsterdam

**Zoom for Government** 

* California
* New York {% endcolumn %} {% endcolumns %}

{% hint style="warning" %}
**Warning** 

Phone calls placed from region-specific accounts will transmit from data centers within the region; however, PSTN calls may traverse international networks beyond their confined region.
{% endhint %}

### Zoom Phone India

Apart from localized regions, Zoom Phone also supports Bring Your Own Carrier with Premises Peering (BYOC-P) connectivity within India through a specialized Zoom Phone India service offering. With Zoom Phone India, customers with a U.S. cluster-based account are provided with a unique Zoom Phone instance specific to the licensed service areas—also known as circles—where both Zoom and the customer account are authorized to operate.

As of the date of this document's publication, Zoom is authorized to operate within the following licensed service areas:

* **Mumbai:** Local area of Mumbai, Navi Mumbai, and Kalyan
* **Andhra Pradesh:** State of Andhra Pradesh and Telangana, including Hyderabad
* **Maharashtra:** State of Maharashtra and Goa, including Pune
* **Karnataka:** State of Karnataka, including Bangalore
* **Tamil Nadu:** State of Tamil Nadu and union territory of Pondicherry, including Chennai
* **Delhi:** Local area of Delhi, New Delhi, Ghaziabad, Faridabad, Noida, and Gurgaon

#### <mark style="color:blue;">Zoom Phone India Requirements</mark>

Due to regulatory requirements, a business must meet certain criteria to be eligible for the Zoom Phone India service. Although the following list is not comprehensive, the most important criteria are outlined below:

* The business **must** pay with the Indian Rupee, and cannot use another denomination like the U.S. Dollar or Euro
* The business **must** be a business entity registered with the Government of India and cannot be an international entity
* The business **must** have both an authorized signatory and a Goods and Sales Tax Identification Number (GSTIN) within the state where they are getting service
* The business **must** be located within one of Zoom's currently supported licensed service areas

If your business meets these requirements and is interested in learning more about Zoom Phone India, reach out to your account team for more information.

### Security Standards

Zoom Phone supports secure voice calls across various platforms, including the Zoom Workplace app for desktop and mobile, the Zoom web client, Zoom Rooms, and supported SIP devices.

During call setup, Zoom Phone utilizes SIP over TLS 1\.2 with an AES 256-bit algorithm for encryption. Additionally, connections from the Zoom Workplace app for desktop and mobile, as well as the Zoom web client, encrypt call media to the Zoom Cloud using secure real-time transport protocol (SRTP) with AES 256-bit encryption.

Supported SIP devices configured with SRTP use either AES-128 or AES-256-bit algorithms for encrypting call media, while unencrypted RTP is utilized as a fallback for devices without SRTP support.

{% hint style="info" %}
**Note** 

By default, AES-128-bit encryption is enabled for call media transmitted by supported SIP devices. Admins can [upgrade devices to AES-256 bit encryption](https://support.zoom.com/hc/en/article?id=zm_kb&sysparm_article=KB0069186#h_01ECXCAW1EWJ42PMJZ41G8SN9G) using the web portal. Fax lines may not support full encryption.
{% endhint %}

### Supported Platforms, Devices, and Hardware

In addition to the Zoom Workplace desktop and mobile apps and Zoom Rooms app, Zoom Phone supports a growing list of IP phones, telephony hardware, and accessories.

The following lists contain supported **hardware manufacturers** for Zoom Phone, not specific models. Because Zoom Phone continues to support new hardware over time, visit Zoom's support center to see the most recent list of [Zoom Phone-certified hardware](https://support.zoom.com/hc/en/article?id=zm_kb&sysparm_article=KB0060242), including supported models, firmware versions, and supported encryption standards available for each.

#### <mark style="color:blue;">Supported Platforms</mark>

Zoom Phone is supported natively within the following platforms:

{% columns %}
{% column width="50%" %}

* Zoom Workplace Mac desktop app
* Zoom Workplace Windows desktop app
* Zoom Rooms app {% endcolumn %}

{% column %}

* Zoom Workplace Android mobile app
* Zoom Workplace iOS/iPadOS mobile app {% endcolumn %} {% endcolumns %}

#### <mark style="color:blue;">Google Chrome Web App</mark>

Zoom Phone has limited feature support within the Zoom for Chrome Zoom Web App, which allows users to use some of the same features available on the Zoom Workplace desktop or mobile app within a Google Chrome web browser.

Refer to Zoom's support center for more information on the [Chrome Web App](https://support.zoom.com/hc/en/article?id=zm_kb&sysparm_article=KB0059744), or speak to your Zoom account team for more information on feature parity and capabilities.

#### <mark style="color:blue;">Supported IP Phone Manufacturers</mark>

Zoom Phone supports limited IP phone models from the following manufacturers:

{% columns %}
{% column %}

* AudioCodes
* Avaya
* Cisco
* Grandstream {% endcolumn %}

{% column %}

* Mitel
* Poly
* Yealink {% endcolumn %} {% endcolumns %}

#### <mark style="color:blue;">Supported IP Phone Accessory Manufacturers</mark>

Zoom Phone supports limited IP phone accessories from the following manufacturers:

{% columns %}
{% column %}

* Poly {% endcolumn %}

{% column %}

* Yealink {% endcolumn %} {% endcolumns %}

#### <mark style="color:blue;">Supported Analog Gateway Manufacturers</mark>

Zoom Phone supports limited analog gateway devices from the following manufacturers:

{% columns %}
{% column %}

* AudioCodes
* Cisco {% endcolumn %}

{% column %}

* Grandstream
* Poly {% endcolumn %} {% endcolumns %}

#### <mark style="color:blue;">Supported Session Border Controller (SBC) Manufacturers</mark>

Zoom Phone supports limited Session Border Controllers from the following manufacturers:

{% columns %}
{% column %}

* AudioCodes
* Avaya
* Cisco
* Mitel {% endcolumn %}

{% column %}

* NextGen
* Oracle
* Ribbon
* TE-Systems {% endcolumn %} {% endcolumns %}

#### <mark style="color:blue;">SBC Requirements</mark>

To integrate an SBC with Zoom Phone, an SBC must meet the following requirements:

{% columns %}
{% column %}

* Support for TLS 1\.2 and SRTP
* Support for Mutual TLS
* Session Initiation Protocol (SIP)
* DTMF (RFC-2833) {% endcolumn %}

{% column %}

* Topology hiding (RFC-5853)
* SIP Early Offer (mandatory)
* **Codecs:** Opus, G.711 μ-law, G.711 A-law and/or G.729 {% endcolumn %} {% endcolumns %}

#### <mark style="color:blue;">Supported Pagers and Intercom Systems</mark>

Zoom Phone supports limited pagers and intercom systems from the following manufacturers:

{% columns %}
{% column %}

* 2N
* Algo {% endcolumn %}

{% column %}

* CyberData
* Grandstream {% endcolumn %} {% endcolumns %}

#### <mark style="color:blue;">Supported Codecs</mark>

By default, the Zoom Workplace desktop and mobile apps will use the Opus codec when connecting to a call; however, Zoom Phone also supports the following codecs for physical devices:

{% columns %}
{% column %}

* Opus
* G.711 μ-law {% endcolumn %}

{% column %}

* G.711 A-law
* G.729 {% endcolumn %} {% endcolumns %}

### Zoom Phone Features

The following lists outline core features available with Zoom Phone. As the Zoom Phone team continually innovates, additional unlisted features may also be available. If a feature important to your organization is not listed, please contact your account team for more information. Feature availability may be impacted by a user's [license](licenses-calling-plans-and-add-ons.md#zoom-phone-licenses) and [calling plan](licenses-calling-plans-and-add-ons.md#zoom-phone-calling-plans).
<table><thead><tr><th valign="top">Zoom Phone User Features</th><th valign="top">Zoom Phone Administration Features</th><th valign="top">Audio Prompt Language Support</th></tr></thead><tbody><tr><td valign="top"><ul><li>Call Blocking</li><li>Call Delegation</li><li>Call Forwarding</li><li>Call Handling Settings</li><li>Call Handoff Between Devices</li><li>Call History</li><li>Call Hold</li><li>Call Me On</li><li>Call Monitoring (Listen, Whisper, Barge, Take Over)</li><li>Call Park</li><li>Call Presence Status</li><li>Call Queue Chats Channels</li><li>Call Queue Opt-In/Out</li><li>Call Recording</li><li>Enhanced Call Transfer</li><li>Caller ID</li><li>Desk Phone Screen Lock</li><li>Elevate Call to Meeting</li><li>Emergency Calling</li><li>End-to-End Encrypted Calls</li><li>Multi-Party Conference Call</li><li>Multi-Key and Position Support</li><li>Personal Business Hours</li><li>Personal Holiday Hours</li><li>Personal Hold Music</li><li>Personal PIN Code</li><li>Push-to-Talk</li><li>Select Outbound Caller ID</li><li>SMS</li><li>Video Mail</li><li>Voicemail</li><li>Voicemail Transcription</li></ul></td><td valign="top"><ul><li>Auto Receptionists</li><li>Blocked Number List</li><li>Bulk Site Creation/Management</li><li>Business Hours</li><li>Call Journey Analytics</li><li>Call Logs</li><li>Call Recording (Ad Hoc, Automatic)</li><li>Call Queues (Callbacks, Routing Overrides)</li><li>Common Area Phones</li><li>Common Area Mobile Support (iOS/Android)</li><li>Configure Email Notifications</li><li>Configure IP Phone Settings</li><li>Customizable Wallboards (Call Queues/Auto Receptionists)</li><li>Define Call/SMS Hours</li><li>Define Call/SMS Locations</li><li>Device Management</li><li>Dial by Name Directory</li><li>Emergency Services</li><li>End-of-Call Feedback Survey</li><li>External Contacts</li><li>Frontline Worker Auto-Provisioning</li><li>Hold Music</li><li>Hot Desking</li><li>Global Consent Management for SMS</li><li>Inbound Call Insights</li><li>Inbound SMS Virus Screening</li><li>IP Address Access Control</li><li>Live Transcriptions</li><li>Mask Personal Data from Dashboard and Call Log</li><li>Multiple Brands and Campaigns (10DLC) </li><li>Multiple Line Appearances </li><li>Paging</li><li>PCI Compliance Support</li><li>PIN Code Requirements and Protections</li><li>Port Range Assignment</li><li>Provisioning Template</li><li>Provision Pending Users</li><li>Push-to-Talk</li><li>Quality Dashboards</li><li>Regional SMS/MMS Storage</li><li>Routing Rules</li><li>SAML Role Mapping</li><li>Shared Line Groups</li><li>Single Sign-On License Assignment</li><li>Site Management</li><li>Smart IVR</li><li>SMS Etiquette Tool</li><li>SMS Security Controls (Disable Hyperlinks, Block Attachments, Disable Group MMS, Character Limits, Emoji Controls)</li><li>Spam Number List</li><li>Spam Protection</li><li>Subscribe to Zoom Phone Reports</li><li>Voicemail PIN Brute Force Protection</li></ul></td><td valign="top"><ul><li>Arabic</li><li>Bengali</li><li>Catalan</li><li>Chinese (Cantonese)</li><li>Chinese (Traditional)</li><li>Chinese (Simplified)</li><li>Czech</li><li>Danish</li><li>Dutch</li><li>English (America)</li><li>English (Britain)</li><li>Estonian</li><li>Finnish</li><li>French (Canada)</li><li>French (France)</li><li>German</li><li>Greek</li><li>Hebrew</li><li>Hindi</li><li>Hungarian</li><li>Indonesian</li><li>Italian</li><li>Japanese</li><li>Korean</li><li>Malay</li><li>Persian</li><li>Polish</li><li>Portuguese (Brazil)</li><li>Portuguese (Portugal)</li><li>Romanian</li><li>Spanish (America)</li><li>Spanish (Spain)</li><li>Swedish</li><li>Tagalog</li><li>Tamil</li><li>Telugu</li><li>Thai</li><li>Turkish</li><li>Vietnamese</li><li>Ukrainian</li></ul></td></tr></tbody></table> 

### Fax Support

Zoom's Online Fax lets licensed Zoom Phone users send and receive faxes through the Zoom Workplace app using Zoom-provided or BYOC numbers, supporting up to 300 pages per fax with multiple file formats and cloud storage integration. The feature includes folder management, preview/download capabilities, bulk actions, enhanced fax transmission retries, detailed reporting, and persistent follow-up notes. 

For more information on the new Online Fax capabilities, please visit Zoom’s [support documentation on Online Fax](https://support.zoom.com/hc/en/article?id=zm_kb&sysparm_article=KB0079042).

### Licenses, Calling Plans, and Add-Ons

Zoom Phone provides a wide range of licenses, calling plans, and add-ons to cater to various customer requirements. Fundamentally, every user or device utilizing Zoom Phone requires a Zoom Phone Basic license to access core PBX features. For Zoom Phone Native users (i.e., non-BYOC-C/P), a calling plan is essential for making outbound calls; alternatively, BYOC-enabled accounts will incur charges from the underlying carrier for their usage.

In addition to calling plans, Zoom also offers several add-ons for both Native service and BYOC-C/P customers, offering users additional features, capabilities, and functionality.

{% hint style="info" %}
**Note** 

Some Zoom pricing plans include bundled licenses which, when applied to a user, may automatically apply a Zoom Phone calling plan and add-on features, simplifying the provisioning process. For more information on bundled licenses, speak to your Zoom account team.
{% endhint %}
<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXeKoG_K5hyyziw4KG0-4uFnNxQtUTntGWVU8jFefA_iq3DPjfu6mQHXLQpFMztK-EgUWEDB_Tw312tdNjKnoveFZ4RaqKxB_U4qK0_2F80qdu_iGlEBodMBjuLOwJ5zLeTu5d-O2SNV9oPkKw7CDLk?key=gORaE6vjeZ6i7Y4PGyLKfw" alt="" width="563"><figcaption><p>Example of Zoom Phone licensing.</p></figcaption></figure> 

{% content-ref url="licenses-calling-plans-and-add-ons.md" %}
[licenses-calling-plans-and-add-ons.md](licenses-calling-plans-and-add-ons.md)
{% endcontent-ref %}

### Zoom Phone Integrations

Zoom Phone supports various integrations for enhanced functionality and user workflow efficiency. Although the following list is not exhaustive, some of Zoom Phone’s most popular integrations are briefly outlined in the following section.

{% content-ref url="zoom-phone-integrations.md" %}
[zoom-phone-integrations.md](zoom-phone-integrations.md)
{% endcontent-ref %}

### Contact Center Integrations

#### <mark style="color:blue;">Zoom Contact Center</mark>

Zoom Contact Center (ZCC) is an enterprise-grade, omni-channel solution that integrates Zoom's unified communications platform with contact center capabilities. Designed to enhance customer experiences, ZCC can deliver prompt and personalized service across a robust suite of channels, including video, voice (phone), SMS, social media, and web chat, along with Zoom's AI-powered Virtual Agent.

For more information on Zoom Contact Center, refer to [Zoom’s website](https://explore.zoom.us/en/products/contactcenter/) or speak with your Zoom account team.

#### <mark style="color:blue;">Zoom's Workforce Engagement Management Suite</mark>

Zoom's Workforce Engagement Management suite provides additional products and features that further supplement and expand the power of Zoom Contact Center with Zoom Phone.

With **Zoom Workforce Management** , businesses have access to AI-powered tools that can forecast future contact engagement volume, organize and design schedules that align with projected volume across various channels, and predict agent workloads.

With **Zoom Quality Management** , contact center managers have access to various tools and features that monitor and analyze consumer interactions, evaluate agent performance, offer actionable insights, and proactively identify areas for improvement.

For more information on Zoom’s Workforce Engagement Management suite, refer to [Zoom’s website](https://www.zoom.com/en/products/contact-center/features/workforce-engagement-management/) or speak with your Zoom account team.

#### <mark style="color:blue;">Additional Contact Center Integrations</mark>

In addition to Zoom Contact Center, Zoom Phone also supports contact center integrations with Five9, Twilio, Genesys, NICE inContact, and Talkdesk.

### Zoom Phone Survivability

For businesses that use a cloud-based telephony service dependent on internet provider connectivity, maintaining telephony services in the event of an internet service failure or a service impacting event is critical for business continuity and operations. To address these scenarios, Zoom offers the Zoom Phone Local Survivability (ZPLS) module as a Zoom Node workload, which provides telephony resiliency in the event of a service disruption.

During a survivability event where Zoom endpoints cannot reach the Zoom Phone cloud service, supported user devices will register to the ZPLS module, which provides basic telephony services—like internal calling and survivability distribution groups—until full service can be restored. Businesses can further expand this functionality by connecting the ZPLS module with a Session Border Controller (SBC) connected to an underlying carrier (BYOC) to route calls across the public switched telephone network (PSTN).

When integrated with an SBC, businesses have the best of both worlds: the simplicity and ease of a cloud-managed phone system, with the survivability and resiliency of on-premises infrastructure when the unforeseen occurs. In short, with ZPLS, businesses can comfortably deprecate most legacy, on-premises telephony appliances and migrate to a cloud-based phone system with confidence.

Refer to the section of this document dedicated to [Zoom Phone Local Survivability](../zoom-phone-local-survivability.md) for more information.

### Call Routing Logic

Zoom Phone supports many nuanced call routing capabilities, supporting multiple Sites, external contacts, routing rules, and more. To support customer understanding for the impact of call flows, Zoom Phone processes different calling scenarios through comprehensive call routing logic.
<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXe8AcIH76HJyaZbZGgLzZGSoYsioREHMSnT-fZmhYUkttArqrTTItC1QHW2UqdK9Za3Gzn3XpmDO-U3sRIBjpvEuareYjb5FM9VCDufgIFDrP5jompyaKIKkAmBXMsIOCOO7MzxMIck7e-lmzsqXyY?key=gORaE6vjeZ6i7Y4PGyLKfw" alt="" width="563"><figcaption><p>Example of different Zoom Phone call flows.</p></figcaption></figure> 

### Network Configuration

Due to Zoom Phone's cloud-based architecture, configuring Zoom Phone for your network is substantially easier in comparison to legacy, on-premises phone systems. From the simplest of perspectives, users need two key factors to begin successful calling: a working internet connection and open network ports. So long as users can successfully maintain an active connection with Zoom Phone data centers and the necessary ports are not blocked, Zoom Phone is ready for use within your network.

{% content-ref url="network-configuration.md" %}
[network-configuration.md](network-configuration.md)
{% endcontent-ref %}

