# Nifi Hello World Example
Apache Nifi is a Data Flow tool that allows for data to be pulled or put into Nifi from many different endpoints.  Once the data is inside of Nifi it can then route data based on payload, enrich data, amongst do many other things before landing this data into another data repository (such as Hbase, Solr, HDFS, RDBMs, etc).  There are over 180+ different processors built inside Nifi and the hopes is to show you in this tutorial how to use Nifi as a WebServer and WebSocket to stream data and write data down to a flat file.  The intention of this tutorial is to provide a basic understanding of flexibility, ease of use this open source tool provides.  This tutorial will leverage Apache Nifi as a web server that launches a web page that accepts any value.  When you enter the value you then open a web socket to another Nifi Processor, Send the value in the text box to Nifi and Nifi will write the contents to a location as defined in the PutFile processor.

# Download/Install
Download Apache Nifi here - https://nifi.apache.org/download.html
This Repo project was tested with version 1.1.0 but should work with later versions.

Follow guidance to download and install the software as illustrated here - https://nifi.apache.org/docs.html

Once the setup is working like in my screen shot below 

![image](/images/NifiInitialLaunchPage.png?raw=true "Nifi Main Page")



If you can log into the Nifi Dashboard you can proceed to the next step.


# Import XML Nifi Template

Download or clone this repo....remember the location you downloaded this repo to.
Now that you have successfully installed Nifi lets import the XML file included in this repository named HelloWorld.xml.  To do this follow the image below and choose import after selecting the HelloWorld.xml to import.  

![Alt text](/images/ImportTemplate.png?raw=true "Nifi Main Page")


# Add Template to Nifi Canvas

Now that we have the Nifi Template uploaded we have to now download add the template to the canvas as shown in the screen shot below 

![image](/images/NifiAddTemplate.png?raw=true "Nifi Main Page")

Once you click Add you’ll see the below screen shot on your canvas

![image](/images/NifiTemplateAdded.png?raw=true "Nifi Main Page")

Notice the Red Circled Warning icons on the different Nifi processors that I circled in red.  The are warning that we will have to address.  NOTE: You probably have another Processor or Two with different warnings on the (Such as ExecuteStreamCommand and PutFile).  I’ll explain why after we get through configuring these three circled processors first.

# Configure HandleHttpRequest Nifi Processor

Now what we have to do is right click on processor named Nifi-WebServer-HandleHTTP processor (which is the HandleHTTPRequest Nifi Processor) and click on Configure.  This will open up a configuration window as shown in the picture below

![image](/images/configureHTTP.png?raw=true "Nifi Main Page")

NOTE:
The listening port an HTTP request is listening on port = 6688
The hostname = localhost
The HTTP Context Map = No Value Set

Action = click on the No Value Set row next to HTTP Context Map hit the drop down arrow and select Create new service.  This will bring up an Add Controller Service window where you’ll have to create a StandardHttpContextMap service which should be populated within the dropdown for you automatically.  Select “Create” and that should create the context map.

Now that you are back in the Configure Processor window you should see StandardHttpContextMap next to HTTP Context Map.  

Action = Notice the arrow pointing to the right in the third column.  Click on the arrow and this will bring up the Process Group Configuration window on the Controller Services tab.  Notice that the StandardHttpContextMap State is listed on disable.  Click on the lightening bolt all the way on the right side to enable this controller service. Leave the option as service only and click “Enable”.  Once enabled you can close the Enable Controller Service and click the “X” in the top right corner of the window to close the Process Group Configuration window.    

We should now be back on the Nifi Canvas looking at the Processor named Nifi-WebServer-HandleHTTP changed from a yellow exclamation to a Red Box.



# Configure HandleHttpResponse Nifi Processor
Now lets right click on the HandleHTTPResponse Nifi Process click on Configure and next to HTTP Context Map there it should say “No Value Set” (note mine has this GUID value).  Click the drop down and select StandardHttpContetMap.  NOTE: This is the same Context Map that we created in the previous step.

See Below for a screen shot

![image](/images/configureHTTPRequest.png?raw=true "Nifi Main Page")


Once you select Apply you’ll see the yellow warning again change to a “Red Box” shape.


# Configure ListenWebSocket Nifi Processor
Right click on ListenWebSocket Nifi Processor and select Configure. Next to WebSocket Server ControllerService click the value listed as “No Value Set” and in the dropdown select JettyWebSocketServer.  

See image below
![image](/images/configureWebSocket.png?raw=true "Nifi Main Page")

Select “Create”.  Just as before the arrow pointing to the right now appears next to JettyWebSocketServer.  Click on the arrow pointing to the right. Click “Yes” to save changes.  This opens the Process Group Configuration screen with the Controller Services tab selected.  We just created a new controller service called JettyWebServer.  Notice the state is invalid that is because we need to add a listening port to this controller service.  Click the pencil icon all the way to the right. This will open up a configure controller service window.  For the Property “Listen Port” lets set that to 9998.  (The reason I selected 9998 is because the index.html code in the Archive directory is going to make a web socket request on this port.).  Select “APPLY” and now click the lightening bolt icon to enabled the service.

# The other processors (ExecuteStream Command and Put File)
Right click on the ExecuteStream process Processor and select configure make sure you set the “Command Path” property to a directory that exists with the server.sh file from the github repo.  In this example it is using this directory “/Users/drice/Downloads/Software/nifi-1.1.0.2.1.2.0-10/server.sh”

Also make sure you edit the content of the server.sh file.  Currently this content is “/Users/drice/Documents/websocket/index.html”.  Again you’ll want to make sure to modify this directory structure to match where you have the index.html on your system.

Lastly the PutFile process - where the data will write the contents of the stream.  Current value is set to “/Users/drice/Downloads/Software/nifi-1.1.0.2.1.2.0-10/logs”.  Make sure the directory changes to reflect a proper value for your system.

# Starting the flow
Now that we have configured everything we should be able to click anywhere on the canvas (on the Grid and not on a processor or a connection) and click start.  As shown below.

![image](/images/StartTemplate.png?raw=true "Nifi Main Page")

This will start all the processors within Nifi.  If successful you should be able to first Launch a Web Page if you point your browser at http://localhost:6688

![image](/images/WebPage.png?raw=true "Nifi Main Page")

Now you can type anything in the text field.  Click on Open, then Send and this will write data out to the directory you defined in the put file processor.  See image below as an example.


![image](/images/WorkingFlow.png?raw=true "Nifi Main Page")






