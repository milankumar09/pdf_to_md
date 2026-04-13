Source tag : https://rndwiki.inc.hpicorp.net/confluence/spaces/CDM/pages/1170247087/Supply+Category

Note : This extracted file is generated from SharePoint or Wiki content. If the source document contains images, charts, or graphical elements, they may not be fully converted into Markdown format. For complete clarity, please refer to the original source using the source tag provided above.

# Supply Category

Contains information for

- Fleet Supply Event
- Documents
- Data requirement documentation
- Sirius to Fleet mapping
- Sirius Supply Event

# Table of Contents

- Documents
- Data Requirement Document
- Sirius to Fleet mapping- CDM_supply_event_1.3_to_1.0
- Telemetry_ImplementedCDMFields_Document.xlsx
- Fleet Common Supply eventDetailType (com.hp.cdm.service.eventing.resource.eventDetail.type.supply.version.1)
- Schema Image
- Documents
- Schema Detailed Info
  - Supply Schema Structure
  - Definitions
    - iphFabDataTIJ2XData
    - iphFabDataTIJ4Data
    - iphFabDataTIJ5Data
  - Identity Info Properties
  - supplyUniqueId specification
  - Manufacturing Info Properties
  - State Info Properties
  - inkCartridgeInfo Properties
  - tonerCartridgeInfo Properties
  - inkTankInfo Properties
  - printHeadInfo Properties
  - vaReman Properties
  - eLabelSignatureTemplate
  - supplyAttribute Info Properties
  - lifeInfo Properties
  - deviceInfo
  - serviceInfo
  - previousSupplyInfo
- Notification Triggers
- Fleet Common Supply JSON Schema
  - Schema Versions
  - Implementation Notes
    - Example Supply Event Notification Sequence (without supplyRemoval support)
    - Example Supply Event Notification Sequence (with supplyRemoval support)
    - Example Supply Event with supplyState: "unknown"

# Documents

- Data Requirement Document
- Sirius to Fleet mapping- CDM_supply_event_1.3_to_1.0
- Telemetry_ImplementedCDMFields_Document.xlsx

The wiki provides details on the fields required in the schema. Because this schema is shared between many supplies, the data required for each supply type varies.

The Data Requirement Document provides details on data requirements.

# Fleet Common Supply eventDetailType (com.hp.cdm.service.eventing.resource.eventDetail.type.supply.version.1)

## Schema Image

Latest Version (1.5.0-alpha.2)

The schema contains the following properties:

- defaultsupplyUnit
- counterInit
- deviceInfo
- identityInfo
- inkCartridgeInfo
- inkTankInfo
- lifeInfo
- manufacturingInfo
- notificationTrigger
- previousSupplyInfo
- printHeadInfo
- serviceInfo
- stateInfo
- supplyAttributeInfo

## Documents

- Data requirement documentation - CDMFleetSupplyInfo.xlsx
- Sirius to Fleet mapping- CDM_supply_event_1.3_to_1.0

The wiki provides details on the fields required in the schema. Because this schema is shared between many supplies, the data required for each supply type varies.

The Data Requirement Document provides details on data requirements.

## Schema Detailed Info

### Supply Schema Structure

Review CDMFleetSupplyInfo.xlsx for data requirements

| Property (new in) Version | Schema Required | Description | Schema dependency | OCV Required | Sirius 1.3 Compare | Dune PEI |
|---|---|---|---|---|---|---|
| version | 1.0.0 | yes | Generic CDM versioning scheme | | Y | Same | N/A |
| notificationTrigger | 1.0.0 | yes | Indicates what triggered the event from the device. A new supply was detected, state/data change for a current supply, time interval trigger. See the Notification Triggers section below for trigger enums and definitions. | | Y | Refactor of eventCategory | N/A |
| supplyType | 1.0.0 | yes | The supply type - Used by clients to route and/or filter supply events by supply type. Also used as a hint for which optional properties would be present/applicable for the supply type. defined in Supply Shared Types. Review Schema for current enums. LFP - future: "wiperRoller", "wasteContainer", "phCleaningRoller", "airflowFilters" - May have composite counts for each filter, "condensateContainer" | type defined in Supply Shared Types | Y | Renamed, consumableType, updated enum list. | ICartridges::ISlot (isSupply, isDrum, isPh) IMaintenance |
| defaultSupplyUnit | | yes | string enum of units. e.g. milligrams Whatever unit applies to the majority of the measurements for this supplyType. | type defined in Supply Shared Types | | Units are implicit in the Capacity structure for Ph/InkSupply/Toner. Think on adding a function to ask for it directly. Units are specified for Maintenance. | |
| eventCode | 1.0.0 | no | Do we need this? How is this used? Is this the event log system error code. i.e 12.06.33. Not included in version 1.0.0. Can be added in next minor revision. | | | Same? | |
| identityInfo | 1.0.0 | yes | object containing supply identity properties. See Identity Info Properties below. | | | New structure | |
| manufacturingInfo | 1.0.0 | no | object containing supply manufacturing properties. See Manufacturing Info Properties below. | | | New structure | |
| stateInfo | 1.0.0 | yes | object containing supply state information. Any value change in this object will trigger a supplyStateChange notification. See State Info Properties below. | | | New structure | |
| \{supplyType}Info i.e. inkCartridgeInfo tonerCartridgeInfo | 1.0.0 | no | object containing supplyType specific properties. See \{supplyType}Info sections below. Sections are: inkCartridgeInfo, tonerCartrigeInfo, inkTankInfo, printHeadInfo | | | New structure | |
| supplyAttributeInfo | 1.0.0 | no | Object containing re-usable properties. A mix of volatile and non-volatile properties. The non-volatile properties are set when the supply is newly discovered by the device. Note: Changes to the volatile properties DO NOT trigger a notification trigger. See supplyAttributes Info section below. | | | new structure | |
| lifeInfo | 1.0.0 | yes | Object containing life related properties. A value change to the levelState property in this object will trigger a "supplyLevelChanged" notification trigger. Value changes to the remaining properties DO NOT trigger a notification. See supplyLife Info Properties section below. | | | new structure | |
| deviceInfo | 1.0.0 | no | Object containing device attributes, not specific to the supply instance. | | | | |
| previousSupplyInfo | 1.0.0 | no | Object containing properties about the previous supply. This object is present if the notificationTrigger is "supplyChangeDetection". supplyUniqueId to enable referencing the previous supply data along with critical data that may have changed since since the last event for the previous supply; "percentageLevelRemaining" and "lastUsedDate". See prevousSupply Info section below. | | | Similar, renaming, extended. | |
| aa | 1.5.0 | no | section for Active Authentication: graylist, remote challenge | | | | |
| deviceUuid | 1.0.0 | yes | originatorDetail provides this data. Removing duplication. | | Y | Removed | |
| deviceModel MakeAndModel | 1.0.0 | yes | originatorDetail provides this data. Removing duplication. | | Y | Removed | |
| deviceSerialNumber | 1.0.0 | yes | originatorDetail provides this data. Removing duplication. | | Y | Removed | |
| firmwareDateCode | 1.0.0 | yes | originatorDetail provides this data. Removing duplication. | | Y | Removed | |

### Definitions

#### iphFabDataTIJ2XData

Description: Pen fab manufacturing data (raw data from Pen ID bits - IPH only) - IPH as a cartridge

The wiki provides details on the fields required in the schema. Because this schema is shared between many supplies, the data required for each supply type varies.

The Data Requirement Document provides details on data requirements.

| Property (new in) Version | Schema Required | Description | OCV Required | Sirius 1.3 Compare | Dune PEI |
|---|---|---|---|---|---|
| dieLocation | 1.1.0 | | TIJ 2.X - 10 or 11 bit integer | New | REVIEW |

#### iphFabDataTIJ4Data

Description: Pen fab manufacturing data (raw data from Pen ID bits - IPH only) - IPH as a cartridge

The wiki provides details on the fields required in the schema. Because this schema is shared between many supplies, the data required for each supply type varies.

The Data Requirement Document provides details on data requirements.

| Property (new in) Version | Schema Required | Description | OCV Required | Sirius 1.3 Compare | Dune PEI |
|---|---|---|---|---|---|
| fab | 1.1.0 | | TIJ4 wafer FAB number where the die was built - will only see 0 (Corvallis) and 2 (Singapore) - 2 bit number (0 to 3) | New | REVIEW |
| fabSerial | 1.1.0 | | TIJ4 Fab serial number - 10-bit number | | |
| fabWafer | 1.1.0 | | TIJ4 Fab wafer number in the lot | | |
| fabWeek | 1.1.0 | | TIJ4 Week the wafer was started (0-53) | | |
| fabYear | 1.1.0 | | TIJ4 Year the wafer was started (only showing the single digit integer of the year, i.e. 2020 shows 0) | | |
| dieCol | 1.1.0 | | | | |
| dieRow | 1.1.0 | | | | |
| dieLocation | 1.1.0 | | TIJ4, TIJ2X for TIJ 2.X - 10 or 11 bit integer | | |

#### iphFabDataTIJ5Data

