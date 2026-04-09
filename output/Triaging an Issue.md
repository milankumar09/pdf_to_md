Source tag : https://rndwiki.inc.hpicorp.net/confluence/spaces/DataOS/pages/1739460550/Triaging+an+Issue

Note : This extracted file is generated from SharePoint or Wiki content. If the source document contains images, charts, or graphical elements, they may not be fully converted into Markdown format. For complete clarity, please refer to the original source using the source tag provided above.

# Triaging an Issue

Triaging Queries

Issue Triaging Steps: Each step's outcome should be in the comments section of the epic.

Jira Check

Check to see if the issue has already been entered in Jira

Yes?
- Ticket found is a closed bug? Then review the resolution and figure out the next steps
- Ticket found is an opened bug? Close our investigation/epic ticket and notify the reporter that this is being investigated elsewhere

No? proceed with the rest of the steps.

Check for Required Information. In order to start investigating a ticket you will need certain information. If a ticket doesn't have the required information reach out to the creator or reporter for additional information:

- Devices/Product Families
- Environment
- Latest fwVersion associated with the Devices/Product Families you're investigating
- Event Gun
- Field in question that is broken

Check reproducibility

- find the original error on the reported fwVersion (Ex. Issue was reportedly seen on 6.23.0.451-202401221652)
- find all instances of the error for Current and past month on the entire fwVersion line (Ex. Issue needs to be checked against 6.23 fwVersion line). At the very least it should be broken down by two sets of 30 days. That way you can see a trend of the issue. It should be clear if it's steady, improving, or worsening.
- Provide breakdown of issue by product family and fwVersion if epic needs to be entered as a bug.

Check the Parent (only applies to null based errors)

Often times the parent is source of the nulls. We need to know what percentage of the field's nulls are caused by the parent or if they belong to the field in question. If they are all caused by the parent then the issue lies there and not within this field.

Check Event Specific Information (not applicable to Datavalve errors) - All Errors related to Job, LTC, or Suppy should be checked against the Telemetry Behavior Document.

Job

- Do a groupBy of the event.eventDetail.jobInfo.jobCategory column so that you can determine where the majority of the errors are occurring.
- Do a groupBy of the event.eventDetail.jobInfo.state column so that you can determine where the majority of the errors are occurring.

Supply

- Do a groupBy of the event.eventDetail.notificationTrigger column so that you can determine where the majority of the errors are occurring.
- Do a groupBy of the event.eventDetail.supplyType column so that you can determine where the majority of the errors are occurring.
- Do a groupBy of the event.eventDetail.supplyAttributeInfo.consumablePlatform column. This will be used against the telemetry behavior document.

LTC

- Do a groupBy of the event.eventDetail.notificationTrigger column so that you can determine where the majority of the errors are occurring.

Check field/column information

Understanding columns by events, Telemetry Behavior Across Products.xlsx

Schema Registry [firefox browser only]: (Used for helping you determine if an eventDetailError should be thrown based on values received)

Check our profiler rules document

If you're unable to find any column/field info, then I recommend reaching out to a fw contact that might be more familiar with rules associated with device you're investigating.

Provide your triage summary (Close|Bug|Cannot Reproduce|Etc).

If you think it could be a bug or if you aren't sure then we will need to attach avalid payloadof the issue and reach out to the [fwContact|Telemetry Events Ownership] to determine the best next steps.

If you don't think it's a bug then close the epic with the resolution of "Won't Do"

Triage Links:

| Link | Purpose |
|------|--------|
| Old Rainbow Chart Product Number | Allows you to find product family by product number or model number |
| Rainbow Chart for Product # | Allows you to find product family by product number or model number |
| eventDetail Categories - CDM - HP R&D Wiki (hpicorp.net) | Research column info by event category |
| Telemetry Events ownership matrix - CDM - HP R&D Wiki (hpicorp.net) | Find a contact by firmware group. This can be used when you can't find any information about the column or if you need to clone this ticket to a target project and need to find who to assign it to. |
| Telemetry Event List by Product - CDM - HP R&D Wiki (hpicorp.net) | Can't find the data? Make sure your path is correct by checking which event paths you should use by product family |
| Schema Registry | Schema Registry – used for determining expected values types in columns |
| Telemetry Behavior Across Products.xlsx | Used for determining when data should be showing up for specific type of jobs. |
| CDM Generated Data Dictionaries - Supplies Big Data - HP R&D Wiki | Similar to the schema registry but may be more user friendly if you don't know how to navigate the schema registry |