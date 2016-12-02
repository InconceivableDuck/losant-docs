# Sandbox

Your Sandbox is the collection of all applications and dashboards owned by your personal account. From your Sandbox, you can test new functionality for eventual [transfer](/organizations/transferring-resources) to a new organization or an existing [organization](/organizations/overview). You can even run small, personal applications out of your Sandbox for an extended period, so long as you stay within the Sandbox's [resource limits](/organizations/resource-limits).

To view your Sandbox, click the `Organizations Tab` and then select `My Sandbox` from the dropdown menu.

![Sandbox Link](/images/user-accounts/sandbox-link.png "Sandbox Link")

## Applications

All application functionality – [devices](/devices/overview), [workflows](/workflows/overview), and everything else within the platform – is available within your Sandbox. The only difference is that any devices within your Sandbox, as well as any payloads generated by applications within your Sandbox, count towards the Sandbox's [resource limits](/organizations/resource-limits), which are considerably lower than for paid plans.

![Sandbox Applications](/images/user-accounts/sandbox-applications.png "Sandbox Applications")

### Resource Limits

**Your will never be charged for Sandbox usage.** However, unlike with organizations – where exceeding your [payload limit](/organizations/resource-limits/#payloads) simply accrues additional charges – any payloads generated when your Sandbox is over its payload limit will be **rejected by the platform**. If that happens, you must either transfer resources to an organization or wait for your Sandbox's limit period to turn over.

Once Sandbox applications are [transferred](/organizations/transferring-resources) to an organization, devices within that application immediately count against the the new organization and are freed up within the Sandbox. Similarly, payloads generated by those applications begin counting towards the organization at the time of transfer.

## Dashboards

![Sandbox Mixed Dashboard](/images/user-accounts/sandbox-mixed-dashboard.png "Sandbox Mixed Dashboard")

Sandbox-owned [dashboards](/dashboards/overview) possess all the same features as organization-owned dashboards – the same block options, the same [access control](/dashboards/overview/#dashboard-access-control), the same themes and data refresh rates.

Sandbox dashboards have one additional feature that is not available to organization-owned dashboards: While organization dashboard blocks may only reference applications owned by that organization, Sandbox dashboard blocks may pull data from any application owned by the user's Sandbox or from any organization the user is a member of. This allows you to build your own views into multiple systems within one dashboard. However, this means that extra care must be taken when transferring a Sandbox dashboard to an organization, as any blocks that reference Sandbox-owned applications or applications owned by other organizations will break after the transfer.