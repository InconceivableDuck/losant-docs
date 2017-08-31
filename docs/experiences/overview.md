# Experiences

Building a product on top of Losant usually involves writing an API service, implementing all of the user authentication, and hosting the result somewhere, which is a lot of work. Experiences bring all of this functionality directly inside your Losant application.

Experiences are a means by which you can build a fully functional API allowing users to interact with your connected [devices](/devices/overview/). Set a custom domain to handle requests; configure [endpoints](/experiences/endpoints/) to respond using the power of Losant's [workflow engine](/workflows/overview/); register [users](/experiences/users/) against your application; and protect data access by assigning those users to [groups](/experiences/groups/). All Experience API Endpoints are powered by workflows inside your Losant application.

![Experiences Overview](/images/experiences/experiences-overview.png "Experiences Overview")

Experience Users, Endpoints and Groups are subject to account [resource limits](/organizations/resource-limits/), with the latter two being [soft limits](/organizations/resource-limits/#soft-limited-resources) (meaning you may request increases to these limits at potentially zero additional charge). If you need to register additional Experience Users, you will have to upgrade to an [organization](/organizations/overview/).

## Initial Setup

There are a few steps to go through before you can start building Experiences within your application. If your Sandbox or organization lacks the number of free workflows, users, endpoints or groups to bootstrap a new Experience, you will be unable to proceed. You will have to request soft limit increases or upgrade your account.

### Choose a Slug

![Bootstrap Slug](/images/experiences/bootstrap-slug.png "Bootstrap Slug")

The first step in working with Experiences is to choose a custom endpoint slug, which is the subdomain at which your endpoint requests will live. Your slug defaults to your application ID, but it can be changed to a custom subdomain that meets these requirements:

*   Must be at least 4 characters
*   May only contain lowercase letters, numbers, hyphens (-) and underscores (\_)
*   Must be unique across the entire Losant Platform
*   Cannot be a commonly used Internet subdomain, such as "webmail" or "cpanel"
*   Cannot be profane (these are subject to change by Losant without notice)

HTTP requests for your endpoints should then go to `https://[my-custom-slug].onlosant.com/[my-endpoint]`. You may change the slug at any time, but doing so after you are receiving traffic can be [dangerous](#editing-experience-settings).

### Bootstrap Your Experience

![Bootstrap Progress](/images/experiences/bootstrap-progress.png "Bootstrap Progress")

Next, Losant must set up a few helper resources within your application:

*   A `/favorite-color/{color?}` [endpoint](/experiences/endpoints/) (and its backing workflow), which demonstrates public endpoints and how to use [path parameters](/experiences/endpoints/#route).
*   An `/auth` endpoint (and its backing workflow), which is a starter template for [authenticating](/workflows/experience/authenticate/) Experience Users and [issuing access tokens](/workflows/experience/generate-token/).
*   A `/me` endpoint (and its backing workflow), which demonstrates authenticated endpoints by returning the user who made the request.
*   A test [Experience User](/experiences/users/) for testing authentication and protected endpoints.
*   An [Experience Group](/experiences/groups/) with the test user as a member.

All of these resources can be deleted at any time, but note that if your Experience uses any authenticated endpoints, you should at least keep the `/auth` endpoint and workflow (or build a similar one) so that your Experience Users can authenticate and receive a token.

### Test Your Experience

Finally, you'll receive a review of what was created and some instructions for testing your new endpoints. The `/favorite-color`  endpoints are public `GET` routes, so they can be tested by simply visiting the URLs in your browser. Authenticating and retrieving the current user will require more advanced requests, so we provide sample [curl](https://curl.haxx.se/) commands for [testing your endpoints](/experiences/endpoints/#using-endpoints).

**Take note of the random password assigned to your test user.** If you lose this password, you will have to [edit the user](/experiences/users/#required-fields) to reset it.

## Editing Experience Settings

Your Experience settings can be updated at any time, but **be warned!** Making changes to any of these settings can have devastating effects if your Experience is in active use by public or signed-in users.

![Edit Experience Settings](/images/experiences/settings-fields.png "Edit Experience Settings")

Experience settings can be changed under the "Settings" tab of your application's "Experience" subsection. There are two attributes that can be edited on this page:

*   **Endpoint Slug** is the custom subdomain at which your application's endpoints live. **Changing this will break all incoming traffic to your Experience** until your users can migrate their requests to the new domain.
*   **Enable Default CORS Settings**, when checked, automatically responds appropriately to [OPTIONS requests](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/OPTIONS) emitted by web browsers that are sending [asynchronous requests](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/Synchronous_and_Asynchronous_Requests) directly to your Experience Endpoints. Disabling this checkbox would cause asynchronous requests to your endpoints to fail; enabling it is less dangerous, but it would allow [cross-origin request](https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS) to any endpoint for which you have not set up an OPTIONS route.

### Invalidating Access Tokens

If for any reason you feel it is necessary to invalidate all existing access tokens, you can do so from the Experience Settings page. This action does not edit or delete any of your Experience Users; rather, it simply requires that they all log in again before making any authenticated requests.

![Invalidate All Tokens](/images/experiences/settings-invalidate-tokens.png "Invalidate All Tokens")

If you only need to invalidate the access tokens for a single user, you can do that from the [Experience User's edit page](/experiences/users/#invalidating-user-tokens).
