description: Applications are the basic scoping mechanism within the Losant platform. Learn more about creating and managing applications.

# Applications

All [devices](/devices/overview/) and [workflows](/workflows/overview/) belong to a single application. Users can have multiple applications as needed. [Dashboards](/dashboards/overview/) do not belong to an application since a single dashboard can contain graphs and blocks for several different applications.

## Creating Applications

There are a few places within the platform from which an application can be created; or, applications can be created at any time using the main `Applications` menu.

![Create Application](/images/applications/create-application.png "Create Application")

When creating an application, you will be asked for three pieces of information:

* **Application Name:** You are required to name your new application. The name can be changed at any time.
* **Description:** Optionally, you may also provide a more detailed description of the application.
* **Owner:** The application must be scoped to your personal [Sandbox](/user-accounts/sandbox/) or to an [organization](/organizations/overview/) for which you have the [Editor role](/organizations/members/#member-roles). The owner can be changed at a later date only if you have Administrator permissions for the parent organization (or Sandbox).

![Create Application Form](/images/applications/create-application-form.png "Create Application Form")

## Deleting Applications

Applications can be deleted on the settings page. Deleting an application cannot be undone. All devices, device data, workflows, and device recipes owned by this application will be permanently removed.

![Delete Application](/images/applications/delete-application.png "Delete Application")

## Communication Log

The Communication Log is a real-time log that displays helpful information about various aspects of your Losant application. It's most useful for debugging purposes.

![Communication Log](/images/applications/communication-log-full.png "Communication Log")

As a real-time tool, the Communication Log will always begin in an empty state. Logs will appear as actions on your application take place. Logs will show for the following cases:

### MQTT

* MQTT Authentication - A log will appear when an [MQTT client](/mqtt/overview/) successfully connects or fails to connect to the [Losant MQTT broker](/mqtt/overview/).
* Raw MQTT Messages - MQTT Messages sent or received by the [Losant MQTT broker](/mqtt/overview/) will appear in the log.

### Device

* Device State - When [devices](/devices/overview/) report [state](/devices/state/), a log will appear.
* Device Commands - When Losant [sends a device command](/devices/commands/), a log will appear.
* Device Connection Status - When [devices](/devices/overview/) successfully connect or disconnect from Losant, a log will appear.

### Webhooks

* Webhooks - When a [Webhook](/applications/webhooks/) is triggered, a log will appear.
* Webhook Replies - When [Losant](/workflows/outputs/webhook-reply/) [replies to a Webhook](/applications/webhooks/#custom-replies), a log will appear.

### Endpoints

* Endpoint - When a request is made to a Losant [Experience Endpoint](/experiences/endpoints/), a log will appear.
* Endpoint Reply - When [Losant replies](/workflows/outputs/endpoint-reply/) to an [Experience Endpoint](/experiences/endpoints/), a log will appear.

### Integrations

* Integration Messages - When Losant receives a message from an [Integration](/applications/integrations/), a log will appear.

## Application Globals

![Application Globals](/images/applications/application-globals.png "Application Globals")

Application globals are a set of key/value pairs that are accessible inside of any workflow in the current application. This is a great place to store application-wide configuration that is used across multiple workflows, like phone numbers or API keys. Any values configured here are accessible under the globals object on the payload in a workflow run. Application globals can be overridden within a workflow by defining a different value at the same key in the globals for that specific workflow. You can read more about workflow globals [here](/workflows/overview/#workflow-globals).

## Application Archive

![Application Archive](/images/applications/application-archive.png "Application Archive")

Application archive is a way to backup an application's devices data on either Amazon S3 or Google Cloud Storage. The archive configuration allows you to specify which devices data should be backed up. After the devices data becomes older than 30 days, the application will create a directory that is the date of the data (31 days ago) and a CSV per device within that directory. Those CSV files will be named by the applicationId, deviceId, and the start and end time of the data contained in the file. In order to configure archiving for AWS, `Bucket`, `Region`, `Access Key ID` and `Secret Access Key` are required. In order to configure archiving from Google Cloud Storage, `Bucket`, `Project ID`, and `Account Key (JSON)` are required. Both have one optional field, `Directory Inside the Bucket`, which specifies a directory for archivals to go, if the files should not be appended to the top level directory.
