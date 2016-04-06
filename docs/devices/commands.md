# Device Commands

Device commands allow you to instruct your device to take some kind of action. Commands include a name and an optional payload. It's then up to the device's firmware to take the appropriate action based on the command and payload.

![Command Diagram](/images/devices/command-diagram.png "Command Diagram")

## Sending Commands

Commands are typically invoked from Losant workflows. Another common way to invoke commands is using the Losant API from a custom interface like a mobile app. For example, a thermostat may have a companion mobile app that allows the user to remotely set the temperature. The developer would then send a command over the Losant REST API to set the temperature. The device will then receive the command and take the appropriate action, which is likely to turn on or off the furnace or air conditioner.

Losant workflows provide a way to easily send commands to devices based on any number of triggers. The example below will send a command to a thermostat to disable "away" mode when a person is detected by a separate smoke detector device that has a motion sensor.

![Away Mode Workflow](/images/devices/away-mode-workflow.png "Away Mode Workflow")

In the above example, the smoke detector is reporting state whenever motion is detected or not. The condition node checks that motion is detected. The condition might look something like `{{ data.motion }} == true`. If motion is detected, it then sends a command to the thermostat to disable its "away" mode. The command name is `set-away` and the payload is `{ "away" : false }`.

Command names and payloads can be anything. It's entirely up the device and its firmware for what commands will be supported.


## Handling Commands

Commands can currently only be received over an [MQTT connection](/mqtt/overview) to Losant. The Losant SDKs make connecting and receiving commands very easy for custom devices. All commands contain a name and an optional payload. All payloads are JSON objects.

Below is an example of using the Losant Arduino SDK to handle a command and turn on an LED.

```arduino
// Called whenever the device receives a command from the Losant platform.
void handleCommand(LosantCommand *command) {
  Serial.print("Command received: ");
  Serial.println(command->name);

  if(strcmp(command->name, "turn-on-led") == 0) {
    digitalWrite(LED_PIN, 1);
  }
}

LosantDevice device("my-device-id");
device.connectSecure(wifiClient, "my-access-key", "my-access-secret");

// Subscribe to commands.
device.onCommand(&handleCommand);
```
