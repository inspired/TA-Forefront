# Add-on for Microsoft Forefront Threat Management Gateway
## Table of Contents

### OVERVIEW

- About the Add-on for Microsoft Forefront Threat Management Gateway
- Release notes
- Support and resources

### INSTALLATION AND CONFIGURATION

- Hardware and software requirements
- Installation steps
- Deploy to single server instance
- Deploy to distributed deployment
- Deploy to distributed deployment with Search Head Pooling
- Deploy to distributed deployment with Search Head Clustering
- Deploy to Splunk Cloud 
- Configure Add-on for Microsoft Forefront Threat Management Gateway

### USER GUIDE

- Data types
- Lookups

### OVERVIEW

#### About the Add-on for Microsoft Forefront Threat Management Gateway

| Author | Mikael Bjerkeland |
| --- | --- |
| App Version | 2.3.1 |
| Vendor Products | Cisco Catalyst, ASR, ISR, Nexus, CRS and other IOS based switches, Wireless LAN Controller |
| Has index-time operations | True |
| Create an index | False |
| Implements summarization | False |

The Add-on for Microsoft Forefront Threat Management Gateway allows a Splunk® Enterprise administrator to extract and filter event information from Cisco IOS and WLC devices. The app sets the correct sourcetype and adds fields required for CIM compliance, and must be installed in order for the Cisco Networks App to work.

##### Scripts and binaries

No scripts or binaries are included.

#### Release notes

##### About this release

Version 2.3.1 of the Add-on for Microsoft Forefront Threat Management Gateway is compatible with:

| Splunk Enterprise versions | 5.0.x, 6.x |
| --- | --- |
| CIM | 4.3, 4.2, 4.1, 4.0 |
| Platforms | Platform independent |
| Vendor Products | Cisco Catalyst, ASR, ISR, Nexus, CRS and other IOS based switches, Wireless LAN Controller |
| Lookup file changes | Added cisco_ios_icmp_code.csv |

##### New features

Add-on for Microsoft Forefront Threat Management Gateway includes the following new features:

- New CIM tags: insecure logins and privilege escalations

##### Fixed issues

Version 2.3.1 of the Add-on for Microsoft Forefront Threat Management Gateway fixes the following issues:

- IOS XR general field extraction and transform fixed
- Corrected a few typos

##### Known issues

Version 2.3.1 of the Add-on for Microsoft Forefront Threat Management Gateway has the following known issues:

- None known

##### Third-party software attributions

Version 2.3.1 of the Add-on for Microsoft Forefront Threat Management Gateway incorporates the following third-party software or libraries.

- None

##### Support and resources

**The Add-on for Microsoft Forefront Threat Management Gateway for Splunk Enterprise is supported for all users who have a Splunk Support Contract or Cisco Service Contract with Datametrix**

* Hours: Mon-Fri 08:00 - 16:00 Central European Time
* Observed Holidays: All Norwegian Public Holidays, December 23 to January 2, Palm Sunday to Easter Monday.
* Support URL: https://github.com/inspired/TA-cisco_ios/issues

**For users who are not customers of Datametrix, best effort support is available via Splunk Answers**

* Access questions and answers specific to the Add-on for Microsoft Forefront Threat Management Gateway at http://answers.splunk.com/app/questions/1467.html

## INSTALLATION AND CONFIGURATION

### Hardware and software requirements

#### Hardware requirements

Add-on for Microsoft Forefront Threat Management Gateway supports the following server platforms in the versions supported by Splunk Enterprise:

- Windows 7, 8, and 8.1 (64-bit)
- Windows Server 2008, 2008 R2, 2012 and 2012 R2 (64-bit)
- Windows 7, and 8 and 8.1 (32-bit)
- Windows Server 2008 (32-bit)
- 2.6+ kernel Linux distributions (64-bit)
- 2.6+ kernel Linux distributions (32-bit)
- Solaris 10, 11 (64-bit)
- Solaris 10, 11 (SPARC)
- OSX 10.8 (Intel)
- OSX 10.9 (Intel)
- OSX 10.10 (Intel)
- FreeBSD 8, and 9 (64-bit)
- AIX 6.1, 7.1

#### Software requirements

