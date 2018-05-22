> #### Under Construction
> User Sessions are an experimental feature at the moment and require manual editing of configuration files.

WebSurge runs tests by running a group of URLs as a session. Each session is isolated on its own thread and can optionally track some state such as **cookies** and an **associated user**.

### Cookie Tracking
WebSurge by default captures Cookie information for each started session. A new session starts with the first URL in the session list of URLs and then executes each of the subsequent URLs. Cookies from the last request are captured and stored on an internal Cookie Container and passed through all subsequent requests.

Using Cookies allows you to record sessions for a specific user, by logging in and then performing authenticated tasks that typically require a cookie.

This works fine for simulating a single user moving through a site, but if running under load you end up using the same user for all running sessions.

### User Mapping
If you want to track multiple users you need to configure custom user profiles. A user can specify one of two identifying features:

* **An Authorization Cookie**  
You can create a specific Cookie for each user that corresponds to a previously validated and still active session and assign it to the `AuthCookie` key for each user.

* **One or More Login URLs and Login Credentials**  
You can specify one or more **exact** URLs that correspond to a URL in your test session, and provide a set of form variables or raw Request buffer (for Services) that allows the user to authenticate.

### Currently Users must be specified as JSON Configuration in the .websurge file
Currently there's no UI for the user management features and the user info has to be added through raw JSON that's part of the .websurge configuration file. 

To set up users:

* Create a WebSurge Session and Save to Disk
* Open the `.websurge` file
* Add Users configuration into the JSON at the bottom of the file


### Json Format for Users
The following is the JSON WebSurge options that lives on the bottom of a `.websurge` file and contains session settings. 

Here's an example of a `.websurge` file that works with an HTML login form in an old WebForms Web application. The key property is `Users`:

```json
{
  "NoProgressEvents": false,
  "DelayTimeMs": 2,
  "NoContentDecompression": false,
  "CaptureMinimalResponseData": false,
  "MaxResponseSize": 0,
  "ReplaceQueryStringValuePairs": null,
  "ReplaceDomain": "localhost",
  "ReplaceCookieValue": null,
  "ReplaceAuthorization": null,
  "Username": "",
  "Password": "",
  "Users": [
    {
      "LoginUrls": [
        {
          "Url": "http://dev.west-wind.com/TimeTrakkerWeb/login.aspx?ReturnUrl=%2fTimeTrakkerWeb%2f",
          "Headers": [],
          "FormVariables": [
            {
              "Key": "ctl00_Content_Username",
              "Value": "rstrahl@west-wind.com",
              "BinaryValue": null
            },
            {
              "Key": "ctl00_Content_Password",
              "Value": "ww",
              "BinaryValue": null
            },
            {
              "Key": "ctl00_Content_RememberMe",
              "Value": "on",
              "BinaryValue": null
            },
            {
              "Key": "ctl00_Content_LoginButton",
              "Value": "Log in",
              "BinaryValue": null
            }
          ],
          "ContentType": "application/x-www-form-urlencoded",
          "RawContent": null,
          "HttpVerb": "POST"
        }
      ],
      "AuthCookie": null
    },
    {
      "LoginUrls": [
        {
          "Url": "http://dev.west-wind.com/TimeTrakkerWeb/login.aspx?ReturnUrl=%2fTimeTrakkerWeb%2f",
          "Headers": [],
          "FormVariables": [
            {
              "Key": "ctl00_Content_Username",
              "Value": "bill@west-wind.com",
              "BinaryValue": null
            },
            {
              "Key": "ctl00_Content_Password",
              "Value": "bb",
              "BinaryValue": null
            },
            {
              "Key": "ctl00_Content_RememberMe",
              "Value": "on",
              "BinaryValue": null
            },
            {
              "Key": "ctl00_Content_LoginButton",
              "Value": "Log in",
              "BinaryValue": null
            }
          ],
          "ContentType": "application/x-www-form-urlencoded",
          "RawContent": null,
          "HttpVerb": "POST"
        }
      ],
      "AuthCookie": null
    }
  ],
  "RandomizeRequests": false,
  "RequestTimeoutMs": 15000,
  "WarmupSeconds": 2,
  "ReloadTemplates": false,
  "FormattedPreviewTheme": "visualstudio",
  "LastThreads": 2,
  "IgnoreCertificateErrors": false,
  "TrackPerSessionCookies": true,
  "LastSecondsToRun": 10
}
```

In this example two users are set up which each specify an exact login URL, and all the form variables that have to be submitted to log this user in. WebSure overrides the original POST data of the captured request with these values to post the form. Once posted, the server sends an authentication cookie which is picked up by WebSurge's CookieContainer and passed through the rest of the current session on all subsequent requests.

### REST Services
The above example uses form variables to force a login, but you can also skip the form variables and instead use `RawContent` to post say a JSON auth request to a REST service.
```json
"Users": [
    {
      {
      "LoginUrls": [
        {
          "Url": "http://dev.west-wind.com/TimeTrakkerWeb/api/login",
          "Headers": [],
          "FormVariables": []
          "ContentType": "application/json",
          "RawContent": '{"username": "frankf", "password": "seekrity" }',
          "HttpVerb": "POST"
        }
      ],
    }
    {
      "LoginUrls": [
        {
          "Url": "http://dev.west-wind.com/TimeTrakkerWeb/api/login",
          "Headers": [],
          "FormVariables": []
          "ContentType": "application/json",
          "RawContent": '{"username": "ricks", "password": "seekrit" }',
          "HttpVerb": "POST"
        }
      ],
      "AuthCookie": null
    }
],
```  

### No UI - yet
While in this experimental stage there's no UI associated with this interface. This will be added once the data format and operation has been finalized.