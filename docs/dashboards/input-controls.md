# Input Controls

The Input Controls block allows you to send commands to devices, or to trigger workflows, directly from a dashboard. The block includes various input components to allow for configuring the payloads sent with those commands or triggers.

![Input Controls Dashboard](/images/dashboards/input-controls-overview.png "Input Controls Dashboard")

## Adding and Removing Controls

From the block's edit screen, controls can be added by clicking the "Add Controls" button at the bottom of the configuration panel. This will open a drop-down menu containing all of the available input types. On selection of a control type, a new configuration panel will appear for that input.

![Add Input Control](/images/dashboards/input-controls-add.png "Add Input Control")

Controls can be removed from the edit screen by clicking the trashcan icon at the right side of the control's configuration panel.

## Rearranging and Resizing Controls

On the edit screen, all controls can be resized and rearranged within the input control block. To move a control, simply click and drag the input to a new location. To resize an input, click and hold the handle in the bottom right corner of the control and drag the control to its new width.

![Rearranging Input Controls](/images/dashboards/input-controls-dragdrop.png "Rearranging Input Controls")

## Control Configuration

The block supports inputs of four types, plus a special ["Help Block" component](#help-block-component). The four inputs share a few common attributes:

*   **Label**: All controls require a label attribute.
*   **Color**: Controls other than text inputs can optionally be given a custom color.
*   **Template ID:** Controls other than buttons are automatically assigned a Template ID, which can be used when constructing your command / workflow payloads. You may change this ID if you wish.

### Button Inputs

Buttons are responsible for triggering device commands or workflows when clicked. Without a button, the other controls within the input controls block are useless, so make sure your block has at least one button within it.

![Button Input](/images/dashboards/input-controls-send-command.png "Button Input")

If you'd like your button press to trigger a [device command](/devices/commands/), select the **Send Device Command** radio button. This will display two required input fields:

*   **Device IDs / Tags**: A [device query](/devices/device-queries/) for which device(s) should receive the command. Note that the only available devices are the ones within the block's currently selected application.
*   **Command Name**: The command that should be sent to the device(s). The field may be set with a static value (e.g. `setColor`), or with a Mustache-wrapped Template ID for a text input (e.g. `{{text-0}}`).

If your button should trigger a [workflow](/workflows/overview/), select the **Trigger Workflow** radio button. This will display one required input field:

*   **Workflow Virtual Button**: In order to trigger a workflow, you must have at least one workflow within the selected application, and at least one [virtual button](/workflows/triggers/virtual-button/) within that workflow. This input will display all virtual buttons across all of the application's workflows, from which one must be selected to trigger when the button is pressed.

![Select Virtual Button](/images/dashboards/input-controls-trigger-workflow.png "Select Virtual Button")

### Range Inputs

Range inputs allow for the setting of **number** values. When configuring the input, it is necessary to define the range's minimum, maximum and default values, as well as the step size (the size of each "tick" in the range slider).

![Range Input](/images/dashboards/input-controls-range-input.png "Range Input")

From the dashboard, the input's knob can be dragged left or right to set the numerical value to be sent in the payload. The area to the left of the knob will appear in the color selected during configuration.

### Toggle Inputs

Toggle inputs allow for the setting of **boolean** values (true or false). The default value must be set.

![Toggle Input](/images/dashboards/input-controls-toggle-input.png "Toggle Input")

From the dashboard, the toggle can be flipped between the two values. When set to **true**, the toggle's background will match the color chosen for it during configuration.

### Text Inputs

Text inputs allow for the setting of arbitrary values, usually as a **string**. The control may be left empty by default if desired.

![Text Input](/images/dashboards/input-controls-text-input.png "Text Input")

From the dashboard, enter some text within the text input field to use within your payload or command name.

## Constructing Payloads

Device commands and workflow triggers may optionally be sent with a JSON payload, constructed as a [JSON template](/workflows/accessing-payload-data/#json-templates). It is the purpose of the input controls to help you construct the payload quickly and easily from the dashboard.

When constructing the [JSON template](/workflows/accessing-payload-data/#json-templates), the values of the other inputs are referenced by their Template ID. For example, given the following configuration ...

![Lights Example](/images/dashboards/input-controls-lights-example.png "Lights Example")

On press of the button, "My First Device" will receive a command named "setColor", with the following payload:

```json
{
  "brightness": 70,
  "enabled": true,
  "foregroundColor": "rgb(125, 50, 75)",
  "backgroundColor": "#f0f0f0",
  "source": "dashboard"
}
```

`brightness` is passed as a number and `enabled` is passed as a boolean, whereas the R, G, and B values are passed as part of a string since the `foregroundColor` property's value is wrapped in double quotes. There is also a static property of `source` being passed in the payload, and since we are not assigning any Template ID to its value, the property will always be submitted with a value of `"dashboard"`.

**Note:** If you do not define a payload for a Trigger Workflow button, the virtual button's default payload – as set within that button's parent workflow – will be sent when your dashboard button is clicked. If you wish to send a blank payload instead of the default payload, set the payload value to `{}` (opening and closing curly braces with nothing in between).

## Help Block Component

The Help Block is a special component in the Input Controls block that allows text to be displayed to users for the purpose of explaining, in greater detail than can be conveyed in a button label, what exactly will happen when a button is pressed and a workflow / device command is fired off.

![Help Block Input](/images/dashboards/input-controls-help-input.png "Help Block Input")

The component has only one input: a textarea in which arbitrary text and [string template](/workflows/accessing-payload-data/#string-templates) referencing values by Template ID can be entered. These values will update as the user changes input values in the other components.

![Help Block Example](/images/dashboards/input-controls-help-example.png "Help Block Example")

The textarea also supports <a href="https://daringfireball.net/projects/markdown/syntax" target="\_blank">Markdown</a>, meaning that links, text formatting and even images can also be displayed within the Help Block.

The Help Block is the only Input Controls component whose height can be adjusted – up to four times a normal component's height.
