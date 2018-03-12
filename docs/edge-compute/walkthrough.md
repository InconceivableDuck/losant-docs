# Edge Compute Walkthrough

This guide provides a complete walkthrough for using [Losant Edge Compute](/edge-compute/overview/) to read data from a piece of industrial equipment using Modbus and then report that data to the cloud.

// Diagram

This system is made up of a kegerator with a <a href="https://www.bannerengineering.com/us/en/products/wireless-sensor-networks/wireless-sensors/m12f-temperature-and-humidity-sensors-wireless.html#all" target="_blank">Banner Temperature &amp; Humidity Sensor</a> installed inside it, a <a href="https://www.bannerengineering.com/us/en/products/wireless-sensor-networks/wireless-controllers/industrial-wireless-controller-dxm-series.html#all" target="_blank">Banner Wireless Controller</a>  and a Raspberry Pi as the Edge Compute device. The Banner Wireless Controller reads sensor data from any number of remote sensors and then exposes that information to your local network over Modbus TCP. The Edge Compute device can then read that Modbus endpoint and report the data to the cloud. Banner is just an example used for this walkthough. The same lessons apply to any Modbus TCP capable devices you may have.



## Register the Devices

[Edge Compute device types](/devices/edge-compute/) can report state for themselves or for any number of Peripheral devices. This examples includes one peripheral, which is the kegerator itself, and one edge compute device to read Modbus data that the kegerator is producing.

With this setup, we'll need to create two devices within Losant. One Edge Compute device and one Peripheral device. Using the `Devices -> Add Device` main application menu, first create the Edge Compute device.

![Add Device Menu](/images/edge-compute/walkthrough/add-device.png "Add Device Menu")

![Edge Compute Device](/images/edge-compute/walkthrough/edge-compute-device.png "Edge Compute Device")

In this example, the device is named "Raspberry Pi Gateway", however you can name it anything you'd like. The only other required setting is to make the device type `Edge Compute`. This device doesn't need any attributes because the actual temperature and humidity information will be added to our peripheral device. Click the `Create Device` button to add this new device to your application.

Next, create a second device for the Kegerator itself.

![Peripheral Device](/images/edge-compute/walkthrough/peripheral-device.png "Peripheral Device")

This example named the device "Kegerator", but you can name it anything you'd like. Set the device type `Peripheral` and set the gateway to our previously created Edge Compute device. This is primarily an access control setting, which restricts which gateways are allowed to report state on behalf of this peripheral. Lastly, add the two attributes for temperature and humidity. When done, click the `Create Device` button to add this device to your application.

## Create Access Key and Secret

In order for the Raspberry Pi to communicate with Losant, it requires authentication details. Using the main `Security` application menu, create a new access key and secret for this device.

![Security Menu](/images/edge-compute/walkthrough/security-menu.png "Security Menu")

![Add Access Key](/images/edge-compute/walkthrough/add-access-key.png "Add Access Key")

![Access Key Settings](/images/edge-compute/walkthrough/access-key-settings.png "Access Key Settings")

We always recommend creating a dedicated access key for each device. With that said, select the `Restricted To Specific Devices` radio and choose your previously created Edge Compute device.

After clicking `Create Access Key`, you'll be presented with a popup with your newly created access key and secret. Losant does not store the secret, so it's **very important to copy/paste this somewhere safe**. You'll be using these details in the next step.

![Access Key and Secret](/images/edge-compute/walkthrough/access-key-secret.png "Access Key and Secret")

## Install Losant Edge Agent

Losant Edge Compute works by deploying [Edge Workflows](/workflows/edge-workflows/) to your devices. In order to receive, process, and manage these workflows on the device, the Edge Agent must be installed.

Follow the [Edge Agent Installation Guide](/edge-compute/edge-agent-installation/) for step-by-step instructions.

## Configure and Run the Edge Agent

Once the Losant Edge Agent is installed, you can now run it with the access key and secret you created earlier. There are two ways to [configure the edge agent](/edge-compute/edge-agent-usage/). You can either use a configuration file or use environment variables. Generally we recommend environment viarables.