Description: Pen fab manufacturing data (raw data from Pen ID bits - IPH only) - IPH as a cartridge

The wiki provides details on the fields required in the schema. Because this schema is shared between many supplies, the data required for each supply type varies.

The Data Requirement Document provides details on data requirements.

| Property (new in) Version | Schema Required | Description | OCV Required | Sirius 1.3 Compare | Dune PEI |
|---|---|---|---|---|---|
| fab | 1.1.0 | | TIJ4 wafer FAB number where the die was built - will only see 0 (Corvallis) and 2 (Singapore) - 2 bit number (0 to 3) | New | REVIEW |
| fabSerial0 | 1.1.0 | | TIJ5 Fab serial number - 10-bit number | | |
| fabSerial1 | 1.1.0 | | TIJ5 Fab serial number - 10-bit number | | |
| fabSerial2 | 1.1.0 | | TIJ5 Fab serial number - 10-bit number | | |
| fabWafer0 | 1.1.0 | | TIJ5 Fab wafer number in the lot | | |
| fabWafer1 | 1.1.0 | | TIJ5 Fab wafer number in the lot | | |
| fabWafer2 | 1.1.0 | | TIJ5 Fab wafer number in the lot | | |
| fabWeek0 | 1.1.0 | | TIJ5 Week the wafer was started (0-53) | | |
| fabWeek0 | 1.1.0 | | TIJ5 Week the wafer was started (0-53) | | |
| fabWeek0 | 1.1.0 | | TIJ5 Week the wafer was started (0-53) | | |
| fabYear0 | 1.1.0 | | TIJ5 Year the wafer was started (only showing the single digit integer of the year, i.e. 2020 shows 0) | | |
| fabYear1 | 1.1.0 | | TIJ5 Year the wafer was started (only showing the single digit integer of the year, i.e. 2020 shows 0) | | |
| fabYear2 | 1.1.0 | | TIJ5 Year the wafer was started (only showing the single digit integer of the year, i.e. 2020 shows 0) | | |
| dieCol0 | 1.1.0 | | | | |
| dieCol1 | 1.1.0 | | | | |
| dieCol2 | 1.1.0 | | | | |
| dieRow0 | 1.1.0 | | | | |
| dieRow1 | 1.1.0 | | | | |
| dieRow2 | 1.1.0 | | | | |

### Identity Info Properties

The wiki provides details on the fields required in the schema. Because this schema is shared between many supplies, the data required for each supply type varies.

The Data Requirement Document provides details on data requirements.

| Property (new in) Version | Schema Required | Description | Schema dependency | OCV Required | Sirius 1.3 Compare | PEI |
|---|---|---|---|---|---|---|
| supplyUniqueId | 1.0.0 | Yes | Unique id per supplyType. Used as the database key. Must be unique within the scope of the supplyType technology and consistent across the full ecosystem, including manufacturing databases. Devices are not allow to create supplyUniqueId on their own. They must follow guidelines indicated in this document. Refer to supplyUniqueId specification. Unique id per supplyType. Used as the database key. Must be unique within the scope of the supplyType technology, need to document how the uniqueId is derived. Example for supplies without chip technology e.g. pickRollers; the deviceUUID could be used as a surrogate. For example: deviceUUID+{supplyTypeCode}+{InstallCount} would make the supply unique to the device, differentiate by supplyType, plus installCount differentiating multiple instances being tracked at the device level. | type defined in Supply Shared Types | Y | Renamed consumableUniqueId, same definition | There is no direct call for a whole life UID. For Supplies with Chip use a hw unique id, for others a unique should be created knowing that it will be weak when replacing. IAuthenticationDataExtensionSnapshot::getUuid() ICartridgeSnapshot::getMemoryChipIdentifier() REVIEWED ( revert to RED if disconform, if ok, remove this line ) DUNE-16848 |
| productNumber | 1.0.0 | no | Supply product number in printer | type defined in Supply Shared Types | Y | | IAuthenticationDataExtensionSnapshot::getProductNumber() REVIEWED ( revert to RED if disconform, if ok, remove this line ) DUNE-16848 |
| orderNumber | 1.0.0 | no | Supply product number used to order a replacement supply. e.g. CF283A | type defined in Supply Shared Types | Y | Renamed conumableProductNumber, same defintion | ICartridgeSnapshot::getOrderNumber() REVIEWED ( revert to RED if disconform, if ok, remove this line ) DUNE-16848 |
| serialNumber | 1.0.0 | no | Supply serial number, if available. | type defined in Supply Shared Types | Y | Same | CartridgeSnapshot getSerialNumber |
| supplyColorCode | 1.0.0 | no | Leverage string enum from Sirius 1.3 schema. Not always present, depends on supplyType. | type defined in Supply Shared Types | Y | Renamed consumableLabelCode, same defintion | ISlot / CartridgeSnapshot getColors() |
| colors | 1.4.0 | | array of colors for multi color | type defined in Supply Shared Types | | | |
| slot | 1.1.0 | no | Supply slot number, if applicable. Important for LF because they have duplicate label/color codes that will be distinguished by which slot the supply is in. | | | New | ISlot |
| selectabilityNumber | 1.0.0 | no | Ink: The "selectability number" string decoded from the IPH printhead memory or IIC Acumen. Intended to represent the set of supplies that are all compatible with the same printers. Laser: Super-set identifier for supply product numbers; multiple cartridges are generally mapped to one selectability (e.g. mono and color cartridges); multiple printer platform subsets are generally mapped to one selectability as cartridges can be used in different printer products; in PDB Web Portal listed as 'Cartridge Package Selectability' ; in RDMA referred to as 'selectability_cd' | type defined in Supply Shared Types | | Same | ICartridgeSnapshot |
| brand | 1.0.0 | | Vendor of the supply i.e. HP, Samsung. Examples: approvedOEM, clone, HP, nonApprovedOEM, refill, unauthorized, unknown | type defined in Supply Shared Types | | Same | ICartridgeSnapshot |
| supplyFamilyId | 1.0.0 | | Leverage Sirius 1.3 definition? Acumen Template to Use. a variable that FW uses to decode the acumen data blob. Is this technology specific? | | | Same | IAuthenticationDataExtensionSnapshot::getFamilyId() REVIEWED ( revert to RED if disconform, if ok, remove this line ) DUNE-16848 |
| modelNumber | 1.0.0 | | Ink: the pen to printer map version of Model Number (from the supply_black_errors_0713.json, in identityInfo). Laser: does not apply | | Y | Same | IAuthenticationDataExtensionSnapshot::getModelNumber() REVIEWED ( revert to RED if disconform, if ok, remove this line ) DUNE-16848 |
| model | 1.0.0 | | Ink: does not apply. Laser: Cartridge model information (CMI) field from e-Label (memory chip attached to LaserJet cartridge). This field (along with the CartridgeModelLife (CL) and Regioncode) provides the information required to uniquely identify a cartridge model. | | Y | Same | IAuthenticationDataExtensionSnapshot::getLaserModel() REVIEWED ( revert to RED if disconform, if ok, remove this line ) DUNE-16848 |
| modelLife | 1.0.0 | | Cartridge life information field from e-Label. This is the life of the cartridge model (not the life of the actual cartridge); can be different even within a supply product number to indicate host/starter supply; these values are maintained in Cartridge Definition Documents by supply R&D | | Y | Same | IAuthenticationDataExtensionSnapshot::getModelLife() It is an hexadecimal number. REVIEWED ( revert to RED if disconform, if ok, remove this line ) DUNE-16848 |
| supplyInsertionCount | 1.0.0 | | Lifetime monotonously incrementing counter. Increments each time a new supply (new consumableUniqueId) is inserted in a particular supply slot. supplyInsertionCount represents the # of valid insertions that have taken place, including 'virtual supplies' (== empty slot) in those devices that allow to print with partial number of supplies. | | | Same | ISlotSnapshot::getNumberOfInsertions |
| supplySetId | 1.0.0 | | Combination of the device UUID and the supplyInsertionCount: <deviceUuid>-<10 digit supplyInsertionCount> Example: 3715a27ff2d642249ee528986a77ded0-0000001234 (also duplicated in supply and RTP events) | | | Same | This should be build in the CDM layer and not being part of the PEI. |
| supplyRegion | 1.1.0 | | Ink: Regional compatibility indicator for region-coded supplies. The specific meaning of a given region code value varies between supply families. Laser: Updated documentation 1/25/2021. This is the FW value for 'Zone' provided from a lookup table that identifies the customer facing value for the supply zone (Typically given as 1,2,3). This value should be analogous to the HW region value regionCode. Not to be confused with printerRegion which is a different element on Laser and not interchangeable. | | | Same | ICartridgeSnapshot |
| serviceCode | 1.6.0-alpha.2 | | code used for service team to mainly identify preventiveMaintananceKit supply type. This field is only implemented for preventiveMaintenanceKit supply type for Large Format DUNE printers | type defined in Supply Shared Types | | | |
| supplyDescription | 1.6.0-alpha.2 | | description that enables mainly to identify preventiveMaintananceKit supply type. This field is only implemented for preventiveMaintenanceKit supply type for Large Format DUNE printers | type defined in Supply Shared Types | | | |

