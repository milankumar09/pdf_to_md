Source tag : https://rndwiki.inc.hpicorp.net/confluence/spaces/DataOS/pages/1739458440/Telemetry+Guide

Note : This extracted file is generated from SharePoint or Wiki content. If the source document contains images, charts, or graphical elements, they may not be fully converted into Markdown format. For complete clarity, please refer to the original source using the source tag provided above.

# Telemetry Guide

Overview: At HP there are various types of printers that create data, also known as telemetry.

Environments:

Data can span across multiple environments from Dev, Pie, Stage, Itg, Prod, etc.. The environments the data can exist in depends on where the data is present. Review the table upstream order (environments) for a deeper understanding. Our team ONLY works in stage/itg and prod. We avoid working with data in Dev and Pie as it's untrustworthy due to constant changes by developers.

Data:

Generally, a printer performs an action that triggers an event. This event contains data/telemetry. The data/telemetry is sent to STRATUS for privacy and consent purposes. Data enters INGESTION for storage, then sent to ETL for processing. ETL tries to make the data "analytics ready." Accessing the data is done via an array of tools using Databricks, Opensearch, or Looker. Jumping into the data can be complicated and overwhelming, but I encourage you to review the diagrams on the architecture to truly understand how the data flows.

Basic Data flow:

FW > STRATUS > INGESTION (Opensearch) > Bronze++ (Looker & Databricks)

Upstream/Downstream:

These are terms used regularly at HP and are used to help isolate where an issue is coming from. Is data missing or not populating in a tool? then check upstream. Use the below list to help you navigate where the issue may lie:

Missing in Bronze++ (Looker & Databricks), but is showing up in Opensearch
Likely an Ingestion issue

Missing in Bronze++ (Looker & Databricks), and is also missing in Opensearch
Likely an Stratus or Fw Issue

If the data is missing in all three Bronze++, Opensearch, and Stratus
Likely a FW issue

Additional Terminology can be found on our Glossary page