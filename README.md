# QA401H
Releases (no source) for the QA401H "headless" application. This application allows a RESTful interface to the QA401 hardware. The app is dotnetcore, which means you can the app on Windows, Linux and MacOs. These are all early releases, shared to get developer feedback. Read more [here](https://quantasylum.com/blogs/news/qa401-headless-linux) 

To run, download the release zip, and unzip it to a directory. Make sure you have the dotnet runtime installed (see README.TXT in zip file for help with this on Linux). Make sure the QA401 application isn't running (as they will both fight for access to the QA401 hardware and you'll see an error). Open a command window in that directory. And then type:

~~~~
dotnet QA401H.dll
~~~~

Once the, app is running, go to your browser and issue
~~~~
http://localhost:9401/
~~~~

That will show the REST API.

Scroll down and look for the the API for the Version command. And then issue

~~~~
http://localhost:9401/Status/Version
~~~~

That will return a REST structure as shown:
~~~~
{ "SessionId":"0", "Value":"0.93" }
~~~~~

From there, you can query THD, etc. 

Some other links that might help:
This post [HERE](https://quantasylum.com/blogs/news/qa401-headless-linux) shows how to set up on Linux. Depending on versions, there may be other steps required. Again, see the README in the zip for a discussion of other issues that might be encountered.

This post [HERE](https://quantasylum.com/blogs/news/qa401h-rest-and-python) shows how to use Python to query the QA401H app for THD via REST