The edge agent also stores data locally, so it's recommended to create a local folder and mount it inside the docker container when you run it. This way the data is persisted between restarts of the container.

```console
sudo mkdir -p /var/lib/losant-edge-agent/data
sudo chmod a+rwx -R /var/lib/losant-edge-agent
```

These commands will create a data folder at `/var/lib/losant-edge-agent/data` and set the required permissions. You will only ever have to run these commands once. 

You can now run the edge agent by mounting in this data folder and providing the edge compute device ID and authentication information using environment variables.

```console
docker run -d --restart always \
  --name losant-edge-agent \
  -e 'DEVICE_ID=<edge-device-id>' \
  -e 'ACCESS_KEY=<your-access-key>' \
  -e 'ACCESS_SECRET=<your-access-secret>' \
  -v /var/lib/losant-edge-agent/data:/data \
  losant/edge-agent
```

If you open the edge compute device page prior to running this command, you'll see it log some connection information when the agent is started.

![Edge Agent Connection](/images/edge-compute/walkthrough/edge-agent-connection.png "Edge Agent Connection")

If nothing shows in the device log when the agent is started, try inspecting the logs locally using the command below.

```console
docker logs losant-edge-agent
```

You should see output similar to the image below. If there are any errors, they will be displayed and should provide helpful information to debug any issues.

![Docker Logs](/images/edge-compute/walkthrough/docker-logs.png "Docker Logs")

## Build the Workflow

Now that you have a Losant Edge Agent installed and running, you can build and deploy an Edge Workflow to it to start reading Modbus information.

You can create an Edge Workflow by clicking the `Workflows -> Create Workflow` main application menu.

![Create Workflow Menu](/images/edge-compute/walkthrough/create-workflow-menu.png "Create Workflow Menu")

![Create Edge Workflow](/images/edge-compute/walkthrough/create-edge-workflow.png "Create Edge Workflow")

![Edge Agent Version](/images/edge-compute/walkthrough/edge-agent-version.png "Edge Agent Version")

It's important to ensure the version you select for `Minimum Agent Version` is the same or below whatever you have installed on your edge devices. Losant continually updates the edge agent with new capabilities, however your devices may not be updated to support the new features.

Once you click `Create Workflow`, you'll be presented with a blank edge workflow canvas.

![Blank Edge Workflow](/images/edge-compute/walkthrough/blank-edge-workflow.png "Blank Edge Workflow")

The workflow you'll create in this example will read two Modbus registers every minute, convert them from raw data to actual measurements, and then report that data to Losant's cloud.

Start by first dragging a [Timer Node](/workflows/triggers/timer/), a [Modbus Read Node](/workflows/data/modbus-read/), and a [Debug Node](/workflows/outputs/debug/) onto the canvas. Connect each node together and then configure the Modbus Node to read your specific Modbus endpoint. The configuration below is for our Banner Wireless Controller, which is reading the temperature sensor in the kegerator.

![Modbus Node Configuration](/images/edge-compute/walkthrough/modbus-node-config.png "Modbus Node Configuration")

The Modbus Read Node has three primary configuration sections. The first is the endpoint itself, which on our network is located at the address `192.168.1.117` on port `502`. You can also adjust the `Unit ID` or `Endianness` if your environment requires those to be changed.

The next section is the registers to read. This will change greatly depending on what piece of equipment you're reading from, but our Banner Wireless Controller is configured to expose the humidity on Holding Register 0, the temperature in celsius on Holding Register 1, and the temperature in Fahrenheit on Holding Register 2. Each register has a required length field as well. In this case, the data is stored in a single register, so the length is set to 1. As you read registers, an object is being built on the workflow payload with the value of each register stored on whatever you specified in the `Result Key` field.

The last configuration section is the `Destination Path`. This is where the final result object, with each key specified by the registers, will be placed on the payload. So in this example, an object with three keys (humidity, tempC, and tempF) will be put on the payload at `working.modbus`. The value at each key will be an array equal to the length configured for that register.

```json
{
  "working" : {
    "modbus" : {
      "humidity" : [5859],
      "tempC" : [111],
      "tempF" : [855]
    }
  }
}
```