#### supplyUniqueId specification

| Property | Type | Acumen | IPH |
|---|---|---|---|
| supplyUniqueId | String | Acumen 5: selectabilityNumber + colorCode + manufacturingID DEPRECATED. UniqueId encoded in acumen. Acumen should cover ICC, LFP printheads and HPPK toner (to be confirmed). Total of 32 bytes. Acumen 5: baseKeyId. Unique ID that meets requirements of uniqueness and security (signed). Acumen 6: PERSO-UUID. Perso-UUID is a random number identifier set during Acumen Perso manufacturing. The lower (LSB) 16 bytes of Perso-ID. Total of 32 lowercase hexadecimal characters | Aria + Fab wafer data. Fab wafer data contains row, colum, wafer number and calibration data. Black pens fab data is 64 bits long. Color pens fab data is 192 bits long. Length for IPH is 72 + 192 bits = 33 bytes. Total of 33 bytes. Aramaki-Lo: HSM UID + AddressOrder + Diode + Mfg Line + Mfg Month + Mfg Year + PenType + Region + SKD + Class. Bytes arrangement for supplyUniqueId: Uid 54 bits 14 hex characters, Address 4 bits 1 hex character, Diode 8 bits 2 hex characters, Line 6 bits 2 hex characters, Month 4 bits 1 hex characters, Year 5 bits 2 hex characters, PenType 5 bits 2 hex characters, Region 5 bits 2 hex characters, SKD 3 bits 1 hex character, Class 2 bits 1 hex character. Total of 28 hex characters. Example: idBits in base64, fields in hex characters. UID: 1be73ebe16a81d Color: CMY. idBits TuZlNSnwcHDDhgAxsYSMFOmZEkydOEBAgwA44AbdGO5M4D0CjD8m/ROQzP8/E0C/lnamBN9/w8xJh2AAAfwABwD2Fzvrgzps7/uMdO64FWh9fOfYAIgAQAAAATjEGkBmnEAiaT0AAP4BAAAAAAAAACYAQ6BgEAC6wa4AEABqtLdTyZLeRBaDT8Cf3mi1xRcga4pL. uid 1be73ebe16a81d, address 1, diode 65, line 0b, month 3, year 00, penType 03, region 01, skd 3, class 2, suid 1be73ebe16a81d1650b300030132 |

| Property | Type | Laser with eTag | Laser No eTag |
|---|---|---|---|
| supplyUniqueId | String | CMI+CL+Region+SerialNumber+ManufacturDate. Combination of 5 fields encoded in the eTag that generate a unique ID across factories and regions. a = CMI: 4 hex chars, b = CL: 4 hex chars, c = Region: 4 hex chars, e = SerialNum: 10 decimal digits (left zero padded), d = MfgDate: 8 decimal digits (zero padded) in the form "YYYYMMDD". Total of 30 characters. The supplyUniqueId string contains a mix of lowercase hexadecimal and decimal characters. Template: 30 characters aaaabbbbcccceeeeeeeeeedddddddd. Example: Supply GL Data | CMI+CL+Region+Hash+GaussTotalImpression. Combination of 5 fields encoded as follows: a = CMI: Cartridge Model Information (Hardcoded in firmware, provided by Canon, Ref: CDD) - (4 hex characters), b = CL: Cartridge Life. (Hardcoded in firmware, 0000- CL Value is unknown) (4 hex characters), c = Region: Region Code. (Hardcoded in firmware, provided by Canon, Ref: CDD) (4 hex characters), d = Hash: The SHA256 hash(32 bytes) of the device UUID truncated to most significant (leftmost) 52 bits (13 hex characters), e = Gauss Total Impression count: when Imaging drum was Installed (for drum) or Gauss Total Impression count when toner was refilled. Shown in hex (5 hex characters). Template: 30 characters aaaabbbbccccdddddddddddddeeeee |
| supplyUniqueId (for A3 laser products) | String | CMI+CL+Region+SerialNumber+ManufacturDate. Combination of 5 fields encoded in the eTag that generate a unique ID across factories and regions. a = CMI: 4 hex chars, b = CL: 4 hex chars, c = Region: 4 hex chars, e = SerialNum: 25 ASCII chars (left zero padded), d = MfgDate: 8 decimal digits (zero padded) in the form "YYYYMMDD". Total of 45 characters. The supplyUniqueId string contains a mix of lowercase hexadecimal, decimal, and ASCII characters. Template: 45 characters aaaabbbbcccceeeeeeeeeeeeeeeeeeeeeeeeeddddddd. Example: Supply GL Data | CMI+CL+Region+Hash+GaussTotalImpression. Combination of 5 fields encoded as follows: a = CMI: Cartridge Model Information (Hardcoded in firmware, provided by Canon, Ref: CDD) - (4 hex characters), b = CL: Cartridge Life. (Hardcoded in firmware, 0000- CL Value is unknown) (4 hex characters), c = Region: Region Code. (Hardcoded in firmware, provided by Canon, Ref: CDD) (4 hex characters), d = Hash: The SHA256 hash(32 bytes) of the device UUID truncated to most significant (leftmost) 108 bits (27 hex characters), e = Gauss Total Impression count: when Imaging drum was Installed (for drum) or Gauss Total Impression count when toner was refilled. Shown in hex (6 hex characters). Template: 45 characters aaaabbbbccccdddddddddddddddddddddddddddeeeeee |

### Manufacturing Info Properties

The wiki provides details on the fields required in the schema. Because this schema is shared between many supplies, the data required for each supply type varies.

The Data Requirement Document provides details on data requirements.

| Property (new in) Version | Schema Required | Description | Schema Dependency | OCV Required | Sirius 1.3 Compare | Dune PEI |
|---|---|---|---|---|---|---|
| manufacturer | 1.0.0 | no | for Acumen and Canon based systems this field represents the raw data stored on the cartridge chip. For IPH systems this will be processed by FW to provide HP and nonHP | | Y | Same | IAuthenticationDataExtensionSnapshot::getManufacturer() REVIEWED ( revert to RED if disconform, if ok, remove this line ) DUNE-16848 |
| manufactureDate | 1.0.0 | no | Time stamp of when the supply was manufactured, if available. Type must be glossary.dateTime UTC format. | type defined in Glossary | Y | Same | AuthenticationExtension getManufac:turingWeek getManufacturingYear |
| manufacturingSignature | 1.0.0 | no | Definition? Should this be an object with "signature" and "type" e.g. signature = "uov data" type = "uovSignature" | | Y | Rename consumableManufacturingSignature, same definion. | AuthenticationExtension |
| manufacturingId | 1.0.0 | no | manufacturingId printed on the outside of the box? | type defined in Supply Shared Types | | Ranamed from midLabel | IAuthenticationDataExtensionSnapshot::getManufacturingId() REVIEWED ( revert to RED if disconform, if ok, remove this line ) DUNE-16848 |
| manufacturingSite | 1.0.0 | no | manufacturing location supply was build sitename - was previously sitename + mfgline. Values: malaysiaMagma4, STM, CJA, Foxcomm | | | | |
| manufacturingLine | 1.1.0 | no | Manufacturing Line. Values: L1, L2, L3, L4, L5, L6, L7, L8, L9, L10, L11, L12, L13, L14, L15, L16, L17, L18, L19, L20, L21, L22, L23, L24, L25, L26, L4E, Orcus2, Orcus3, M1, M4 | | | | |
| manufacturingStatus | 1.0.0 | no | Requested by Mfg - Records supply's end state in factory: GOOD means OK, shipped; SCRAP means supply built but never shipped from factory. Values: good, scrap, audit, onHold | | | | |

### State Info Properties

The wiki provides details on the fields required in the schema. Because this schema is shared between many supplies, the data required for each supply type varies.

The Data Requirement Document provides details on data requirements.

| Property (new in) Version | Schema Required | Description | Schema Dependency | OCV Required | Sirius 1.3 Compare | Dune PEI |
|---|---|---|---|---|---|---|
| supplyState | 1.0.0 | Yes | High level supply state. string enum: "ok" - All good, "stateResaons" is "none" and all sub states are "ok", "inform" - All good, "stateReasons" is not empty and have some extra information, "warning" - Device still printing but supplyStateDetails:stateReasons" contains reasons why the state is not "ok", "error" - Printing is blocked. supplyStateDetails.stateReasons" contains reasons why the state is not "ok", "unknown" - not applicable to telemetry, means no telemetry event will be published with supplyState = "unknown" | | Y | New, refactor of trigger reasons and consumableState | ICartridges::getState() |
| stateReasons | 1.0.0 | Yes | Reasons why the "state" is not equal to "ok". AI: Reconcile with Sirius eventTrigger | type defined in Supply Shared Types | | New, refactor of trigger reasons and consuableState | ICartridges::getStatus() coarse grained ICartridges::getDetailedStatus() fine grained REVIEWED: enumeration checked ( revert to RED if disconform, if ok, remove this line ) DUNE-16848 |
| eventCode | 1.0.0 | no | Event Code | | | | |
| inSafeStopMode | 1.1.0 | no | move to stateReasons enum? | | | Moved, same definition | I guess this is part of the Status (SAFE_STOP) REVIEW |
| maxTrialsReached | 1.1.0 | no | move to stateReasons enum? | | | Moved, same definition | Coming from homesmb - Instant Ink maxim amount of phs used on onboarding. REVIEW |
| inReserveMode | 1.1.0 | no | move to stateReasons enum? | | | Moved, same definition | Coming from homesmb - When a ink is OOI but you want to continue printing with other colors. REVIEW |
| singleCartridgeMode | 1.1.0 | no | move to stateReasons enum? | | | Moved, same definition | User removes a ctg and prints without it - IPH. REVIEW |

