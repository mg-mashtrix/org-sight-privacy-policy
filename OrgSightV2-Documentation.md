# OrgSight for Salesforce

> The all-in-one field intelligence and metadata toolkit for Salesforce admins and developers.
> Alt-click any field. See everything connected to it. Instantly.

[![Chrome Web Store](https://img.shields.io/badge/Chrome%20Web%20Store-Available-brightgreen?logo=googlechrome)](https://chromewebstore.google.com/detail/joellpmaagdomhfmgbaklpngnaoaddgg)
[![Version](https://img.shields.io/badge/Version-2.0-blue)](https://mashtrixx.com/solutions/orgsight)
[![License](https://img.shields.io/badge/License-Free-orange)](https://mashtrixx.com/solutions/orgsight)

---

## Table of Contents

- [Overview](#overview)
- [Installation](#installation)
- [Field Inspector](#field-inspector)
  - [Overview Tab](#overview-tab)
  - [Object Tab](#object-tab)
  - [Permissions Tab](#permissions-tab)
  - [Automation Tab](#automation-tab)
  - [Impact Tab](#impact-tab)
  - [Graph Tab](#graph-tab)
- [All Fields](#all-fields)
- [SOQL Runner](#soql-runner)
- [Flow Health Analyser](#flow-health-analyser)
- [Metadata Explorer](#metadata-explorer)
- [Environment Bar](#environment-bar)
- [Settings](#settings)
- [Keyboard Shortcuts](#keyboard-shortcuts)
- [Error Reference](#error-reference)
- [Privacy](#privacy)

---

## Overview

OrgSight is a free Chrome extension that surfaces deep field-level intelligence, metadata analysis, and org health information directly inside the Salesforce interface.

Instead of running manual SOQL queries or navigating across multiple Setup tabs to understand how a field is used, OrgSight aggregates all of that information into a single panel that opens alongside the record you are working on.

**Supported domains**

| Domain | Supported |
|---|---|
| Production `*.my.salesforce.com` | Yes |
| Sandbox `*.sandbox.my.salesforce.com` | Yes |
| Lightning `*.lightning.force.com` | Yes |
| Setup `*.salesforce-setup.com` | Yes |
| Scratch orgs | Yes |
| Experience Cloud `*.site.com` | Yes |
| Trailhead, AppExchange, login pages | No |

---

## Installation

1. Open the [Chrome Web Store listing](https://chromewebstore.google.com/detail/joellpmaagdomhfmgbaklpngnaoaddgg)
2. Click **Add to Chrome**
3. Navigate to any Salesforce record page
4. Hold `Alt` and click any field label to open the Field Inspector

> **Extension ID:** `joellpmaagdomhfmgbaklpngnaoaddgg`

---

## Field Inspector

The Field Inspector is the core feature of OrgSight. It opens as a side panel on any Salesforce record page when you `Alt + Click` a field label.

**Opening the Inspector**

| Method | How |
|---|---|
| From a record page | Hold `Alt` and click any field label |
| From the All Fields page | Hold `Alt` and click any row in the field list |
| From the Explorer sidebar | Click the panel icon and search for a field |

**Panel Controls**

| Button | Action |
|---|---|
| `↓` teal | Export field dependencies as CSV or JSON |
| `↺` | Refresh — clears cache and re-fetches all data |
| `Light / Dark` | Toggle theme |
| `⚙` | Open Settings |
| `✕` | Close panel |

---

### Overview Tab

The first screen shown when the inspector opens. Gives a complete picture of one field at a glance.

**Field Details**

| Field | Description |
|---|---|
| Label | Display label shown to users |
| API Name | Developer API name used in Apex, SOQL, and flows |
| Object | Parent object with a copy button |
| Type | Field data type from the Salesforce describe API |
| Custom | Whether the field is custom or standard |
| Source | Where the field originates. `FieldDefinition` means created in your org |

> **Managed package fields** — When a field belongs to a managed package some metadata sections show limited information because Salesforce seals managed package source code.

**Stat Cards**

| Card | What it shows |
|---|---|
| FLS Entries | Total `FieldPermissions` records across all profiles and permission sets |
| Can Edit | Of all FLS entries, how many grant write access |
| Triggers | Active Apex triggers on the parent object (object-level count) |
| Flows | Active flows on the parent object (object-level count) |
| Populated | Percentage of records with a non-null value in this field |

> **Note on population query** — OrgSight uses `WHERE Field != null` instead of `COUNT(Field)` because `COUNT(Field)` fails for Long Text Area, Rich Text Area, and Multi-select Picklist field types.

**Population colour coding**

| Colour | Range |
|---|---|
| Green | 70% and above |
| Amber | 30% to 69% |
| Red | Below 30% |

**Field Usage Score**

A score from **0 to 100** estimating how actively the field is used. Based on seven signals.

| Signal | Description |
|---|---|
| Flows | Active flows reference this field in structured metadata. Up to 30 pts |
| Apex references | Trigger or class bodies contain the field API name |
| LWC and Aura | Lightning component source files reference the field |
| Population rate | 70% or above adds 20 pts. 30–69% adds 8 pts |
| Page layouts | Field appears on at least one page layout |
| Validation rules | Field appears in a validation rule formula |
| Description | Field has a description filled in |

**Verdict labels**

| Score | Verdict |
|---|---|
| 70 and above | Active |
| 50 to 69 | Likely Active |
| 25 to 49 | Low Usage |
| Below 25 | Likely Dead |

**Picklist Value Distribution**

For picklist fields a bar chart shows the distribution of values across all records. Requires the **Picklist Usage** feature to be enabled in Settings.

---

### Object Tab

Shows metadata about the parent object rather than the individual field.

**Object Information**

| Field | Description |
|---|---|
| Label and plural label | Display names used in the Salesforce interface |
| API name | Developer name used in code and configuration |
| Object ID | 18-character ID of the object entity definition |
| Key prefix | 3-character prefix used in record IDs. For example `001` for Account |
| Internal sharing | Organisation-wide default for internal user sharing |
| External sharing | Organisation-wide default for external portal sharing |

**Object Permissions**

Lists which profiles and permission sets have CRUD and View All / Modify All access on the parent object. The `↗` arrow next to each row opens that entity directly in Salesforce Setup.

---

### Permissions Tab

Shows field-level security for the inspected field across every profile and permission set in the org.

**Access Badges**

| Badge | Meaning |
|---|---|
| `R` teal | Entity has read access |
| `W` green | Entity has write access |
| Greyed-out | Access not granted |
| `↗` | Opens that profile or permission set in Setup |

**Setup Link Destinations**

| Type | Opens |
|---|---|
| Profile | Enhanced Profile page using the profile ID |
| Permission Set | Permission Set detail page |
| Permission Set Group | Permission Set Group detail page |

**Permission Gap Finder**

Flags profiles and permission sets that have object-level access to the parent object but have no field-level access configured for this specific field.

---

### Automation Tab

Scans all automation components on the parent object and identifies which ones reference the inspected field.

**Match Types**

| Match Type | Confidence | Description |
|---|---|---|
| Exact match | Highest | Field API name appears verbatim in source or metadata |
| Object.Field match | Highest | Full `Object.FieldName` format found — fully qualified reference |
| Schema token match | Highest | `@salesforce/schema/Object.Field` static import found in LWC |
| Field API string match | Medium | Field API name appears as a string literal in source code |
| Name match | Medium | Match on a related name rather than the API name |
| Dynamic reference | Medium | `record.get()`, `record.put()`, or dynamic SOQL pattern found |

**LWC Source References**

Each LWC card shows additional badges beyond the match type.

| Badge | Colour | Meaning |
|---|---|---|
| JS Controller | Amber | Match found in the component `.js` file |
| HTML Template | Red | Match found in the component `.html` template |
| @salesforce/schema import | Teal | Static schema import — explicit compile-time dependency |
| Dynamic ref | Grey | String literal or dynamic access pattern |
| File name | Grey | Exact file within the bundle where the match was found |

**Flow Process Types**

| Process Type | Triggered by |
|---|---|
| Record-Triggered | Record create, update, or delete |
| Screen Flow | User clicking a button or navigating to a flow screen |
| Scheduled | Time-based schedule against a batch of records |
| Auto-Launched | Apex code, process builders, or REST API calls |
| Platform Event | Platform event message published |

**Custom Dependencies**

| Section | What it scans |
|---|---|
| Custom Labels | MetadataComponentDependency API and Apex source for custom label references |
| Custom Settings | Apex source for `getInstance` and `getValues` patterns |
| Custom Metadata Types | References to `__mdt` type records in automation |

---

### Impact Tab

Shows where the field surfaces in the Salesforce UI and performs a delete risk analysis.

**Delete Risk Score**

| Verdict | Meaning |
|---|---|
| LOW | Few or no known dependencies |
| MEDIUM | Some dependencies found — review before deleting |
| HIGH | Significant dependencies — deletion will break things |
| CRITICAL | Extensive dependencies — do not delete without a full audit |

**Safe Deletion Checklist**

A list of 11 items to verify before deleting a field. Items are automatically checked based on what OrgSight found. A progress bar tracks completion. Reaching 100% means all safety conditions are satisfied.

> Unchecking a pre-checked item requires confirmation to prevent accidental data loss.

---

### Graph Tab

Visualises all field dependencies as a node diagram.

**Node Colours**

| Colour | Type |
|---|---|
| Teal | The inspected field (centre) |
| Red | Apex Triggers |
| Blue | Apex Classes |
| Green | LWC Components |
| Light green | Aura Components |
| Purple | Flows |
| Amber | Validation Rules |
| Orange | Page Layouts |
| Grey | Profiles and Permission Sets |

**Interactions**

- Hover over any node to see the full name in a tooltip
- Click any node to open the corresponding Salesforce Setup page in a new tab

**Full Graph Page**

When dependencies exceed the inline view an **Open full graph** button appears. The full-page graph adds:

| Control | Description |
|---|---|
| Type filters | Toggle buttons to show or hide each dependency type |
| Radial view | Circular layout — auto-scales node size and radius based on count |
| Grid view | Card-based list layout — easier to read for 50 or more nodes |

---

## All Fields

Shows every field on the current object in a searchable filterable table with optional inline editing.

**Filter Bar**

| Filter | Shows |
|---|---|
| All / Custom / Standard | Filter by field origin |
| Editable | Fields the current user can edit based on FLS |
| Required | Required fields only |
| Picklist | Picklist and multi-select picklist fields |
| Lookup | Lookup and master-detail relationship fields |
| Has Value | Fields with a non-null value on the loaded record |
| Search box | Filter by API name, label, or type |

**Inline Edit Input Types**

| Field type | Input |
|---|---|
| Date | Native date picker — opens on click anywhere in the field |
| DateTime | Native date and time picker |
| Picklist | Dropdown of available values |
| Checkbox | Toggle checkbox |
| Long Text Area / Rich Text | Multi-line textarea — minimum 72px, expands as you type |
| Text | Standard text input with field length limit enforced |

**Alt-Click to Inspect**

Hold `Alt` and click any row to open the full six-tab Field Inspector panel on the right side of the All Fields page. Close with `✕` or `Escape`.

**Actions**

| Button | Action |
|---|---|
| Export | Downloads the visible field list as CSV |
| Clone | Creates a copy of the current record |
| Delete | Deletes the current record after confirmation |
| Metadata | Opens an overlay showing object describe metadata |

---

## SOQL Runner

A full SOQL and Tooling API query editor with up to 15 independent tabs.

**API Types**

| Mode | Use for |
|---|---|
| REST API | Standard and custom objects |
| Tooling API | Metadata objects such as ApexClass, Flow, FieldPermissions |

**Keyboard Shortcut**

Run query: `Ctrl + Enter` or `Cmd + Enter`

**Function Toolbar**

| Button | Inserts |
|---|---|
| `FIELDS(ALL)` | Selects all fields |
| `FIELDS(CUSTOM)` | Selects custom fields only |
| `FIELDS(STANDARD)` | Selects standard fields only |
| `COUNT()` `SUM()` `AVG()` `MIN()` `MAX()` | Aggregate functions |
| `TODAY` `LAST_N_DAYS:30` `LAST_N_MONTHS:3` | Date literals |
| `= NULL` `!= NULL` | Null filters |

**ID Context Menu**

Clicking any Salesforce ID in the results opens a context menu.

| Option | Action |
|---|---|
| Show all data | Fetches the full record and opens it in All Fields in a new tab |
| Query Record | Opens a new tab pre-filled with `SELECT FIELDS(ALL) FROM Object WHERE Id = '...' LIMIT 1` |
| View in Salesforce | Opens the record standard page in a new tab |
| Copy Id | Copies the ID to clipboard with a confirmation toast |

> The object type is identified automatically from the record ID. You do not need to know which object it belongs to before clicking.

**Copy and Export**

| Button | Output |
|---|---|
| Copy CSV | Comma-separated values to clipboard |
| Copy JSON | JSON array to clipboard |
| Copy Excel | Tab-separated format for pasting into Excel |
| Download | File download |

---

## Flow Health Analyser

Scans all active flows for patterns that commonly cause governor limit errors and production incidents.

**Issues Detected**

| Issue | Severity | Description |
|---|---|---|
| SOQL in loop | Critical | SOQL query inside a loop element — hits the 100-query governor limit |
| DML in loop | Critical | Record operation inside a loop — hits the 150 DML limit |
| Subflow in loop | Warning | Subflow inside a loop multiplies SOQL and DML usage |
| Apex action in loop | Warning | Invocable Apex inside a loop consumes limits internally |
| No fault path on DML | Warning | DML element with no error handling path |
| Multiple Get Records on same object | Warning | Same object queried more than once when a single query could cover both |
| Unfiltered scheduled flow | Warning | Get Records with no filter — queries all records on every scheduled run |
| Old API version | Warning | Flow saved on API version 49 or earlier |

**Severity Levels**

| Colour | Level | Meaning |
|---|---|---|
| Red | Critical | Likely to cause governor limit errors at production scale |
| Amber | Warning | Poor practice or future risk |
| Green | Healthy | No issues detected |

**Caching**

OrgSight caches flow health results after the first scan. On repeat opens it checks the most recent `LastModifiedDate` across all flows. If nothing changed the cached results load instantly. If any flow was modified a fresh scan runs automatically.

---

## Metadata Explorer

A full org metadata browser, package.xml generator, and retrieval tool.

**Metadata Groups**

| Group | Examples |
|---|---|
| Apex and Visualforce | ApexClass, ApexTrigger, ApexPage, ApexComponent |
| Lightning | LightningComponentBundle, AuraDefinitionBundle |
| Flows and Automation | Flow, WorkflowRule, AssignmentRule, ApprovalProcess |
| Objects and Fields | CustomObject, CustomField, RecordType, ValidationRule |
| Layouts and Pages | Layout, FlexiPage, QuickAction |
| Security and Access | Profile, PermissionSet, PermissionSetGroup |
| Analytics | Report, Dashboard |

**Selecting Components**

| Action | How |
|---|---|
| Select whole type | Check the checkbox next to the type name — uses wildcard |
| Select individual components | Expand the type then check individual component checkboxes |
| Exclude managed packages | Check the **Excl. managed** checkbox |
| Search | Type in the search box — filters both type and component names |

**Package XML**

| Control | Description |
|---|---|
| API version | Dropdown of supported API versions from your org |
| Wildcards toggle | On uses `*` for members where supported. Off uses explicit names only |
| Copy XML | Copies package.xml to clipboard |
| Download package.xml | Downloads the file |

**Retrieval**

| Mode | Description |
|---|---|
| Wildcard | Retrieves all components of each type using `*` where the API supports it |
| Selective | Retrieves only specifically selected components by name |

> **Large org handling** — Salesforce has a hard limit of 10,000 components per retrieve call. OrgSight automatically detects when this would be exceeded and splits the retrieval into chunks downloading as separate ZIP files named `metadata_part1of3.zip` and so on.

---

## Environment Bar

Adds a colour-coded identification bar to every Salesforce page so you always know which org you are working in.

**Configuration per org**

| Setting | Description |
|---|---|
| Text | Custom text such as `PRODUCTION` or `Developer Sandbox` |
| Background colour | Bar background. Red for production and green for sandbox is common |
| Text colour | Text colour in the bar |
| Position | Top or bottom of the browser window |

Configuration is stored per org identified by the org slug in the URL. The bar automatically re-inserts itself if the Salesforce framework removes it during navigation.

---

## Settings

Open Settings from the `⚙` icon in the panel header or explorer sidebar.

**Feature Toggles**

| Feature | What it controls |
|---|---|
| Field Explorer | The floating panel and Alt-click functionality |
| All Fields page | The full field list page |
| Org Audit | Object-level audit and field health summary |
| Flow Health Analyser | The flow scanning page |
| Metadata Explorer | The metadata browser and retrieval tool |
| Dead Field Detector | Usage score and scoring signals in the Overview tab |
| Picklist Value Distribution | Value distribution chart for picklist fields |

---

## Keyboard Shortcuts

| Action | Shortcut |
|---|---|
| Open Field Inspector | `Alt + Click` on any field label |
| Open Inspector from All Fields | `Alt + Click` on any row |
| Close Field Inspector | `Escape` or `✕` |
| Run SOQL query | `Ctrl + Enter` or `Cmd + Enter` |
| Undo in SOQL editor | `Ctrl + Z` or `Cmd + Z` |
| Redo in SOQL editor | `Ctrl + Y` or `Cmd + Y` |
| Close Alt-click panel | `Escape` |

---

## Error Reference

| Error | Cause | Fix |
|---|---|---|
| URL not in allowed Salesforce domains | API call blocked — domain not in allowed list | Refresh the page |
| Extension context invalidated | Extension updated or reloaded while panel was open | Refresh the Salesforce page |
| Field not found in Tooling API | Field exists in describe API but not in Tooling API metadata objects | Expected for some managed package fields — partial information still shown |
| Managed package: extended metadata not accessible | Field belongs to a managed package — source code sealed by Salesforce | FLS, usage counts, and dependency data still available |
| LIMIT undefined | Missing internal configuration value | Close and reopen the panel |
| G._getRecordIdFromPage is not a function | Inspector opened from All Fields rather than a live record page | Expected — sections requiring a record ID show this. All other tabs load normally |

---

## Privacy

OrgSight does not send any data to external servers.

- All API calls go directly from your browser to your own Salesforce org
- Your Salesforce session token is read from the browser cookie store, held in memory only, and never stored or transmitted elsewhere
- Field notes, settings, and caches are stored locally in Chrome extension storage on your device only
- OrgSight has no backend server, no analytics integration, and no data pipeline

Full privacy policy: [https://mg-mashtrix.github.io/org-sight-privacy-policy](https://mg-mashtrix.github.io/org-sight-privacy-policy)

---

## Support

- **Website:** [mashtrixx.com/solutions/orgsight](https://mashtrixx.com/solutions/orgsight)
- **Chrome Web Store:** [Install OrgSight](https://chromewebstore.google.com/detail/joellpmaagdomhfmgbaklpngnaoaddgg)
- **Issues and feedback:** Open an issue on this repository

---

*Built by [Mashtrix](https://mashtrixx.com)*