At this point, no data is being sent to the cloud, but this is a good time to deploy and test that this workflow is properly reading Modbus data. Click the `Save` button on the top-right of the screen and then click the  `Deploy` button.

![Deploy Popup](/images/edge-compute/walkthrough/deploy-popup.png "Deploy Popup")

Losant keeps track of every version of every workflow deployed to edge compute devices. This means a workflow must first be versioned before it can be deployed. This popup provides a quick way to version this workflow, which defaults to the current date and time in UTC. You can change it to whatever you'd like. You next need to choose which edge compute devices to deploy this workflow version to. Choose the edge compute device you created earlier in this walkthrough. Click the `Deploy Version` button to schedule this deployment.

Under normal conditions, a workflow version will be successfully deployed to an edge compute device in a matter of a few seconds. You can monitor the process by clicking the `Deployments` tab on the menu along the right side of the screen.

After the deploy completes, open the `Debug` tab and select your edge compute device from the dropdown. This will allow you to stream any debug information from that device to your browser. You can use this to verify that your Modbus read operations are working correctly.

![Debug Output](/images/edge-compute/walkthrough/debug-output.png "Debug Output")

When you hover over a debug message, a notice will show up over the canvas area instructing you to switch versions to see the "node path". This is because you're currently viewing the `develop` version of the workflow, but you just created and deployed a different version to the edge device. The "node path" is a helpful visual indicator to know which path in the workflow was taken to reach the Debug Node that generated whatever message you're currently hovering over. Since workflows can change drastically between versions, you'll have to be viewing the same version that generated the debug message in order to highlight the path. If you want to check it out, you can switch versions by clicking the `Versions` menu on the right side of the screen.

Since it looks like this workflow is successfully reading Modbus data, we can continue editing the workflow to translate the values and report them to the cloud.

What's stored in Modbus registers is not always in a friendly format. Below is the table from the Banner temperature sensor that describes how the data is stored and how it translates to actual values.

![Modbus Registers](/images/edge-compute/walkthrough/modbus-registers.png "Modbus Registers")

As you can see, we're getting a value between 0 and 10000 for humidity, and between -32768 and 32767 for celsius and Fahrenheit. So in order to convert these to actual values, we need to divide humidity by 100 and divide the temperatures by 20.

Fortunately, this is easily done with a [Math Node](/workflows/logic/math/).

![Math Node](/images/edge-compute/walkthrough/math-node.png "Math Node")

Add three expressions, one for each conversion to the math node. The expressions are below.

```text
{{ working.modbus.humdity.[0] }} / 100
{{ working.modbus.tempC.[0] }} / 20
{{ working.modbus.tempF.[0] }} / 20
```

Each expression uses a template to reference the raw value and then divides them by the appropriate conversion factor. The result of each expression is then put back on the payload at `state.humidity`, `state.tempC`, and `state.tempF`. Once you save and deploy this workflow, you can see these converted values in the debug output.

The last step is to report these converted values to our kegerator peripheral. Add a [Device State Node](/workflows/outputs/device-state/) to do this.

![Device State Node](/images/edge-compute/walkthrough/device-state-node.png "Device State Node")

Change the radio to `Select a specific device` and choose the peripheral device created earlier. In this example, the peripheral device is named "Kegerator".

This device has two attributes, one for humdity and one for temperature. Set the humidity value to `{{ state.humdity }}` and set the temperature value to `{{ state.tempF }}`. In this example, the temperature in celsius won't be reported to the cloud. After you save and deploy this workflow again, data is now being reported from your edge device to the cloud. You can verify this by opening the `Debug` tab on your peripheral device page.

![Device Debug Tab](/images/edge-compute/walkthrough/device-debug-tab.png "Device Debug Tab")

The device's debug tab allows you see recent state messages reported by this device. You can also view real-time activity by inspecting the Device Log, which on the right side of every device tab.

At this point, you've successfully deployed a working edge compute device that reads local Modbus data over TCP, performs some processing on that data, and then reports it to the cloud. You can now trigger a [Cloud Workflow](/workflows/cloud-workflows/) for further processing or alerting, build a [Dashboard](/dashboards/overview/) to visualize this data, or use [Experiences](/experiences/overview/) to create an entire custom application.