### inkCartridgeInfo Properties

The wiki provides details on the fields required in the schema. Because this schema is shared between many supplies, the data required for each supply type varies.

The Data Requirement Document provides details on data requirements.

| Property (new in) Version | Required (mandatory) | Description | Schema dependencies | Sirius 1.3 Compare | Dune PEI |
|---|---|---|---|---|---|
| inkCapacity | 1.0.0 | Yes | Approximate usable capacity Based on feedback from Dave Novak, the name is misleading. Usable capacity, not Fill compacity. This is T2 for ink, also known as customer average available ink (customer usable extractable ink). Latest agreement: inkCapacity should reflect the usable ink to customer, which can be calculated as encoded T2 - in channel WVL - startup servicing - new insertion priming | | renamed inkFillCapacity similar definition | ICartridgeSnapshot getCapacity |
| inkCapacityUnit | 1.1.0 | Yes | Units for the inkCapacity. | type defined in Supply Shared Types | | |
| refillThreshold | 1.0.0 | Yes | Ink t4 refill threshold, defaultSupplyUnit e.g t4 | | renamed | Threshold that detects the refill. REVIEW |
| refillThresholdUnit | 1.1.0 | Yes | Units for refill threshold unit | type defined in Supply Shared Types | | |
| inkLevelSensorValue | 1.0.0 | Yes | IIC Gen1 - PTOOI last temperature value. IIC Gen2 - PHA SHAID sensor reading | | Same | |
| inkLevelGauge | 1.0.0 | Yes | A continuous value representing the amount of ink sensed to be present by an ink level measurement technology (such as Sherlock). For IPH products, this field is set to lifeInfo.percentLifeRemaining. (definition needs review) | type defined in Supply Shared Types | Same | |
| postStartupSupplyVolume | 1.0.0 | iic gen1/gen2/pwa with acumen | The amount of ink available after the startup (OOBE). It refers to the printhead given for the OOBE (recheck) | | Same | This is something not in the PEI, but it should be get via ICartridgeSnapshot::getLevel after the startup. |
| preInstallWvl | 1.4.0 | iph / iic | WVL (water vapor loss) in total ink lost from the supply pre-install (shipping channel) | type defined in Supply Shared Types | | |
| postInstallWvl | 1.4.0 | iph/ iic | WVL (water vapor loss) in total ink lost from the supply post-install (in printer) | type defined in Supply Shared Types | | |
| shaidSensorReading | 1.1.0 | iic gen2/ iph ciss | IIC Gen2 PWAX, some IPH CISS products and IIC CISS products | | | |
| ptooiState | 1.1.0 updated 1.3.0 with new enums | iic gen1 | IIC Gen1, state information for PTOOI (print thermal out of ink). "undefined", "differentInk", "ink", "lookingForAir", "air", "altered", "malfunctioning", "aborted", "differentAirButPrinterNotReady", "t4AwaitingPriming". A supply would report ptooiState of 'ink' while the supply's levelState reports 'ok'. As soon as levelState gets to 'low', ptooiState would change to 'lookingForAir'. Finally, when levelState gets to 'veryLow', ptooiState would change to 'air'. In the event that, while in 'air', ink is detected, ptooiState would change to 'altered'. | | | |
| eurekaState | 1.1.0 | iph | IPH, new functionality with Vasari. "cal1Needed", "cal1Done", "cal2Needed", "cal2Done", "cal3Needed", "cal3Done", "ooiTestNeeded", "ooiKnown1", "ooiKnown2", "ooiKnown3", "ooiKnown4", "ooiKnown5", "ooiKnown6", "ooiKnown7", "refilled" | | | |
| printUniqueness | 1.1.0 | iph | PIDF Printer Uniqueness | | | |
| compositeCounts | 1.0.0 updated 1.1.0 | iph cmy | supplyType e.g. inkCartridge specific composite counts. When a supply has sub-components. This represents those sub-components like for a CMY supply giving the level for each of the supplies. updated to include order (need to provide order documentation) | | Similar, renmes, enhanced | REVIEW |
| compositeCounts.order | 1.1.0 | iph cmy | The order of the composit ink. Values: CYM, CMY, YCM, YMC, MCY, MYC | | | |
| compositeCounters.c | 1.0.0 | iph cmy | Structure with lifeCount, lowThreshold | | | |
| compositeCounters.m | 1.0.0 | iph cmy | Structure with lifeCount, lowThreshold | | | |
| compositeCounters.y | 1.0.0 | iph cmy | Structure with lifeCount, lowThreshold | | | |
| reserveMode | 1.0.0 | iic gen2 | Indicates whether a supply is being used in reserve mode to compensate for missing colors of ink. compositeBack, greySlale. When in reserve mode, in which mode is the system. | | | ICartridgeSnapshot::getReserveMode() REVIEWED: New enum added on microservice JSON and Dune counterpart in Cartridges.fbs, ICartridges updated ( revert to RED if disconform, if ok, remove this line ) DUNE-16848 |
| expirationDate | 1.0.0 | Never in consumer / latex supplies only | expiration date of the ink supply. | type defined in Glossary | New | ICartridgeSnapshot::getExpirationDate() |
| idBitRevision | 1.0.0 | iph | Revision number for the data being written to the supply (important for supply refresh identification). IPH cartridges now contain a revision for the bit string being used. For SIE and troubleshooting reasons, it would be extremely helpful to have this value visible in big data (instead of having to go find the value in the data BLOB) | | Same | |
| persoRevision | 1.0.0 | acumen | Perso revision number for the data being written to the supply (important for supply refresh identification). Its an Acumen mechanism which documents the partitions, keys, and other information encoded in the personalization process. For SIE and troubleshooting reasons, it would be extremely helpful to have this value visible in bit data (instead of having to go find the value in the data BLOB) | | Same | ICartridgeSnapshot::getPersoRevisionNumber() REVIEWED: ICartridges updated ( revert to RED if disconform, if ok, remove this line ) DUNE-16848 |
| hostTradeId | 1.0.0 | Yes | part of pen to printer map - contact Dave Novak for more info | | | |
| subBrand | 1.0.0 | Yes | part of pen to printer map - contact Dave Novak for more info (all ink and GSB products) | | | |
| desKeying | 1.0.0 | Yes | part of pen to printer map - contact Dave Novak for more info (all ink and GSB products - also known as class) | | | |
| penType | 1.1.0 | iph | part of pen to printer map (IPH only) | | | |
| supplyKeyDescription | 1.0.0 | Yes | part of pen to printer map - contact Dave Novak for more info (all ink and GSB products) | | | |
| ssa | 1.0.0 | Yes | part of pen to printer map - contact Dave Novak for more info (all ink and GSB products) | | | |
| majorAccount | 1.0.0 | acumen | part of pen to printer map - contact Dave Novak for more info | | | |
| timeTravel1 | 1.0.0 | Yes | part of pen to printer map - contact Dave Novak for more info (all ink and GSB products) | | | |
| timeTravel2 | 1.0.0 | Yes | part of pen to printer map - contact Dave Novak for more info | | | |
| timeTravel3 | 1.0.0 | Yes | part of pen to printer map - contact Dave Novak for more info (all ink and GSB products) | | | |
| timeTravel4 | 1.0.0 | Yes | part of pen to printer map - contact Dave Novak for more info (all ink and GSB products) | | | |
| timeTravel5 | 1.0.0 | Yes | part of pen to printer map - contact Dave Novak for more info (all ink and GSB products) | | | |
| templateMajor | 1.0.0 | acumen | part of pen to printer map - contact Dave Novak for more info (all acumen based ink and GSB products) | | | |
| templateMinor | 1.1.0 | acumen | part of pen to printer map - contact Dave Novak for more info (all acumen based ink and GSB products) | | | |
| trademark | 1.0.0 | Yes | part of pen to printer map - contact Dave Novak for more info (all ink and GSB products) | | | |
| iphFabDataTIJ2X | 1.1.0 | iph | Pen fab manufacturing data (raw data from Pen ID bits - IPH only) - IPH as a cartridge. type is defined in schema - iphFabDataTIJ2XData | | | |
| iphFabDataTIJ4 | 1.1.0 | iph | Pen fab manufacturing data (raw data from Pen ID bits - IPH only) - IPH as a cartridge. type is defined in schema - iphFabDataTIJ4Data | | | |
| iphFabDataTIJ5 | 1.1.0 | iph | Pen fab manufacturing data (raw data from Pen ID bits - IPH only) - IPH as a cartridge. type is defined in schema - iphFabDataTIJ4Data | | | |
| consumableId | 1.0.0 | iph* | The consumableId is the current value of the pen id bits in the memory device with in the pen. Eg, we may change/record some bits within the pen to record that the pen is now used when the user first install a new pen. Pen id bits are also populated in supplyAttributeInfo.consumableRawData. So this field is a duplicate for IPH. Starting from Victoria (Aramaki-Lo), future IPH products will not populate this field. | | | |
| iphUniqueId | 1.1.0 | iph | IPH based ID | | | |
| platformFamily | 1.0.0 new fields added in 1.1.0 | Yes | ink specific platform family. Visit 'inkPlatformFamily' enum in schema com.hp.cdm.service.supply.version.1.sharedTypes.supply.schema | | | |
| inkSupplyType | 1.8.0 | iic | SupplyType from Acumen and Pen-to-Printer map. It is used to decide to accept/reject supplies with. Would be useful for big data and AA. IIC only. Note that it's the same as the integer type of supplyType in SupplyAssessment.inkDetailInfo.supplyType. | | renamed from supplyType | |
| iphAnalogBitsAnalogIdWidthInBytes | 1.8.0 | iph | Number of bytes for each analog pen ID value | | | |
| iphAnalogBitsAnalogIdScaleShift | 1.8.0 | iph | Number of LSB bits removed from each analog pen ID value | | | |
| iphAnalogBitsAnalogIdDataB64 | 1.8.0 | iph | Base 64 encoded analog value of logical ID bits in descending order, i.e, from highest id to the lowest id bit. The buffer should be lzip compressed prior to base64 encode. | | | |

