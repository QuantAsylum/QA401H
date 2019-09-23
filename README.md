# QA401H
Releases (no source) for the QA401H "headless" application. This application allows a RESTful interface to the QA401 hardware. The app is dotnetcore, which means you can the app on Windows, Linux and MacOs. These are all early releases, shared to get developer feedback. Read more [here](https://quantasylum.com/blogs/news/qa401-headless-linux) 

To run, download the release zip, and unzip it to a directory. Make sure the QA401 application isn't running (as they will both fight for access to the QA401 hardware). Open a command window in that directory. And then type:

~~~~
dotnet qa401h.dll
~~~~

At that point, you will be instructed to re-plug the QA401 hardware. You have about 5 seconds to do this. Alternately, you may replug the hardware before you launch the app. This need to "start fresh" is a bug that needs to be resolved but it's related to the USB library.

Once the, app is running, go to your browser and issue
~~~~
http://localhost:9401/
~~~~

That will show the REST api.

Look in the api for the Version command. And then issue

~~~~
http://localhost:9401/Status/Version
~~~~

That will return a REST structure as shown:
~~~~
{ "SessionId":"0", "Value":"0.93" }
~~~~~
