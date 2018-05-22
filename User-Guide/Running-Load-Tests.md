Once you’ve created a Session you can specify the length of the test in seconds, and specify the number of simultaneous threads to run each session on. To start a test press the Start button on the main toolbar.

Sessions run through each of the URLs in the session sequentially by default. One option in the options list above is that you can also randomize the URLs so each thread runs requests in a different order. This avoids bunching up URLs initially when tests start as all threads run the same requests simultaneously which can sometimes skew the results of the first few minutes of a test.

While sessions run some progress information is displayed: 

![](https://weblog.west-wind.com/images/2014Windows-Live-Writer/Web-Load-Testing-West-Wind-WebSurge_EBFD/Progress_2.png)

By default there’s a live view of requests displayed in a Console-like window. On the bottom of the window there’s a running total summary that displays where you’re at in the test, how many requests have been processed and what the requests per second count is currently for all requests.

Note that for tests that run over a thousand requests a second it’s a good idea to turn off the console display. While the console display is nice to see that something is happening and also gives you slight idea what’s happening with actual requests, once a lot of requests are processed, this UI updating actually adds a lot of CPU overhead to the application which may cause the actual load generated to be reduced. If you are running a 1000 requests a second there’s not much to see anyway as requests roll by way too fast to see individual lines anyway. If you look on the options panel, there is a NoProgressEvents option that disables the console display. Note that the summary display is still updated approximately once a second so you can always tell that the test is still running.
