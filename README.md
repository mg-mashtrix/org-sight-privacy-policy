# OrgSight Privacy Policy

## Last updated: April 2026

1. Overview
OrgSight is a Chrome extension designed to help Salesforce administrators and developers inspect and analyze metadata directly within their Salesforce environment.
We are committed to protecting your privacy. OrgSight is designed to operate primarily within your browser and interacts only with your authenticated Salesforce session.

2. Information We Access
OrgSight may access the following information within your browser session:

Salesforce session cookies (e.g., sid)
Salesforce metadata and configuration data (objects, fields, flows, etc.)
The current Salesforce page URL and domain

This access is required solely to enable the extension’s core functionality.

3. How Information Is Used
All accessed information is used strictly for:

Making Salesforce API calls to your own org
Displaying insights and analysis within the extension UI
Enabling features requested by the user

All processing occurs locally within your browser.

4. Data Storage
OrgSight does not:

Store Salesforce session IDs persistently
Store Salesforce data on external servers
Maintain any user database

Any data used by the extension exists only temporarily during active use.

5. Data Sharing and Transmission
OrgSight does not automatically transmit any data externally. All Salesforce API calls go directly to your own org via your active browser session.

The extension contains one optional "Reach out to Mashtrix" link in the Org Audit panel.

If a user chooses to click this link:

The URL includes the user's Salesforce org domain (e.g., yourcompany.my.salesforce.com) as a referral parameter
This allows Mashtrix to identify which Salesforce org the inquiry came from

This link is:

Never triggered automatically
Only activated through explicit user action

No Salesforce metadata, record data, credentials, or personal information is ever sent to Mashtrix or any third party.

6. Cookies and Authentication
OrgSight uses the Chrome Extensions API to read Salesforce session cookies (such as sid) in order to:

Authenticate API requests to your Salesforce org
Enable seamless interaction without requiring manual login

These cookies:
Are accessed locally
Are not stored persistently
Are never transmitted to external servers
7. Third-Party Services

OrgSight does not use:

Analytics tools
Tracking technologies
Advertising networks

The extension operates independently and does not share data with third-party services, except when a user explicitly chooses to navigate to an external link as described above.

8. Security
OrgSight follows modern Chrome extension security practices:

Built using Chrome Manifest V3
No remote code execution
No use of eval or dynamic script loading
Strict Content Security Policy (script-src 'self')
All logic runs within the extension environment

9. User Control
You can:
Disable or uninstall the extension at any time via Chrome settings
Control permissions through Chrome’s extension management interface
10. Changes to This Policy

We may update this Privacy Policy from time to time. Updates will be reflected by the “Last updated” date above.

11. Contact
If you have any questions about this Privacy Policy, you can contact:
OrgSight Team
Email: hello@mashtrixx.com
