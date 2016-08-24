# Dashboards

Losant dashboards provide a flexible and powerful way to display information relevant to your specific connected solution. Users can have many different dashboards and a single dashboard can display information from many different applications and devices.

![Full Dashboard](/images/dashboards/overview-dashboard-full.png "Full Dashboard")

## Adding Blocks

Losant supports many different blocks for visualizing various pieces of information. New blocks can be added to your dashboard by clicking the `Add Block` link at the top of the dashboard.

![Add Block](/images/dashboards/overview-add-block.png "Add Block")

![Select Block](/images/dashboards/overview-select-block.png "Select Block")

## Editing Dashboards

Dashboard blocks and be dynamically resized and dragged for the arrangement that most meets your specific needs.

![Dashboard Animation](/images/dashboards/overview-animation.gif "Dashboard Animation")

## Auto Refreshing

Dashboards by default will automatically refresh the data every 60 seconds. You can pause the refreshing at any time by clicking the pause button at the top of the dashboard. You can also force the dashboard to refresh by clicking the refresh button.  You can also control the refresh interval under the settings for the dashboard.

![Refresh Button](/images/dashboards/overview-refresh-button.png "Refresh Button")

## Viewing Past Dashboard States

By default, dashboards show values as of the last time data was fetched from Losant ("Now"). To view the state of your dashboard blocks at a given point in time, open the Time Jumper dropdown and select the "Jump to a specific date/time" option. After choosing a past time, the dashboard will refresh and display each dashboard block as it appeared at that moment.

![Dashboard Time Jumper](/images/dashboards/dashboard-time-jumper.png "Dashboard Time Jumper")

It is also possible to jump backward and forward in time simply by clicking the arrows on either side of the time jumper dropdown. This allows for quick perusing of dashboard states as they progressed over a period of time. By default, the arrows jump 60 minutes forward and backward, but this value can be changed in the Time Jumper dropdown. The arrow jump amount is stored locally on your browser and will be maintained across different dashboards.

![Dashboard Time Jumper Arrows](/images/dashboards/dashboard-time-jumper-arrows.png "Dashboard Time Jumper Arrows")

A few things to note when viewing past dashboard states:

*  **The following dashboard blocks do not update** when viewing a past dashboard state (meaning, they continue to reflect the "as of now" state of the block): Input Controls, Event List, Device List, Workflow List, Application List, Dashboard List, External Website
* When viewing a past state, the dashboard will cease to refresh data on a regular basis.
* **Each individual block will honor its specific duration settings** regardless of the selected date. For example, when viewing 10:00am on June 1, 2016, a Time Series Graph configured to show the last hour of data will display data from 9:00am to 10:00am of that same date. Meanwhile, a Gauge Block set to display a mean aggregation of data collected over the past four hours will show the aggregated value of its attribute as collected from 6:00am to 10:00am that morning.
* If you attempt to go forward in time past the current date/time, the dashboard will automatically revert to displaying "Now" data and the ability to go forward from that point will be disabled.

## Dashboard Access Control

Dashboards have a three levels of access - private, password protected, and public.  Private
means that only you (or members of your organization, if it is an organization-owned
dashboard) can see the dashboard.  Public dashboards can be seen by anyone who has the
dashboard url, regardless of whether that person is logged in to a Losant account. This is great for sharing public data, but remember that any data exposed in a public dashboard is *public* and is accessible by anyone. Do not make your dashboard public if it contains any private or sensitive data. The third level of access is in between public and private -
you can add a password to your dashboard, and allow anyone with the url and the password
to view the dashboard.  This adds some protection to your dashboard, while still making it
easy to share with people who do not have Losant accounts. You can manage the access control for a dashboard on the settings page for the dashboard:

![Dashboard Access Control](/images/dashboards/dashboard-access-control.png "Dashboard Access Control")

## Embedding Dashboard Blocks into Other Sites

If your dashboard has been set to `public`, you may embed any of your dashboard blocks into a third-party site. To get an embed code, hover over your dashboard block and click the `<>` icon in the block header.

This will display a modal where you can set the block's `width`, `height` and `theme` properties. For your width and height, make sure to enter a valid CSS length attribute (`%`, `px`, `em`, `vw`, etc.).

![Embed Block Modal Checkbox](/images/dashboards/embed-block-modal.png "Embed Block Modal")

NOTE: The following blocks will not display any data on public dashboards or to non-authorized users when embedded:

*   `Application List`
*   `Input Controls`

## Templating

A number of the dashboard blocks allow templating of various output, for greater control over how data is displayed.  Templates are rendered through the [Handlebars templating language](http://handlebarsjs.com/), and in most cases (but not all) the result is treated as [Markdown](http://commonmark.org/help/) for display.  Handlebars has a number of [built in](http://handlebarsjs.com/builtin_helpers.html) helpers, but Losant provides a number of extra ones to make complex templating much easier:

*   `eq` - If a value is equal to some number or string.  
For example: `{{#eq value 100}}Value is 100{{else}}Value is not 100{{/eq}}`  
<br/>
*   `ne` - If a value is not equal to some number or string.  
For example: `{{#ne value 100}}Value is not 100{{else}}Value is 100{{/ne}}`  
<br/>
*   `gt`, `gte` - If a value is greater than (or equal to) some number.  
For example: `{{#gt value 100}}Bigger than 100{{else}}Not bigger than 100{{/gt}}`  
<br/>
*   `lt`, `lte` - If a value is less than (or equal to) some number.  
For example: `{{#lt value 100}}Smaller than 100{{else}}Not smaller than 100{{/lt}}`  
<br/>
*   `match` - If a value matches a given regexp or string.  
For example: `{{#match value "hello"}}Has hello{{else}}Does not have hello{{/match}}`  
<br/>
*   `format` - Formats a number or date using [d3](https://github.com/d3/d3-format) or [moment](http://momentjs.com/docs/#/displaying/format/) syntax, or JSON stringify objects or arrays. The second argument is optional - if not passed, default formatting will be used.  
For example: `{{format value "0.1f"}}` or `{{format value}}`  
<br/>
*   `lower` - Transforms a string to all lowercase.  
For example: `{{lower value}}`  
<br/>
*   `upper` - Transforms a string to all uppercase.  
For example: `{{upper value}}`  
<br/>
*   `encodeURI` - Transforms a string through the [encodeURI](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/encodeURI) function.  
For example: `{{encodeURI value}}`  
<br/>
*   `decodeURI` - Transforms a string through the [decodeURI](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/decodeURI) function.  
For example: `{{decodeURI value}}`  
<br/>
*   `encodeURIComponent` - Transforms a string through the [encodeURIComponent](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/encodeURIComponent) function.  
For example: `{{encodeURIComponent value}}`  
<br/>
*   `decodeURIComponent` - Transforms a string through the [decodeURIComponent](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/decodeURIComponent) function.  
For example: `{{decodeURIComponent value}}`  
