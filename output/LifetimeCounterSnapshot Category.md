Source tag : https://rndwiki.inc.hpicorp.net/confluence/spaces/CDM/pages/1180768557/LifetimeCounterSnapshot+Category

Note : This extracted file is generated from SharePoint or Wiki content. If the source document contains images, charts, or graphical elements, they may not be fully converted into Markdown format. For complete clarity, please refer to the original source using the source tag provided above.

# LifetimeCounterSnapshot Category

Summary

LifetimeCounterSnaphot schema has been been evolving in order to support more use cases and printer categories. Additionally, LifetimeCounterSnapshot has been updated to align more closely with the deviceUsage service and the new CDM naming conventions.

CDM Gun Support

Sirius

com.hp.cdm.service.eventing.resource.eventDetail.type.lifetimeCounterSnapshot.platform.sirius (versions 1.0.0, 1.1.0, 1.2.0, 1.3.0)

deployed on early versions of firmware supporting CDM (dual reporting CDM/LEDM)

Fleet

com.hp.cdm.service.eventing.resource.eventDetail.type.lifetimeCounterSnapshot (1.0.0, 1.1.0, 1.2.0)

deployed on SOL firmware (dual reporting CDM/LEDM)

known as "fleet (service)"

com.hp.cdm.domain.telemetry.type.eventDetail.category.lifetimeCounterSnapshot (1.0.0, 1.1.0, ongoing)

deployed with Dune & Ares

compatible with DeviceUsageService

known as "fleet (domain)"

CDM Shared Types Utilized

- Supply Shared Types
- Device Usage Shared Types
- Glossary

Definitions and Metering Strategies

From the Page Counters Implementers Guide

Impression counts are counts on what occurs on one side of a sheet of paper (i.e. the marking agent applied to that side, the print mode setting for that side, etc.)

Sheet counts are counts on what occurs to an entire sheet of paper as it moves through the device (i.e. input source, duplexer, finishing, etc.).

Impression is one side of a page that has ink/toner on it and jammed/cancelled/blank pages should not be counted for it

What to Meter - At Page Picked or Page Delivered

All print metering should occur when the sheet of media is delivered to an output bin. For billing purposes this ensures that customers are only charged for printing and not for jammed pages. Some of our current products are metering when the sheet is picked out of the input tray. The desire is to migrate these products as soon as possible to begin metering when the page is delivered to an output bin.

Schema Versions

Schema Registry Login

| Version | Schema type | CDM Domain Type | Schema File | Description |
|---------|-------------|-----------------|-------------|-------------|
| 1.0.0 | Sirius | service.eventing | | |
| 1.1.0 | Sirius | service.eventing | | |
| 1.2.0 | Sirius | service.eventing | | |
| 1.3.0 | Sirius | service.eventing | | |
| 1.0.0 | Fleet | service.eventing | | 3M fall candidate |
| 1.1.0 | Fleet | service.eventing | | 1.1.0 release |
| 1.0.0 (new domain) | Fleet | domain.telemetry | | 1.0.0 - beta 1 |

Files

Mapping Table from Sirius Version 1.2 to Fleet version 1.0

CDM_lifetimeCounter_event_1.2_to_1.0.xlsx

Data Requirements and additional mapping info

CDMFleetLifetimeCounterInfoV2.xlsx