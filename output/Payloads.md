Source tag : https://rndwiki.inc.hpicorp.net/confluence/spaces/DataOS/pages/1800510075/Payloads

Note : This extracted file is generated from SharePoint or Wiki content. If the source document contains images, charts, or graphical elements, they may not be fully converted into Markdown format. For complete clarity, please refer to the original source using the source tag provided above.

# Payloads

Payloads are important json files that contain telemetry information useful for devs to triage errors. When reporting an issue it's good practice to a payload sample of both the error and what the data should be behaving like.

Finding Payloads (less than seven days old and the data contains an eventDetailError):

This can be found in databricks and Opensearch. It is easier to find valid payloads in databricks then Opensearch since you can filter through the payloads in databricks.

Databricks payload can be found in rawjson field

eventDetailErrors allow the rawjson field to populate, if there's no error in that field then you will need to get the payloadId and find the data in Opensearch. Using that value you can find the payload you need in Opensearch if the data is less than 6 days old.

Opensearch payload can be found by expanding the event and clicking on JSON.

payloads in databricks are located in the rawjson field and are only present if there's an error in the data.

Finding Payloads (if the above method fails):

If the above method isn't working for you then you should always be able to build a payload using this tool. Please note that this method should be used as a last resort and ONLY if the data of a specific event is needed.

When rawJson field is empty we must put the data together piece by piece to build the payload.

We are needing the event, originator, privacy, and originatorContext. We must build the necessary dataframes whilst joining them together with the desired pieces

This workbook is not currently functional as it is from an older piece of architecture, however the theory still stands.

if a telemetry event has an error, whichever piece had that error won't be populated

- eventDetailError would block out event
- originatorDetailError would block out originator
- etc..

The only way to piece it together full at that point is access to the error tables which very few people have access to.

Prepping Payloads:

- Copy and paste data into text editor
- Reformat JSON data so all data is indented properly and can be read easily by all future readers.
- Save file with error description and whether it's an example of the error or an example of how the data should be working.

Example: Euthenia Schema Error Example | Euthenia Schema As Expected Example

How to determine a Payload is Valid?

Payload (rawJson) should contain the following:

- Attributes = $..
- Payload must have an eventDetail
- Payload must have an originator
- filterType = inclusion

In this image the attributes section is correct, but the filterType is incorrect.

"event":
"dateTime":
"eventCategory":
"eventDetailType":
"filter":
"attributes":
"FilterId":
"filterType":
"resourceId":
"filterError":