### tonerCartridgeInfo Properties

The wiki provides details on the fields required in the schema. Because this schema is shared between many supplies, the data required for each supply type varies.

The Data Requirement Document provides details on data requirements.

| Property (new in) Version | Schema Required | Description | Sirius 1.3 Compare | Dune PEI |
|---|---|---|---|---|
| compositeCounts | 1.1.0 | | supplyType e.g. tonerCartridge specific composite counts. If a composite supply, sub life counts represented in this object. Worst case life count replicated in the root lifeCount and lifeExpected properties. Example: "developerWear", "engineToner", "formatterToner", "wasteToner", "developer", "imageDrum" | New, made composite counts technology specific | REVIEWED: ICartridges updated, new class CompositeCounts that contains LifeCounter struct that mimics CountersSnapshot of Counters.fbs ( revert to RED if disconform, if ok, remove this line ) DUNE-16848 |
| cleaningCycles | 1.0.0 | | cleaning cycle count for the supply instance. | New | REVIEWED: ICartridges updated ( revert to RED if disconform, if ok, remove this line ) DUNE-16848 |
| tonerArrivalTime | 1.4.0 | | During the cartridge alienation detection process the engine will try to form toner with the cartridge alienated and then measure the time that toner reaches the CPR sensor. If the cartridge is alienated, toner is not formed and the engine indicates the toner arrival time is msecs | | |
| regionCode | 1.1.0 | | Update description 1/25/2021. The code provided by Canon (eTag value) - 2 character hex strings -for example: 0x10, 0x20, 0x30, 0xFF. (where the 0x denotes a hex value to follow) This value is used in the Supply UUID. | | |
| platformFamily | 1.0.0 | | toner specific platform family. "acumen4.1", "acumen5", "acumen6", "cub", "cub+", "cat4", "fox", "crum", "fox+", "eeProm", "hppkLaser", "canonLaser" | | |
| printingPastBeyondVeryLow | 1.10.0 | | This property is set to true when the printer detects that the installed cartridge has reached the "Beyond Very low " threshold, and the customer chooses to continue printing after receiving the corresponding prompt notification. The set of this property will not trigger a telemetry event but it is expected that the could gets the value on the next timedInterval event. This property is set to false for new supplies. | | |

### inkTankInfo Properties

The wiki provides details on the fields required in the schema. Because this schema is shared between many supplies, the data required for each supply type varies.

The Data Requirement Document provides details on data requirements.

| Property (new in) Version | Schema Required | Description | Sirius 1.3 Compare | Dune PEI |
|---|---|---|---|---|
| shaidSensorReading | 1.1.0 | | IPH CISS products | New | REVIEW( type not defined yet in CDMFleetSuppklyInfo.xlsx ) |
| markingAgentUsedPastShaid | 1.1.0 | | Amount of ink used after the ink level sensor is exposed - 0 means shaid is covered | New | REVIEW( type not defined yet in CDMFleetSuppklyInfo.xlsx ) |
| platformFamily | 1.1.0 | | ink tank platform family "iphSingleShaidCiss" | New | |

### printHeadInfo Properties

The wiki provides details on the fields required in the schema. Because this schema is shared between many supplies, the data required for each supply type varies.

The Data Requirement Document provides details on data requirements.