To function properly, Add-on for Microsoft Forefront Threat Management Gateway requires the following software:

- Optional: Cisco Networks App, 2.2.0 or higher (for dashboards etc)

#### Splunk Enterprise system requirements

Because this add-on runs on Splunk Enterprise, all of the [Splunk Enterprise system requirements](http://docs.splunk.com/Documentation/Splunk/latest/Installation/Systemrequirements) apply.

#### Download

Download the Add-on for Microsoft Forefront Threat Management Gateway at https://apps.splunk.com/app/1467/.

#### Installation steps

To install and configure this app on your supported platform, follow these steps:

1. In your Splunk Enterprise web interface, click on App(s) -> Manage Apps
1. Click on Install app from file
1. Select the file you downloaded, Click Upload, optionally selecting Upgrade app if you are upgrading from an earlier version. Restart Splunk if required

##### Deploy to single server instance

Follow these steps to install the app in a single server instance of Splunk Enterprise:

1. In your Splunk Enterprise web interface, click on App(s) -> Manage Apps
1. Click on Install app from file
1. Select the file you downloaded, Click Upload, optionally selecting Upgrade app if you are upgrading from an earlier version. Restart Splunk if required

##### Deploy to distributed deployment

**Install to search head**

1. In your Splunk Enterprise web interface, click on App(s) -> Manage Apps
1. Click on Install app from file
1. Select the file you downloaded, Click Upload, optionally selecting Upgrade app if you are upgrading from an earlier version. Restart Splunk if required

**Install to indexers**

1. In your Splunk Enterprise web interface, click on App(s) -> Manage Apps
1. Click on Install app from file
1. Select the file you downloaded, Click Upload, optionally selecting Upgrade app if you are upgrading from an earlier version. Restart Splunk if required

**Install to forwarders**

This app should not be installed on forwarders.

##### Deploy to distributed deployment with Search Head Pooling
Follow the same steps as *Install to search head*.
##### Deploy to distributed deployment with Search Head Clustering
Follow the same steps as *Install to search head*.
##### Deploy to Splunk Cloud
Unknown
#### Configure Add-on for Microsoft Forefront Threat Management Gateway

1. Install in $SPLUNK_HOME/etc/apps/TA-cisco_ios

1. Create a UDP input on one of your Splunk servers or a forwarder with sourcetype set to *syslog* or *cisco:ios*. A regex match will be performed to rewrite the events to the cisco:ios sourcetype.
2. Configure your Cisco devices to send their syslogs to the UDP input created in step 2 with logging level informational.

1. Step 4 to 6: OPTIONAL for Smart Call Home support

1. OPTIONAL - Add a new TCP data input on a port of your choice, set sourcetype to Cisco:SmartCallHome

1. OPTIONAL - On your Cisco devices:

        service call-home
        call-home
        contact-email-addr YOUR.EMAIL@ADDR.ESS
        site-id "YOUR_SITE_NAME"
        profile "Splunk"
        destination transport-method http
        destination address http http://SPLUNK.SERVER.IP:TCP_PORT_FROM_STEP_4
        subscribe-to-alert-group diagnostic severity debug
        subscribe-to-alert-group environment severity debug
        subscribe-to-alert-group inventory
        subscribe-to-alert-group inventory periodic daily 22:30

4. Restart Splunk

## USER GUIDE

### Data types

This app provides search-time and index time knowledge for the following types of data from Microsoft Forefront Threat Management Gateway:

**Search-time**

- microsoft:forefront:tmg:proxy - Proxy events from w3c files
- microsoft:forefront:tmg:fw - Firewall events from w3c files

These data types support the following Common Information Model data models:

| Source Type | CIM Data Models |
| --- | --- |
| microsoft:forefront:tmg:proxy | Web<br/>|
| microsoft:forefront:tmg:fw | Network Traffic|


### Lookups

The Add-on for Microsoft Forefront Threat Management Gateway contains 1 lookup files.

**microsoft_forefront_tmg_actions.csv**

Maps a vendor action to a CIM compliant action.

- File location: lookups/microsoft_forefront_tmg_actions.csv
- Lookup fields: vendor_action, action
- Lookup contents: See the file contents

