description: Learn about the latest version of the Losant Edge Agent and what's changed over time.

# Edge Agent Changelog

This file represents all changes to the `losant-edge-agent` since it's initial release. This project adheres to [Semantic Versioning](http://semver.org/spec/v2.0.0.html).

<!--
The format is based on [Keep a Changelog](http://keepachangelog.com/en/1.0.0/).
-->

***

## 1.2.2 - 2018-08-22

### Added <a name="1.2.2-added"></a>

- Added a configuration flag to control the queuing of messages while the agent is offline.
- Added the new payload helper [`scaleLinear`](/workflows/accessing-payload-data/#format-helpers).
- Added the new payload helper [`currentDateTime`](/workflows/accessing-payload-data/#format-helpers).

### Changed <a name="1.2.2-changed"></a>

- Improved [Google Big Query](/workflows/data/google-big-query/) and [GoogleML Node](/workflows/data/google-ml/) error handling.
- Clarified certain verbose log messages.

***

## 1.2.1 - 2018-08-07

### Added <a name="1.2.1-added"></a>

- Can now choose to have no expiration time for the [JWT: Create Node](/workflows/logic/jwt-create/).

### Changed <a name="1.2.1-changed"></a>

- [Modbus: Read Node](/workflows/data/modbus-read/) and [Modbus: Write Node](/workflows/data/modbus-write/) now default to port 502.
- Improved [MongoDB Node](/workflows/data/mongo/) error handling.
- A workflow publishing MQTT messages to an invalid or unauthorized topic will no longer cause the agent to disconnect from the Losant Platform.

### Fixed <a name="1.2.1-fixed"></a>

- System clock changes no longer affect the firing of interval timers while the agent is running.
- Debug messages with circular references correctly send to the Losant Platform.

***

## 1.2.0 - 2018-06-21

### Added <a name="1.2.0-added"></a>

- Data / [ServiceNow Node](/workflows/data/service-now/)
- Triggers / [UDP Trigger](/workflows/triggers/udp/)
- Outputs / [UDP Send Node](/workflows/outputs/udp-send/)
- Edge workflow payloads now have environment variables available under the field `agentEnvironment`.
- Edge workflow payloads now have the field `isConnectedToLosant`, representing if the agent is currently connected to Losant.

### Changed <a name="1.2.0-changed"></a>

- Easily set authorization headers for requests on the [HTTP Node](/workflows/data/http/).
- Can now set the path for a cookie on the [HTTP Response Node](/workflows/outputs/http-response/).
- Improved phone number casting for the [Twilio Node](/workflows/outputs/twilio/).
- Update to Node.js 8.11.3.

***

## 1.1.1 - 2018-05-21

### Changed <a name="1.1.1-changed"></a>

- Improved startup messages.
- The [HTTP Node](/workflows/data/http/) now allows for setting timeouts and capturing network errors.

### Fixed <a name="1.1.1-fixed"></a>

- Improved messages for [Slack Node](/workflows/output/slack/) errors.
- Support circular references in debug messages.

***

## 1.1.0 - 2018-03-29

### Added <a name="1.1.0-added"></a>

- Logic / [Generate ID Node](/workflows/logic/generate-id/)
- Logic / [Hash Node](/workflows/logic/hash/)

### Changed <a name="1.1.0-changed"></a>

- Improved error messages
- The [Validate Payload Node](/workflows/logic/validate-payload/) now allows for defining your schema using either a [payload path](/workflows/accessing-payload-data/#payload-paths) or a [JSON template](/workflows/accessing-payload-data/#json-templates).

### Fixed <a name="1.1.0-fixed"></a>

- [Modbus: Read Node's](/workflows/data/modbus-read/) "Length" property now defaults to a value of 1 if left blank.
- [Modbus: Read](/workflows/data/modbus-read/) and [Modbus: Write](/workflows/data/modbus-write/) Nodes will now time out if they fail to connect to Modbus.

***

## 1.0.0 - 2018-03-08

### Added <a name="1.0.0-added"></a>

- Triggers / [Timer Trigger](/workflows/triggers/timer/)
- Triggers / [HTTP Request Trigger](/workflows/triggers/request/)
- Triggers / [MQTT Trigger](/workflows/triggers/mqtt/)
- Triggers / [Device: Command Trigger](/workflows/triggers/device-command/)
- Data / [Modbus: Read Node](/workflows/data/modbus-read/)
- Data / [Modbus: Write Node](/workflows/data/modbus-write/)
- Data / [File: Read Node](/workflows/data/file-read/)
- Data / [File: Write Node](/workflows/data/file-write/)
- Data / [Run Executable Node](/workflows/data/run-executable/)
- Outputs / [HTTP Response Node](/workflows/outputs/http-response/)