| Property | SubField (new in) Version | Schema Required | Description | Sirius 1.3 Compare | Dune PEI |
|---|---|---|---|---|---|
| iphFabDataTij2X | | 1.1.0 | | Pen fab manufacturing data (raw data from Pen ID bits - IPH only) | |
| iphFabDataTij4 | | 1.1.0 | | Pen fab manufacturing data (raw data from Pen ID bits - IPH only) | New | REVIEW( type not defined yet in CDMFleetSuppklyInfo.xlsx ) |
| iphFinalAssemblyData | | 1.1.0 | | Pen final assembly manufacturing data (raw data from Pen ID bits) | New | REVIEW( type not defined yet in CDMFleetSuppklyInfo.xlsx ) |
| iphFinalAssemblyData | desKeying | 1.1.0 | | Part of Pen to Printer Mapping (duplicate of class) | New | |
| iphFinalAssemblyData | extendedLife | 1.1.0 | | use the Extended Ink Fill Table | | |
| iphFinalAssemblyData | host | 1.1.0 | | ost vs Trade supply | | |
| iphFinalAssemblyData | longBodyPen | 1.1.0 | | Is this a long body pen | | |
| iphFinalAssemblyData | lowFillScale | 1.1.0 | | use the low fill ink fill table | | |
| iphFinalAssemblyData | mfgLine | 1.1.0 | | which FA Line | | |
| iphFinalAssemblyData | mfgMonth | 1.1.0 | | FA Month Built | | |
| iphFinalAssemblyData | mfgYear | 1.1.0 | | FA Year Built based on a Year Offset | | |
| iphFinalAssemblyData | modT1T3 | 1.1.0 | | Low On Ink Table Reference | | |
| iphFinalAssemblyData | penMoved | 1.1.0 | | Has the pen moved to a different printer | | |
| iphFinalAssemblyData | penType | 1.1.0 | | Part of Pen to Printer Mapping | | |
| iphFinalAssemblyData | proto | 1.1.0 | | Is this a Prototype Pen? | | |
| iphFinalAssemblyData | pvpId | 1.1.0 | | Marketing identification | | |
| iphFinalAssemblyData | region | 1.1.0 | | Part of Pen to Printer Mapping | | |
| iphFinalAssemblyData | supplyKeyDescription | 1.1.0 | | Part of Pen to Printer Mapping | | |
| iphFinalAssemblyData | support | 1.1.0 | | Support Message | | |
| iphFinalAssemblyData | timeTravel1 | 1.1.0 | | Part of Pen to Printer Mapping | | |
| iphFinalAssemblyData | timeTravel2 | 1.1.0 | | Part of Pen to Printer Mapping | | |
| iphFinalAssemblyData | timeTravel3 | 1.1.0 | | Part of Pen to Printer Mapping | | |
| iphFinalAssemblyData | timeTravel4 | 1.1.0 | | Part of Pen to Printer Mapping | | |
| iphFinalAssemblyData | timeTravel5 | 1.1.0 | | Part of Pen to Printer Mapping | | |
| iphFinalAssemblyData | trialPen | 1.1.0 | | Is this a Trial Pen (usually also Host Pen) | | |
| iphFinalAssemblyData | trigger1 | 1.1.0 | | Has LOI been reached by color | | |
| iphFinalAssemblyData | trigger2 | 1.1.0 | | Has T2 been reached by color | | |
| iphFinalAssemblyData | consumableId | 1.1.0 | | The consumableId is the current value of the pen id bits in the memory device with in the pen. Eg, we may change/record some bits within the pen to record that the pen is now used when the user first install a new pen. | | |
| iphFinalAssemblyData | ssa | 1.1.0 | | part of pen to printer map (all ink and GSB products) | | |
| iphFinalAssemblyData | trademark | 1.1.0 | | part of pen to printer map (all ink and GSB products) | | |
| iphFinalAssemblyData | subBrand | 1.1.0 | | part of pen to printer map (all ink and GSB products) | | |
| iphFinalAssemblyData | printerUniqueness | | | a value assigned to by IPH printer FW to the cartridge to help provide more supply uniqueness in a limited supply Uniqueness scenario. It is also occasionally used for other information. See SIE for how printerUniqueness is used for a given printer | | |
| iphUniqueId | | 1.1.0 | | iph based id | | |
| timeUsedSeconds | | 1.4.0 | | cumulative time used in seconds | | |
| usedWithNonHpInk | | 1.4.0 | | true if printhead has been used with nonHp ink | | |
| usedWithExpiredHpInk | | 1.4.0 | | true if printhead has been used with expired hp ink | | |
| healthGaugeLevel | | 1.4.0 | | computed health level of the printhead | | |
| paperJams | | 1.4.0 | | number of paper jams experienced by printhead | | |
| platformFamily | | 1.1.0 | | ink printhead family (HestiaCiss is the color tij4 pen, there is a color 2x pen that goes with Poseidon. iphKronosCiss, iphCentaurCiss, iphHestiaCiss | | |
| iphBitsAnalog | | 1.6.0 | | AD readings of the id bits in physical order. Field format: Downshift AD value by 1 bit (from 9bit to 8bit values), Transform bytes into buffer, Compress buffer with ZLib, Convert compressed binary to a Base64 string | | |

### vaReman Properties

The wiki provides details on the fields required in the schema. Because this schema is shared between many supplies, the data required for each supply type varies.

The Data Requirement Document provides details on data requirements.

| Property | SubField (new in) Version | Schema Required | Description | Sirius 1.3 Compare | Dune PEI |
|---|---|---|---|---|---|
| vaRemanCounter | | 1.1.0 | | the number of times supply has be reprogrammed - convert bin to dec (000=0,100=4,110=6,111=7) | | |
| vaRemanSignature | | 1.1.0 | | digital signature | | |
| rUsed | | 1.1.0 | | 3 bit string i.e. 100, 110, 111 | | |
| rawTagFwTonerPlr | | 1.1.0 | | 4Bytes - raw toner remaining value from the formatter | | |
| keyId | | | | | | |
| signatureAlgorithm | | | | com.hp.cdm.service.supply.version.1.sharedTypes.supply.schema.json#/definitions/signatureAlgorithm | | |
| acumenSignatureTemplate | | | | | | |
| vaRemanType | | | | renew types to identify if the renew is hp branded, third party, and third party using hp marking agent. "hpBranded", "thirdParty", "thirdPartyUsingHpMarking" | | |
| eLabelSignatureTemplate | | 1.11.0-alpha.1 | | See definition below | | |

#### eLabelSignatureTemplate

| Field | encoding | Detail |
|---|---|---|
| signatureVersion | integer | range 1-65535 |
| serialNumber | Base64 encoded binary | cartridge serial number that corresponds to original cartridge id |
| remOptionalData | Base64 encoded binary | cartridge life eLabel value that corresponds to the reman cartridge |
| remManufactureDate | Base64 encoded binary | cartridge manufacturer date eLabel value that corresponds to the reman cartridge |
| remId | Base64 encoded binary | see Specification at link |
| region | Base64 encoded binary | cartridge region eLabel value that corresponds to the original cartridge |
| model | Base64 encoded binary | cartridge model eLabel value that corresonds to the original cartridge |
| manufactureDate | Base64 encoded binary | cartridge manufacturer date eLabel value that corresponds to the original cartridge |
| life | Base64 encoded binary | cartridge life eLabel value that corresponds to the original cartridge |
| futureUse2 | Base64 encoded binary | see Specification at link |
| futureUse1 | Base64 encoded binary | see Specification at link |

### supplyAttribute Info Properties

The wiki provides details on the fields required in the schema. Because this schema is shared between many supplies, the data required for each supply type varies.

The Data Requirement Document provides details on data requirements.

| Property (new in) Version | Schema Required | Description | Schema Dependencies | Sirius 1.3 Compare | Dune PEI |
|---|---|---|---|---|---|
| installDate | 1.0.0 | no | Time stamp of when the supply was initially installed in the device. For ink products, this field will be update when the supply is accepted. So it is normal for the field to be missing on telemetry events associated with the new supply before it is accepted. | type defined in Glossary | Same | ICartridgeSnapshot::getInstallDate |
| isGenuineHP | 1.0.0 | | Device genuine HP assessment | type defined in Supply Shared Types | Same | getStatus not having NON_HP REVIEW: It is really necessary to have the GENUINE_HP as a state. |
| totalAgentUsed | 1.0.0 | | Reusable total used count. How much been used in the current printer. | type defined in Supply Shared Types | renamed totalInkUsageGauge similar definition | ICartridgeSnapshot::getTotalAgentUsed() REVIEWED: ICartridges updated: also Counter struct added ( revert to RED if disconform, if ok, remove this line ) DUNE-16848 |
| isRefilled | 1.0.0 | | Supply was detected to have been refilled while in the printer | type defined in Glossary | Same | ::ICartridgeSnapshot getStatus() - CartridgeStatus::REFILLED REVIEWED: it did refer to detected as REFILLED , not REFILLING, added REFILLED to CartridgeStatus enum ( revert to RED if disconform, if ok, remove this line ) |
| isUsed | 1.0.0 | | Supply was detected to have been used at insertion time | type defined in Supply Shared Types | Same | ICartridgeSnapshot::getStatus() - CartridgeStatus::USED_MOVED REVIEWED: ICartridges updated ( revert to RED if disconform, if ok, remove this line ) DUNE-16848 |
| isAltered | 1.0.0 | | Supply was detected to have been refilled at insertion time | type defined in Glossary | Same | ICartridgeSnapshot::getStatus() - CartridgeStatus::ALTERED REVIEWED: ICartridges updated ( revert to RED if disconform, if ok, remove this line ) DUNE-16848 |
| isCounterfeitResponse | 1.0.0 | | When prompted, the customer indicated that they believed the supply to be hp original though it was detected not to be. For ink Products, this field corresponds to the user response to a refill condition. It is not updated in the telemetry event that is triggered when FW detects the refill condition on the ink cartridge. The field will be updated in the next telemetry event triggered by a Cartridge event, e.g., servicing, printing, etc. | type defined in Glossary | Same | ICartridgeSnapshot::isCounterfeitResponse() REVIEWED: ICartridges updated ( revert to RED if disconform, if ok, remove this line ) DUNE-16848 |
| isSetup | 1.0.0 | | A supply with isSetup flag enabled is a supply that has shipped with the printer and only has enough supply to prime the device. If supplyType is "toner", isSetup corresponds to the Starter Cartridge. | type defined in Supply Shared Types | Same | ICartridgeSnapshot::getStatus() - CartridgeStatus::SETUP REVIEWED ( revert to RED if disconform, if ok, remove this line ) DUNE-16848 |
| isTrial | 1.0.0 | | A supply with isTrial flag enabled is a supply sent with a printer to enable Instant* trial. Device will monitor how many supplies with isTrial flag enabled have seen and after a certain amount it will reject with an error state. Field related to Instant* (ink and toner) | type defined in Supply Shared Types | Same | ICartridgeSnapshot::getStatus() - CartridgeStatus::TRIAL REVIEWED ( revert to RED if disconform, if ok, remove this line ) DUNE-16848 |
| isVaReman | 1.1.0 | | Is this a VA remain? has been reprogrammed at least once | type defined in Supply Shared Types | | |
| antiTheftMode | 1.0.0 | | antiTheftMode written to the supply. Enum (printer, fleet, none) defined in Supply Schema | | Same | getSupplySettingValue(ANTI_THEFT, _) |
| lastUsedDateTime | 1.0.0 | | dateTime the supply was last used | type defined in Glossary | Same | ICartridgeSnapshot::getLastUseDate() REVIEWED ( revert to RED if disconform, if ok, remove this line ) DUNE-16848 |
| lowThreshold | 1.0.0 | | User settable threshold at which the supply is believed to be low on remaining printing. Ink, this is equivalent to t1 value in percentage - it is a counter type so a value and a unit are defined. Example: The lowThreshold counter (count, unit) For ink specified in miligramsequivalent to t1 value in milligram units | type defined in Supply Shared Types | Equivalent to 1.3 lowThresholdMg | ICartridgeSnapshot::getLowThreshold() REVIEWED: ICartridges updated ( revert to RED if disconform, if ok, remove this line ) DUNE-16848 |
| lowThresholdPercentage | 1.0.0 | | Duplicate of lowThreadhold. The percent remaining threshold used to indicate when a supply has reached the low warning state. User settable threshold at which the supply is believed to be low on remaining printing. Ink, this is equivalent to t1 value in percentage | | Same | getSupplySettingValue(LOW_THRESHOLD, _) |
| lowTriggered | 1.0.0 | | true if the low on remaining printing threshold has been crossed | type defined in Glossary | Same | We do have the CartridgeState::LOW, but the meaning of the field is if it has been LOW in any moment in the past. REVIEW: It is really needed if the ctg cannot change its status |
| veryLowTriggered | 1.0.0 | | true if the very low on remaining printing threshold has been crossed | type defined in Glossary | Same | We do have the CartridgeState::VERY_LOW, but the meaning of the field is if it has been VERY LOW in any moment in the past. REVIEW: It is really needed if the ctg cannot change its status |
| supplyMarkedEmpty | 1.0.0 | | true if the supply has been marked as empty | type defined in Glossary | Same | We do have the CartridgeState::EMPTY, but the meaning of the field is if it has been EMPTY in any moment in the past. REVIEW: It is really needed if the ctg cannot change its status |
| consumableRawData | 1.0.0 | | Ink: It is the IPH blob data and in Acumen based cartridges its first 256 bytes up to 16K. Toner: eLabel data blob. TODO: Not clear its meaning or common between enterprise / ink. Review its location if reused between toner & ink | | Same | ICartridgeSnapshot::getMemoryChipBitmap |
| serviceIssuer | 1.0.0 | | Business Model describing the supply service used: instantInk, instantToner, aRS | type defined in Glossary | Same | |
| isSubscriptionSupply | 1.0.0 | | true if the supply is for a subscription service (instant ink or instant toner). Ink: A flag indicating whether the supply is associated with a subscription service, and thus not usable in non-subscription printers. Laser: new capability for laser; understanding is to use this to designate whether a specific supply is enabled for ITP (instant toner program) | type defined in Glossary | Same | REVIEW Discuss about the ServiceSubscription |
| consumablePlatform | 1.0.0 | | Type of supply platform. (From Dave Novak) iicGen1, iicGen2, pwax, iph - Integrated print head, cissIph - Continuous ink supply system IPH, hpLaser, canonLaser. Later 1.x consideration: cissIic, other? | | Same, enhanced enums | ICartridgeSnapshot::getConsumablePlatform() REVIEWED: ICartridges updated , new ConsumablePlatform enum at Cartridges.fbs ( revert to RED if disconform, if ok, remove this line ) DUNE-16848 |
| baseKeyId | 1.0.0 | | acumen based id | | | |
| maxCapacity | 1.1.0 | | max capacity of the supply. For ink supply, it is the ink level encoded in the cartridge, a.k.a., encoded T2. | | | |
| upgradeContent | 1.1.0 | | Snapshot of upgrade data present on the supply. REVIEW: Check if still needed. Stil exist? | | | |
| deploymentType | 1.1.0 | | Device determined deployment data. string enum: "setup", "starter", "trade", "unknown" | | ?? New? | |
| warrantyStatus | 1.1.0 | | 1.1 inWarranty, outOfWarrantyLiters, outOfWarrantyTime, outOfWarranty3rdParty. Requested by LFP, Not vetted | | New | ICartrdigeSnapshot::isUnderWarranty ICartrdigeSnapshot::getEndOfWarrantyDate REVIEW: Missing the Liters Warranty and 3rdParty |
| warrantyStatus | 1.4.0 | | "inWarranty", "almostOutOfWarranty", "outOfWarranty", "seeWarrantyNotes" | | | |
| warrantyEndDate | 1.4.0 | | warrantyExpireDate | | | |
| glDetected | 1.12.0-alpha.1 | | indicates whether this supply was detected in one of the graylist(s). See definitions at Supply GrayList Data Format and API (HP Only) | | | |

### lifeInfo Properties

The wiki provides details on the fields required in the schema. Because this schema is shared between many supplies, the data required for each supply type varies.

The Data Requirement Document provides details on data requirements.

| Property (new in) Version | Schema Required | Description | Schema Dependencies | OCV Required | Sirius 1.3 Compare | Dune PEI |
|---|---|---|---|---|---|---|
| levelState | 1.0.0 | Yes | "ok", "low", "veryLow", "veryVeryLow", "depleted", "fulfillment", "unknown" | type defined in Supply Shared Types | | Renamed, same definition as measuredQuanityState | ICartrdigeSnapshot::getState() / ICartrdige Snapshot::getStatus |
| percentLifeDisplay | 1.0.0 | no | Represents the user view (gas gauge display). Decrements by 10 percent increments. Note: Same property exposed in the public /cmd/supply/v1/supplies resource data model. | type defined in Supply Shared Types | | New | ICartridgeSnapshot::getReportedLevelPercentage |
| percentLifeRemaining | 1.0.0 | Yes | Detailed PLR decrements by 1 percent increments | type defined in Supply Shared Types | Y | 1.3 has consumablePercentageLevelRemaining rename because "level" implies a volume. For example, fuser would be using "cyles" for its life count unit making "level" very odd. | ICartridgeSnapshot::getLevelPercentage |
| lifeInfo | 1.0.0 | Yes | Composite type. lifeCount - incrementing life count of the applicable unit, lifeExpected - expected life count of the applicable unit, lifeUnit - unit used to define lifeCount and lifeExpected, - type CounterUnit. Justification: For telemetry, we have loss of data when relying on percent life remaining. For suppy's that do not have level sensors, the device usual calculates the percentLifeRemaining from underlying counts. We want the raw values, not processed values. percentLife can go negative with extended life which creates loss of data because a percentage stops at 0. This creates havoc with life tracking services. If a supply is used beyond the lifeExpected, we can see the lifeCount continue to increment, not masking information. The combination of lifeCount and lifeExpected can be use to calculate a percent life by the client if needed. | type defined in Supply Shared Types | Y? because percentLifeRemaing decrement granularity can vary? and needed for non-marking agent supplies. e.g. fuser. | New | REVIEWED: Can be obtained as described ICartridgeSnapshot::getCapacity() That returns the total capacity of the supply and the ICartridgeSnapShot::getLevel() the current remaining level. I guess the lifeCount can be obtained from the substraction. The units are in the Capacity class. |
| approximatePagesRemaining | 1.0.0 | no | Rename of estimatedPagesRemaining | | | | ICartridgeSnapshot::getLevel when it supports remaining pages |

### deviceInfo

The wiki provides details on the fields required in the schema. Because this schema is shared between many supplies, the data required for each supply type varies.

The Data Requirement Document provides details on data requirements.

| Property (new in) Version | Schema Required | Description | Schema dependencies | Sirius 1.3 Compare | Dune PEI |
|---|---|---|---|---|---|
| printerRegion | 1.0.0 | | ?? ink - printer region, for laser - printer zone (not the etag region value) | | Same | ICartridgeSnapshot::getRegion But it is the region of the supply, not the printer. Not sure if same intent than the property. |
| previousPrinterRegion | 1.0.0 | | ?? ink - previous printer region, for laser - previous printer zone (not the etag region value | | Same | |
| printerRegionalizedCount | 1.0.0 | no | Count of the number of times the printer region has been changed. Only a limited number of times are allowed | | Same | |
| isAntiTheftConfiguration | 1.0.0 | no | "printer", "fleet", "off" | | Same | setSupplySettingValue with ANTI_THEFT |
| genuineHpSuppliesOnly | 1.0.0 | no | Clarify definition If this is a device setting to only accept HP genuine, then move to deviceInfo? | type defined in Glossary | Same | REVIEW |
| storeSupplyUsageData | 1.0.0 | | Clarify definition. true or false value indicating consent from the user? Move to device setting. That's a configuration bit in the telemetry that says whether the customer has allowed storing usage data in the cartridge. (Data like cartridge page counters, usage by media size, etc). | type defined in Glossary | Same | REVIEW |
| veryLowStateAction | 1.0.0 | | The behavior of the device when the veryLow levelState is triggered. Stop, warn and continue. AI: Move to deviceInfo | | Same | setSupplySettingValue with VERY_LOW |
| stId | 1.0.0 | no | The gauss id encoded on the printer | | Same | ICartridges::getGaussIdEncoder() REVIEWED: ICartridges updated ( revert to RED if disconform, if ok, remove this line ) DUNE-16848 |
| engineCycleCount | 1.0.0 | | REVIEW: Description | | New | |
| integrityStatus | 1.11.0 | | Information regarding recent supplies security events, specifically related to Yellow Blobs encrypted scripts. Sub-fields are: activeKeyIds (array of up to 10 hashes of most recently discovered keys), activeBlobs (array of up to 10 ID values of recently executed scripts (blobs)), alertingBlobs (array of up to 10 ID values of active blobs which rejected a supply recently). | | New | |
| glStaticUuid | 1.12.0-alpha.1 | | The UUID of the static graylist. See definitions at Supply GrayList Data Format and API (HP Only) | | | |
| glStaticErrorReasons | 1.12.0-alpha.1 | | The error reasons for why the graylist was rejected | | | |

### serviceInfo

The wiki provides details on the fields required in the schema. Because this schema is shared between many supplies, the data required for each supply type varies.

The Data Requirement Document provides details on data requirements.

| Property (new in) Version | Required | Description | Sirius 1.3 Compare | Dune PEI |
|---|---|---|---|---|
| supplyModelType | 1.0.0 | | definition from com.hp.cdm.service.rtp.version.1.resource.supply.schema.json#/definitions/supplyModelType | | |
| supplyModelIds | 1.0.0 | | definition from com.hp.cdm.service.rtp.version.1.resource.supply.schema.json#/definitions/supplyModelType | | |
| incrementBizlogicCount | 1.0.0 | | defined from com.hp.cdm.domain.glossary.version.1.schema.json#/definitions/featureEnabled | | |
| serviceIssuer | 1.0.0 | | Business Model describing the supply service used: instantInk, instantToner, aRS | | |

### previousSupplyInfo

The wiki provides details on the fields required in the schema. Because this schema is shared between many supplies, the data required for each supply type varies.

The Data Requirement Document provides details on data requirements.

| Property (new in) Version | Required | Description | Schema dependencies | Sirius 1.3 Compare | Dune PEI |
|---|---|---|---|---|---|
| supplyUniqueId | | | enable referencing the previous supply data | type defined in Supply Shared Types | rename of conumableUniqueId | Same property than in IdentityInfo |
| percentLifeDisplay | | | Represents the user view (gas gauge display). Decrements by 10 percent increments. Note: Same property exposed in the public /cmd/supply/v1/supplies resource data model. | type defined in Supply Shared Types | | |
| percentLifeRemaining | | | critical data that may have changed since the last supply record | type defined in Supply Shared Types | rename of percentageLevelRemaining | Same property than in supplyLife |
| lastUsedDateTime | | | critical data that may have changed since the last supply record | | renamed LastUdateDate | REVIEW |
| lifeCount | | | critical data that may have changed since the last supply record | type defined in Supply Shared Types | New | Same property than in supplyLife |
| compositeCounts.order | 1.1.0 | | The order of the composite ink. Values: CYM, CMY, YCM, YMC, MCY, MYC | | | |
| compositeCounts.c | 1.1.0 | | lifeCount | | | |
| compositeCounts.m | 1.1.0 | | lifeCount | | | |
| compositeCounts.y | 1.1.0 | | lifeCount | | | |

## Notification Triggers

| Category | New in version | Definition | Dune PEI |
|---|---|---|---|
| supplyStateChange | 1.0 | Informs the client that a property value has changed in the stateInfo object. | CartridgeStateChangeEvent |
| supplyLevelChange | 1.0 | Informs the client that the lifeInfo.levelState property value has changed. | LevelChangeEvent |
| supplyChangeDetected | 1.0 | Informs the client when the device has detected a supply new to the device (identity differs from previous supply in the supply slot). Evaluation of the supply usually performed after the supply door is closed. | StatusChangeEvent It includes any change in the Slot |
| supplyReplaced | 1.0 | Provides a complete snapshot of the replaced supply information. All information included in the snapshot must reflect the information that was valid for the supply when it was originally inserted, including fields like supplyInsertionCount. This notification trigger is always paired with supplyDetection event when a new supply is detected and previous supply information is available. | StatusChangeEvent It includes any change in the Slot |
| supplySameDetected (1.1) | 1.1 | Printer evaluated the supply after cover was closed and determined the supply had the same supplyUniqueId as before the door was opened. | |
| timedInterval (1.1) | 1.1 | Snap shot of the current supply supply ticket, one event per life tracked supplyType. | N/A Could be implemented at CDM layer. |
| supplyInsertion (1.1) | 1.1 | If the device electronically supports the "supplyRemoval" event, this event would also be supported. Informs the client that a supply has been installed with the door open. The intended use case is to track removal and insertion events with the door open for products with the capability. | REVIEW |
| supplyRemoval (1.1) | 1.1 | If the device can electronically detect removal with the supply door open. Send an event that the supply was removed. Encourage minimal data, IdentityData, plus just what's needed. | StatusChangeEvent It includes any change in the Slot |
| tankFillDected(1.1) | 1.1 | TBD | |

## Fleet Common Supply JSON Schema

### Schema Versions

Schema Registry Login

| Version | Schema File | Description |
|---|---|---|
| 1.0.0 | https://schemaregistry.cso-hp.com/cdm/gun/com.hp.cdm.service.eventing.resource.eventDetail.type.supply.version.1?pp=1&version=1.0.0 | fleet version 1.0.0 |
| 1.1.0 | https://schemaregistry.cso-hp.com/cdm/gun/com.hp.cdm.service.eventing.resource.eventDetail.type.supply.version.1?pp=1&version=1.1.0 | fleet version 1.1.0 |
| 1.2.0-alpha.1 | https://schemaregistry.cso-hp.com/cdm/gun/com.hp.cdm.service.eventing.resource.eventDetail.type.supply.version.1?pp=1&version=1.2.0-alpha.1 | fleet version 1.2.0-alpha.1 |
| 1.2.0-alpha.2 | https://schemaregistry.cso-hp.com/cdm/gun/com.hp.cdm.service.eventing.resource.eventDetail.type.supply.version.1?pp=1&version=1.2.0-alpha.2 | fleet version 1.2.0-alpha.2 |
| 1.2.0 | https://schemaregistry.cso-hp.com/cdm/gun/com.hp.cdm.service.eventing.resource.eventDetail.type.supply.version.1?pp=1&version=1.2.0 | fleet version 1.2.0 |
| 1.3.0 | https://schemaregistry.cso-hp.com/cdm/gun/com.hp.cdm.service.eventing.resource.eventDetail.type.supply.version.1?pp=1&version=1.3.0 | fleet version 1.3.0 |
| 1.3.1-alpha.4 | https://schemaregistry.cso-hp.com/cdm/gun/com.hp.cdm.service.eventing.resource.eventDetail.type.supply.version.1?pp=1&version=1.3.1-alpha.4 | added support for large format and toner |
| 1.4.0-beta.1 | https://schemaregistry.cso-hp.com/cdm/gun/com.hp.cdm.service.eventing.resource.eventDetail.type.supply.version.1?pp=1&version=1.4.0-beta.1 | added support for large format and toner |
| 1.5.0 | https://schemaregistry.cso-hp.com/cdm/gun/com.hp.cdm.service.eventing.resource.eventDetail.type.supply.version.1?pp=1&version=1.5.0 | alpha.2: add subsection "aa"containing the grayList and remote challenge information |
| 1.6.0-alpha.2 | https://schemaregistry.cso-hp.com/cdm/gun/com.hp.cdm.service.eventing.resource.eventDetail.type.supply.version.1?pp=1&version=1.6.0-alpha.2 | add serviceCode and supplyDescription in identityInfo to support preventiveMaintenanceKit supply type |

If Schema Registry returns an authentication error, please login first: see button above!

### Implementation Notes

#### Example Supply Event Notification Sequence (without supplyRemoval support)

- supplyChangeDetected - Initial boot, first time the fw evaluates initial set of supplies. One event per supplyType. Note: previousSupplyInfo will be missing since there is no previous supply at his point.
- timedInterval – pushing a supply snapshot once a day
- timedInternal – pushing a supply snapshot once a day
- supplyLevelChange – The level state has changed value, let's say from ok to low.
- timedInterval
- …
- supplyStateChange - Data in the supplyStateInfo has changed. User removed the supply and closed the door and we're getting a stateInfo.supplyState = error and a stateInfo.stateReasons = [missingError].
- supplyStateChange – Data in the supplyStateInfo has changed. User put the same supply back in and closed the door, now the stateInfo.supplyState = ok and the stateReasons is now an empty array
- timeInterval
- …
- supplyLevelChange – The level state has change value, let's say from low to depleted.
- supplyChangeDetected – The user just changed the supply and closed the door. FW see's the new supply. Note previousSupplyInfo now has data.
- supplyReplaced – Should see one of these for every supplyChangeDetected trigger when there is previous supply data, so we send a snapshot of complete previous replaced supply information.
- timedInterval
- timedInerval
- etc. an so on.

#### Example Supply Event Notification Sequence (with supplyRemoval support)

- supplyChangeDetected - Initial boot, first time the fw evaluates initial set of supplies. One event per supplyType. Note: previousSupplyInfo will be missing since there is no previous supply at his point.
- timedInterval – pushing a supply snapshot once a day
- timedInternal – pushing a supply snapshot once a day
- supplyLevelChange – The level state has changed value, let's say from ok to low.
- timedInterval
- …
- supplyRemoval - Can see when the user removes the supply with the access door open.
- supplyStateChange -User removed the supply and closed the door. supplyStateInfo as changed; stateInfo.supplyState = error and a stateInfo.stateReasons = [missingError].
- supplyReinserted - Can see when the user reinserted the supply with the access open. Put the same supply back in.
- supplyStateChange – Data in the supplyStateInfo has changed. The user put the same supply back in and closed the door, now the stateInfo.supplyState = ok and the stateReasons is now an empty array
- timeInterval
- …
- supplyLevelChange – The level state has change value, let's say from low to depleted.
- supplyRemoval - Can see when the user removes the supply with the access door open. Note: No supplyReinserte notificaiton because it's not the same supply.
- supplyChangeDetected – The user just changed the supply and closed the door. FW see's the new supply. Note previousSupplyInfo now has data.
- supplyReplaced – Should see one of these for every supplyChangeDetected trigger when there is previous supply data, so we send a snapshot of complete previous replaced supply information.
- timedInterval
- timedInerval
- etc. an so on.

#### Example Supply Event with supplyState: "unknown"

1. supplyState is set to 'unknown' when:
  - i.cartridge door is opened
  - ii.engine booting up

2. This is for suppliesPublic & Private CDM resources, and not applicable to supply telemetry

3. Example:
  - i) User open cartridge door, no telemetry event will be published
  - ii)User close cartridge door without replace any supply, telemetry with 'supplySameDetected' notification trigger will be published.