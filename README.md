# OrgSight Privacy Policy

**Last updated: May 2026**

1. **Overview**
   OrgSight is a Chrome extension designed to help Salesforce administrators and developers inspect and analyze metadata, field dependencies, automation health, and org configuration directly within their Salesforce environment. We are committed to protecting your privacy. OrgSight is designed to operate entirely within your browser and interacts only with your authenticated Salesforce session.

2. **Information We Access**
   OrgSight may access the following information within your browser session:

   - Salesforce session cookies (e.g., sid)
   - Salesforce metadata and configuration data (objects, fields, flows, Apex classes, profiles, permission sets, validation rules, page layouts, etc.)
   - The current Salesforce page URL and domain
   - Record data on the current page when you use the Field Inspector or All Fields features

   This access is required solely to enable the extension's core functionality.

3. **How Information Is Used**
   All accessed information is used strictly for:

   - Making Salesforce API calls to your own org
   - Displaying field intelligence, dependency analysis, and metadata insights within the extension UI
   - Enabling features requested by the user (SOQL Runner, Flow Health Analyser, Metadata Explorer, All Fields, Field Inspector)

   All processing occurs locally within your browser. No data is ever sent to Mashtrix or any external server.

4. **Data Storage**
   OrgSight does not:

   - Store Salesforce session IDs persistently
   - Store Salesforce record data or metadata on external servers
   - Maintain any user database

   OrgSight stores the following data locally in Chrome extension storage on your device only:

   - Extension settings and feature toggles
   - Environment bar configuration per org
   - Field notes you write
   - SOQL query history and saved queries
   - Metadata member caches (maximum 1 hour TTL)

   Any data used by the extension exists only locally on your device and is never transmitted externally.

5. **Data Sharing and Transmission**
   OrgSight does not automatically transmit any data externally. All Salesforce API calls go directly to your own org via your active browser session.

   If a user chooses to click the "Buy Me a Chai" link in the extension panel:

   - The link opens an external Stripe payment page in a new tab
   - No Salesforce data, metadata, credentials, or personal information is included in or transmitted with that link

   This link is:

   - Never triggered automatically
   - Only activated through explicit user action

   No Salesforce metadata, record data, credentials, or personal information is ever sent to Mashtrix or any third party.

6. **Cookies and Authentication**
   OrgSight uses the Chrome Extensions API to read Salesforce session cookies (such as sid) in order to:

   - Authenticate API requests to your Salesforce org
   - Enable seamless interaction with Salesforce without requiring manual login

   These cookies:

   - Are accessed locally
   - Are not stored persistently
   - Are never transmitted to external servers

7. **File Downloads**
   OrgSight uses the Chrome downloads API to save files to your device when you explicitly request an export. This includes metadata ZIP files from the Metadata Explorer and CSV or JSON exports from the SOQL Runner. Downloads are initiated only by direct user action and the files are saved to your local device only.

8. **Third-Party Services**
   OrgSight does not use:

   - Analytics tools
   - Tracking technologies
   - Advertising networks

   The extension operates independently and does not share data with any third-party service. The only optional external navigation is the Stripe chai link described in Section 5, which is triggered only by explicit user action.

9. **Security**
   OrgSight follows modern Chrome extension security practices:

   - Built using Chrome Manifest V3
   - No remote code execution
   - No use of eval or dynamic script loading
   - Strict Content Security Policy (script-src 'self')
   - All logic runs within the extension environment
   - All API calls are made only to the user's own Salesforce org domains

10. **User Control**
    You can:

    - Disable or uninstall the extension at any time via Chrome settings
    - Control permissions through Chrome's extension management interface
    - Clear locally stored data by removing the extension

11. **Changes to This Policy**
    We may update this Privacy Policy from time to time. Updates will be reflected by the "Last updated" date above.

12. **Contact**
If you have any questions about this Privacy Policy, you can contact:
OrgSight Team
Email: [hello@mashtrixx.com](mailto:hello@mashtrixx.com)
