Source tag : https://rndwiki.inc.hpicorp.net/confluence/spaces/DataOS/pages/1785497360/Isolating+Bugs+Upstream+Downstream

Note : This extracted file is generated from SharePoint or Wiki content. If the source document contains images, charts, or graphical elements, they may not be fully converted into Markdown format. For complete clarity, please refer to the original source using the source tag provided above.

# Isolating Bugs (Upstream / Downstream)

A big part of investigating tickets is trying to identify the root cause and who can help us fix it. Finding the right team can be hard, but hopefully this guide will help.

| Device Configuration (Firmware) | Stratus Ingestion | ETL | DST | Dashboard |
|---|---|---|---|---|
| Description | Data doesn't show up in either Stratus, OpenSearch, or Bronze++ | filterErrors, filterWarnings, privacyError | data is showing up in Stratus but not in OpenSearch | Shows up in OpenSearch but not in Bronze++ |
| Contact to Assign Tickets to | Manager | Contact is specific to product name and event type | ?????? | Ray Hechavarria | Lisa Michels |
| Jira Project Name | This is dependent on the product name the error originates from | DUNE LOWINKFW SRFWBUG ARES | STPI | DATAPLAT |