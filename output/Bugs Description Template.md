Source tag : https://rndwiki.inc.hpicorp.net/confluence/spaces/DataOS/pages/1739460560/Bugs+Description+Template

Note : This extracted file is generated from SharePoint or Wiki content. If the source document contains images, charts, or graphical elements, they may not be fully converted into Markdown format. For complete clarity, please refer to the original source using the source tag provided above.

# Bugs : Description Template

1. Brief summary of Issue : The description should be clear and well defined. If the issue is schema validation based it should provide an explanation behind the errors meaning. The ticket should also mention the specific error that is being experienced, this way fixes for the error can be better tested. If no specifics are provided then we cannot expect the developers to be able to fix the issue.

   - Bad: Schema validation errors for U/S devices in Stage
   - Good: Schema validation errors (Error: dateTime 'xxx' is not a valid input) for U/S devices in Stage. This error means we are receiving an incorrect input of 'xxx' when we should be receiving "2012-04-23T18:25:43.511Z"

2. Environment: list of environments issue is present in

3. originator gun: "com.hp.cdm.domain.telemetry.type.originatorDetail.originator.imagingDevice.version.1"

4. event gun: "com.hp.cdm.service.eventing.resource.eventDetail.type.supply.version.1"

5. Applicable products/devices affected by issue: list of products/devices/product families affected by the issue

6. fwVersions: list of fwVersions affected by the issues

7. Attachments:

   - Payload of Issue: This should be attached as a document, but a note should be applied in the description field stating it has been attached to the ticket for reference. This should contain a VALID payload if possible. If not possible then state no valid payload available on the ticket.
   - Payload of Good Data: Same as above but it should be an example of how the data should work.
   - Conversations (Email Threads, Discussions with fwContacts, Etc)

8. Results: This should showcase the reproducibility % of the issue in comparison to normal events for the current and past months in the environments the issue is located in. Ideally it should also breakdown the fwVersions and devices affected by the issue. The data for this should be the current month as well as the month previous so a possible trend can be identified.

   - Rate of Occurrence for the errors in the past 30 days.
   - Rate of Occurrence for the errors in the past 30 days before the above result.
   - Analysis of both months determining if the errors are getting worse or better.

Source: This template was built, consulting various leads across multiple fw teams.

Example