Source tag : https://rndwiki.inc.hpicorp.net/confluence/spaces/BAT/pages/1668101238/%F0%9F%93%83Bug

Note : This extracted file is generated from SharePoint or Wiki content. If the source document contains images, charts, or graphical elements, they may not be fully converted into Markdown format. For complete clarity, please refer to the original source using the source tag provided above.

# Bug Tracking & Issue Management Overview

Have a request or feedback to share? We'd love to hear from you. Use the Contact Us button, located to the left or the link below, to submit a request or provide feedback to help us improve and evolve ADAPT 2.0 Whether it's a suggestion, a gap you noticed, or a request for support, your input helps us build better, together.

Bug Video

Overview

A brief introduction to guide you through this space, what it is, how to use it, and what to expect.

Related Pages

- Program
- Initiative
- Epic
- User Story
- Spikes
- Sub Tasks
- Risk
- Chore

Bug

Bug refers to an error or flaw in the software that causes it to behave unexpectedly or produce incorrect results, also prevents the functions of a product

- A deviation from expected behavior.
- An issue found during development, testing, or even after release.
- Often logged in tools like Jira for tracking and resolution.

Statuses and Descriptions

| Status | Description |
| --- | --- |
| Open | New Bug Ticket created |
| Triaged | Indicate whether an issue has been reviewed, assessed, and prioritized for further action or resolution. |
| Ready for Development | Prioritized Bug items to be actioned during the upcoming sprint |
| In Development | Bug fix in progress |
| Resolved | Internal QA Testing is done |
| Ready for QA | Ready for System QA |
| In QA | System QA Testing |
| Ready for Demo | Ready for PO to review and signoff |
| Reopened | Bug previously resolved or closed has been reopened for further investigation or action. |
| Closed | The issue is resolved, verified, and requires no further action |
| Deferred | Fix scheduled for later version |
| Blocked | Work on the issue is paused due to pending dependencies or unresolved issues |
| Canceled | The issue is no longer relevant or needed and will not be pursued further. |

Field Configuration

