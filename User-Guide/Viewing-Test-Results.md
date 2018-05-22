Tests run for the specified number of seconds or until you press the Stop button. When the test is done you get a simple Results display:

![](https://weblog.west-wind.com/images/2014Windows-Live-Writer/Web-Load-Testing-West-Wind-WebSurge_EBFD/WebSurgeResult_2.png)

On the right you get an overall summary as well as breakdown by each URL in the session. Both success and failures are highlighted so it’s easy to see what’s breaking in your load test. The report can be printed or you can also open the HTML document in your default Web Browser for printing to PDF or saving the HTML document to disk.

The list on the right shows you a partial list of the URLs that were fired so you can look in detail at the request and response data. The list can be filtered by success and failure requests. Each list is partial only (at the moment) and limited to a max of 1000 items in order to render reasonably quickly.

Each item in the list can be clicked to see the full request and response data: 

![](https://weblog.west-wind.com/images/2014Windows-Live-Writer/Web-Load-Testing-West-Wind-WebSurge_EBFD/WebSurgeRequestDetail_2.png)

This particularly useful for errors so you can quickly see and copy what request data was used and in the case of a GET request you can also just click the link to quickly jump to the page. For non-GET requests you can find the URL in the Session list, and use the context menu to Test the URL as configured including any HTTP content data to send.

You get to see the full HTTP request and response as well as a link in the Request header to go visit the actual page. Not so useful for a POST as above, but definitely useful for GET requests.

Finally you can also get a few charts. The most useful one is probably the Request per Second chart which can be accessed from the Charts menu or shortcut. Here’s what it looks like:

 ![](http://weblog.west-wind.com/images/2014Windows-Live-Writer/Web-Load-Testing-West-Wind-WebSurge_EBFD/Chart_2.png)

Results can also be exported to JSON, XML and HTML. Keep in mind that these files can get very large rather quickly though, so exports can end up taking a while to complete.
