WebSurge works by creating multiple URLs to capture as a set called a Session. Sessions are then 'played back' under load. The first step to using WebSurge then is to create Sessions.


![](https://weblog.west-wind.com/images/2014Windows-Live-Writer/Web-Load-Testing-West-Wind-WebSurge_EBFD/Sessions_2.png)

Sessions can be created in several different ways:

### Manually Creating Requests
You can create requests using Sessions tab and the  *New* option on the Session view. This allows you to manually create URLs and add HTTP headers using the Request tab input fields.

 ![](https://weblog.west-wind.com/images/2014Windows-Live-Writer/Web-Load-Testing-West-Wind-WebSurge_EBFD/RequestEditing_2.png)

You can enter URLs and fill in plain HTTP headers and request content to send to the server.

**Use it for single URL Testing**
Incidentally I’ve also found this form as an excellent way to test and replay individual URLs for simple non-load testing purposes. Because you can capture a single or many URLs and store them on disk, this also provides a nice HTTP playground where you can record URLs with their headers, and fire them one at a time or as a session and see results immediately. It’s actually an easy way for REST presentations and I find the simple UI flow actually easier than using Fiddler natively.

Finally you can save one or more URLs as a session for later retrieval. I’m using this more and more for simple URL checks.

### Using the Capture Tool
WebSurge includes a built-in URL capture tool that can capture requests from any HTTP based application on your machine. The capture acts as an automated proxy that intercepts and captures HTTP requests from browsers, or any Windows application. 

![](http://west-wind.com/WebSurge/Images/WebSurge_Capture.png)

With this tool you can capture anything HTTP -SSL requests and content from Web pages, AJAX calls, SOAP or REST services – again anything that uses Windows or .NET HTTP APIs. Behind the scenes the capture tool uses FiddlerCore so basically anything you can capture with Fiddler you can also capture with Web Surge Session capture tool. Alternately you can actually use Fiddler as well, and then export the captured Fiddler trace to a file, which can then be imported into WebSurge. This is a nice way to let somebody capture session without having to actually install WebSurge or for your customers to provide an exact playback scenario for a given set of URLs that cause a problem perhaps.

Note that not all applications work with Fiddler’s proxy unless you configure a proxy. For example, .NET Web applications that make HTTP calls usually don’t show up in Fiddler by default. For those .NET applications you can explicitly override proxy settings to capture those requests to service calls.

The capture tool also has handy optional filters that allow you to filter by domain, to help block out noise that you typically don’t want to include in your requests. For example, if your pages include links to CDNs, or Google Analytics or social links you typically don’t want to include those in your load test, so by capturing just from a specific domain you are guaranteed content from only that one domain. Additionally you can provide url filters in the configuration file – filters allow to provide filter strings that if contained in a url will cause requests to be ignored. Again this is useful if you don’t filter by domain but you want to filter out things like static image, css and script files etc. Often you’re not interested in the load characteristics of these static and usually cached resources as they just add noise to tests and often skew the overall url performance results. In my testing I tend to care only about my dynamic requests.

> #### @icon-info-circle SSL Captures Certificate Installation
> Note, that in order to capture SSL requests you’ll have to install an intermediate self-signed certificate so these secure requests can be parsed. You can do this on the Capture form with the button in the upper right corner.

### Loading Sessions From File
Session can be stored and loaded from disk and use Fiddler's request capture format, so captured Fiddler data can be easily loaded in WebSurge. When you create sessions either manually or using the capture tool sessions are stored initially in memory until you click on the Save button to write them to disk.

The format used for storage is essentially raw HTTP headers with a very slight modification: The first header contains the full URL instead of a relative URL and a Host: header. This tends to be more readable and allows for easier grouping of the same URLs after test runs are complete and the results are calculated. Because the Session files are just plain text you can also create and edit these files directly either by hand or using programmatic tools. 

Once a Session file is associated with a particular session by loading it it or saving it, the session file shows on status bar of the WebSurge form. If you edit this file and save, any changes made are immediately reflected in the Session list. Likewise any changes made in the Session list directly can be saved to disk at any time to update the underlying file.