| Filed | Type | Mandatory | Description |
| --- | --- | --- | --- |
| Summary | System field | Yes | High-level summary of the Bug |
| Issue Type | System field | Yes | New Bug is open |
| Reporter | System field | Yes | Name of the person who opened the ticket |
| Category | Select List (single choice) | No | Name of the person who opened the ticket |
| Component/s | System field | No | Categorizes issues into specific project sections for better tracking |
| Epic Link | Epic Link Relationship | No | Associates the bug with a larger Epic to track its relevance to a broader goal |
| Scrum Team | Select List (single choice) | No | Identifies the team responsible for addressing and resolving the bug |
| Story Points | Number Field | No | Overall work effort estimation |
| Sprint | Jira Sprint Field | No | Helps track the sprint the Bug is assigned |
| Severity | Select List (single choice) | No | Indicates the impact level of the bug on system functionality or user experience. |
| Reproducibility | Select List (single choice) | No | Specifies how consistently the bug can be reproduced |
| Stack Environment1 | Select List (multiple choices) | No | Specifies the technical stack or environment where the bug was encountered |
| Fix SW Versions | Select List (multiple choices) | No | Specifies the software version(s) in which the bug is planned to be or has been fixed. |
| Description | System field | No | Summarizes the issue, highlighting the problem and steps to reproduce it. |
| Deployment Notes (str) | Text Field (multi-line) | No | Provides essential instructions or considerations for deploying the fix or update |
| Fix Version/s | System field | No | Indicates the software version(s) in which the issue is or will be resolved. |
| Priority | System field | No | Reflects the urgency of addressing the issue based on its business or project impact |
| Labels | System field | No | User-defined tags used to group, filter, and search for related issues |
| Security Level | System field | No | Defines who can view this bug based on the assigned issue security level |
| Environment | System field | No | Specifies where the bug was observed. |
| Attachment | System field | No | Add files like screenshots or logs to help explain the bug |
| Affects Version/s | System field | No | Indicates the product version where the bug or issue was found |
| Linked Issues | System field | No | Shows how this bug is connected to other issues, like blocking or being caused by them |
| Assignee | System field | No | The individual accountable for investigating and resolving this bug |
| Root Cause | Select List (single choice) | No | Underlying reason for the issue |
| Feature Group | Select List (multiple choices) | No | Identifies the functional area or module of the product that the bug impacts |
| Additional Owners | User Picker (multiple users) | No | Other individuals responsible for or supporting bug resolution |
| Additional Watchers | User Picker (multiple users) | No | People who will get updates about this bug |
| Applicable Products | Select List (multiple choices) | No | Lists the products that are affected by this bug |
| Blocked Reason | Select List (single choice) | No | Describes the specific cause preventing progress on this bug |
| Bug Resolution | Select List (single choice) | No | Specifies how the bug was addressed or why it was closed |
| Found in Build | Text Field (single line) | No | Specifies the build version in which the bug was initially identified |
| Found in FW Version | Text Field (single line) | No | Firmware version where the bug was detected |
| Found in SW Version | Text Field (single line) | No | Indicates the software version where the bug was first observed |
| Found in HW Version | Text Field (single line) | No | Hardware version where the bug was detected |
| Team Watch List | Select List (multiple choices) | No | Teams monitoring or impacted by the bug |
| Fixed in Build | Text Field (single line) | No | Indicates the build version in which the bug was resolved and verified as fixed |
| Encountered By | Select List (single choice) | No | Identifies the user or team member who first observed and reported the bug |
| OS. | Select List (multiple choices) | No | Specifies the operating system on which the bug was encountered |
| Heuristic | Select List (single choice) | No | Detection method based on pattern recognition or rule-based logic |
| SIV Escape From | Select List (multiple choices) | No | Environment from which the issue escaped undetected into production |
| How Found | Select List (single choice) | No | Explains how the bug was discovered |
| Resolution Note | Text Field (multi-line) | No | Summarizes how the issue was resolved |
| IM: Dependencies | Issue Matrix for Jira | No | Related items impacting this issue |
| IM: Sub-Tasks | Issue Matrix for Jira | No | Captures the individual work items required to complete this issue |
| Current Status | Text Field (single line) | No | Reflects the bug's present state in the resolution process |
| Target end | Target end | No | Planned date to complete bug resolution |
| Target start | Target start | No | Planned date to begin bug resolution |
| Pie Date | Date Time Picker | No | The date when the bug was released to the PIE environment |
| Stage Date | Date Time Picker | No | The date when the bug was released to the Stage environment |
| Prod Date | Date Picker | No | The date when the bug was released to the Production environment |
| Attempts Failed | Number Field | No | Logs unsuccessful fixes or troubleshooting steps |
| Attempts Tried | Number Field | No | Records prior efforts made to resolve the bug |
| Cost Impact | Select List (single choice) | No | Reflects the financial significance of the work |
| Issue Category | Select List (cascading) | No | Classifies the work item based on its nature or business impact |
| Rank Requested | Text Field (single line) | No | Defines Priority |
| Feature Flag key | Text Field (single line) | No | Stores the identifier used to toggle this feature via a feature flag system |
| Feature Flag - dev | Text Field (single line) | No | Indicates the development feature flag used to enable or disable this functionality |
| Feature Flag - pie/itg | Text Field (single line) | No | Identifies the feature flag used in PIE/ITG environments to control feature rollout |
| Feature Flag - stage | Text Field (single line) | No | Specifies the feature flag used to control rollout in the staging environment |
| Feature Flag - prod | Text Field (single line) | No | Specifies the feature flag used to manage rollout in the production environment. |
| Feature Flag details | Text Field (multi-line) | No | Provides additional context or configuration notes related to the feature flag implementation |

Have a request or feedback to share?

We'd love to hear from you. Use the link below to submit a request or provide feedback to help us improve and evolve ADAPT 2.0. Whether it's a suggestion, a gap you noticed, or a request for support — your input helps us build better, together.