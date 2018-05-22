WebSurge runs with a small core load engine and this engine is plugged into the front end application I’ve shown so far.

There’s also a command line interface available to run WebSurge from the Windows command prompt. You can run WebSurgeCli.exe from anywhere to run tests for either an individual URL (similar to AB.exe for example) or a full Session file.

![](https://weblog.west-wind.com/images/2014Windows-Live-Writer/Web-Load-Testing-West-Wind-WebSurge_EBFD/Console_2.png)

By default when it runs WebSurgeCli shows progress every second showing total request count, failures and the requests per second for the entire test. A silent option can turn off this progress display and display only the results.

The command line interface can be useful for build integration which allows checking for failures perhaps or hitting a specific requests per second count etc.

It’s also nice to use this as quick and dirty URL test facility similar to the way you’d use Apache Bench (ab.exe). Unlike ab.exe though, WebSurgeCli supports SSL and makes it much easier to create multi-URL tests using either manual editing or the WebSurge UI.

### Command Line Options
The following command line options are available:

```
usage:   WebSurgeCli <SessionFile|Url> -sXX -tXX -dXX -r -yX

Parameters:
-----------
SessionFile     Filename to a WebSurge/Fiddler HTTP session file
Url             Single URL to to hit

Commands:
---------
-h | -?      This help display

Value Options:
--------------
-s          Number of seconds to run the test (10)
-t          Number of simultaneous threads to run (2)
-d          Per request delay (0)
-y          Display mode for progress (1)
            0 - No progress, 1 - no request detail,
            2 - no progress summary, 3 - show all

Switches:
---------
-r          Randomize order of requests in Session file

Examples:
---------
WebSurgeCli c:\temp\LoadTest.txt  -s20 -t10
WebSurgeCli http://localhost/testpage/  -s20 -t10</pre>
```