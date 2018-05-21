description: Learn about the latest version of the Losant Edge Agent and what's changed over time.

# Edge Agent Changelog

This file represents all changes to the `losant-edge-agent` since it's initial release. This project adheres to [Semantic Versioning](http://semver.org/spec/v2.0.0.html).

<!--
The format is based on [Keep a Changelog](http://keepachangelog.com/en/1.0.0/).
-->

***

## 1.1.1 - 2018-05-21

### Changed

- Improved startup messages.
- The [HTTP Node](/workflows/data/http/) now allows for setting timeouts and capturing network errors.

### Fixed

- Improved messages for [Slack Node](/workflows/output/slack/) errors.
- Support circular references in debug messages.

___

## 1.1.0 - 2018-03-29

### Added

- Logic / [Generate ID Node](/workflows/logic/generate-id/)
- Logic / [Hash Node](/workflows/logic/hash/)

### Changed

- Improved error messages
- The [Validate Payload Node](/workflows/logic/validate-payload/) now allows for defining your schema using either a [payload path](/workflows/accessing-payload-data/#payload-paths) or a [JSON template](/workflows/accessing-payload-data/#json-templates).

### Fixed

- [Modbus: Read Node's](/workflows/data/modbus-read/) "Length" property now defaults to a value of 1 if left blank.
- [Modbus: Read](/workflows/data/modbus-read/) and [Modbus: Write](/workflows/data/modbus-write/) Nodes will now time out if they fail to connect to Modbus.

___

## 1.0.0 - 2018-03-08

### Added

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
