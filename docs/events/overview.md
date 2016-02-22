# Events

Events provide a way to collect, view, and respond to exceptional occurrences in your application. For example, if the temperature of a refrigerator exceeds 40 degrees, a temperature warning event could be created. If the temperature then exceeds 50 degrees a temperature error could be created.

![Event List](/images/events/event-list.png "Event List")

## Creating Events

Events are typically created using Structure [workflows](/workflows/overview). The [events](/workflows/outputs/record-event) output node allow you to create events as needed.

![Create Event Workflow](/images/events/create-event-workflow.png "Create Event Workflow")

In the above example, a device is reporting temperature state and triggering the workflow. The condition node is checking the value of the temperature. If the value is greater than 40 a temperature warning event is created.

## Using Events

Events are typically consumed using the events page, which is accessible on the Events menu.

![Events Menu](/images/events/events-menu.png "Events Menu")

The events page allows you to review the details about each event, acknowledged them if needed, and resolve them. Resolved events will no longer show up on the events page.

Events can also be used to trigger other workflows. In the refrigerator example, if you wanted to perform additional actions when an event gets created, you could use the [event trigger](/workflows/triggers/event/) to run additional workflows.

![Event Trigger](/images/events/event-trigger.png "Event Trigger")

In the above example, the workflow is trigger whenever an event is created with a specific level (info, warning, error) and specific subject. The workflow then sends an SMS message to alert the user.

## Events Lifecycle

Events include basic lifecycle features for proper organization and handling.

```
Open -> Acknowledged -> Resolved
```

How the events transition through these states is entirely up to your and your specific application.
