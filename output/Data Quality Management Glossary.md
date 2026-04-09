Source tag : https://rndwiki.inc.hpicorp.net/confluence/spaces/DataOS/pages/1739171619/Data+Quality+Management+Glossary

Note : This extracted file is generated from SharePoint or Wiki content. If the source document contains images, charts, or graphical elements, they may not be fully converted into Markdown format. For complete clarity, please refer to the original source using the source tag provided above.

# Data Quality Management Glossary

| Term | Definition |
|------|------------|
| Bronze (DECOMMISSIONED) | Has the same data as bronze++ but it's stored with a different lake storage structure. The s3 bucket that our team typically pulls from in databricks is Bronze. bronze is in S3 |
| Bronze++ | Bronze++ data product consumes data from 4 archive buckets of bronze. is in team_onecloud core_data_products is a schema ETL team built based on bronze++ |
| CDM | Common Data Model Dune ARES Fw Platform devices Functionality Loads data from bonded store. Validates schema, de-duplicates records. Archives data as compressed, partitioned Parquet (hourly). Publishes repartitioned data (daily) and custom data products. |
| CMYK | Cyan Magenta Yellow Black |
| Derivative | updates/changes to a preexisting set product families |
| ETL | "We try to make the data "analytics ready". For LEDM, we do xpath parsing. For CDM, before bronze++ we would join it to privacy and geo and do field extractions. Minimal aggregations, and some clean up, filtering" Josh Yim |
| Low Touch | minor changes to fw (example: add skus to existing family) |
| Mid Touch | minor changes that might include additional features to fw |
| Fleet | is a grouped firmwarer newer version to sirius with schema changes |
| IDST | The IDST (Ink Device State Trend) Data pipeline transforms "standardized raw" data into analysis-ready tables. |
| Ink | Data Deep Dives: Ink, Laser, and CDM - Supplies Big Data - HP R&D Wiki Data Deep Dives 02 - Ink and Laser.pptx Ink and Laser Big Data compare - Supplies Big Data - HP R&D Wiki |
| IPH | Integrated printhead Two consumables, K (black) and CMY (cyan, magenta, yellow). Each is a combination printhead and ink supply. IPH cartridges have EPROMs on the printhead. |
| Job | Job category - CDM - HP R&D Wiki |
| Laser | Data Deep Dives: Ink, Laser, and CDM - Supplies Big Data - HP R&D Wiki Data Deep Dives 02 - Ink and Laser.pptx Ink and Laser Big Data compare - Supplies Big Data - HP R&D Wiki Laser Printer Identifiers - Supplies Big Data - HP R&D Wiki |
| LEDM | Low End Data Model A RESTful interface to the printer's functionality. It allows clients to query and change printer settings, trigger and track jobs, opt for HP web services, etc. A type of data that resides in legacy printer. Located in PSUJ |
| LF | |
| LTC | LifetimeCounterSnapshot Category - CDM - HP R&D Wiki |
| Looker | This is used to collect and showcase data in a graph-like depiction. It can help you see weaknesses in deploys and even identify bugs in specific builds and environments. Is good for high leveled information and visualization It gets its information from OpenSearch |
| NPI | New Product introduction A product that has not been released to prod yet, and is undergoing modifications to it's overall design in the lower environments. |
| Opensearch / Kibana | Data from this tool typically becomes available to databricks within 24-36 hours. Data is only stored for the past 8-9 days in OpenSearch Gets data from S3 bucket Data that has not been checked against the schema, meaning it will not contain eventDetailErrors or filterErrors The fact that a record is not observed in OpenSearch does not mean it was not ingested into DataOS Bronze++ lake. OpenSearch is just a log observation tool, not to be trusted as confirmation of landing in the delta lakes. What probably happened here is that when these events were processed by our onramp service, OpenSearch was unavailable, so we have no logs. The data could still have landed though. The most reliable mechanism to verify data landing is querying the Bronze++ tables, like Tammy did. |
| Pepto | "Pepto is legacy data, before we had the cdm data format" -Tammy Fuchigami |
| PSU | A combination of CDM and LEDM data, you can filter by fields.groupName = 'taz_logs' (CDM) and fields.groupName = 'pepto_k8s_logs' (LEDM) |
| PSUJ | Print and Supplies Usage Journal PSUJ is a common view which combines Stdraw(non-CDM) and PSU (CDM) data into single view. Finding PSUJ DATA Upstream PSUJ - Finding the Source of Data (LEDM/CDM) - Supplies Big Data - HP R&D Wiki |
| Raw | Is bronze for non cdm data |
| RDMA | This originates from HPIT and is NOT telemetry data |
| Redshift | |
| Sage | |
| Schema | This is a set of rules defined by the fw teams and business that ultimately say which values and types of data can be present in specific fields. |
| Silver (DECOMMISSIONED) | Silver Pipeline - Platform Big Data - HP R&D Wiki |
| Sirius | |
| Stdraw | This is the PSU equalent for non-CDM data |
| Stratus | Stratus is an overarching cloud platform, DataValves is a privacy driven requirement to gate data we collect from customer. DataValves has many firmware and cloud services that work together to make the privacy pipeline. The cloud services supporting dataValves feature is part of Stratus umbrella Stratus filters data before TAZ gets it. |
| Supply | Supply Category - CDM - HP R&D Wiki |
| Taz | Taz is a service that receives and processes CDM JSON. Taz gets its data from the Stratus Data Gateway. The data is then sent through AWS Firehose to S3. There are two ways Taz can receive data: HTTPS POSTs Files delivered to s3 buckets Ingests, authenticates, and validates CDM payloads. Reorganizes payloads into post data and event data. Augments data with geo information and metadata. Writes data to bonded store as compressed JSON. |
| Teamcumulus | Data that is further downstream from teamonecloud. This data is down selected, meaning it's been. Contains all of our data products as well as some metrics and development stuff. |
| Teamonecloud | Bronze level data accessed via teams. team_onecloud is just the larger pool of data that we draw our specific products for. For example, we publish a tiny dataproduct called biz_model, the entire purpose of the product is to get (event.eventDetail.claimType) and see if a printer changes its claim type. It reads from the entire onecloud_prod deviceClaim path, but we only care about that claimType field. So we only grab that one field from it. The biz_model data product lives in team_cumulus, but it is only a single field picked out of the giant lake available in team_onecloud |
| UDM | Unified Data Model Old Lf printers Atlas fw devices |
| Unity | Unity Catalog - Pricing promo team - HP R&D Wiki |
| Upstream | Is data missing or not populating in a tool? then check upstream. Use the below list to help you navigate where the issue may lie: Missing in Bronze++ (Looker & Databricks), but is showing up in Opensearch Likely an Ingestion issue Missing in Bronze++ (Looker & Databricks), and is also missing in Opensearch Likely an Stratus or Fw Issue If the data is missing in all three Bronze++, Opensearch, and Stratus Likely a FW issue |