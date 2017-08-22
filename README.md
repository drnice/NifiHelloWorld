# Nifi Hello World Example
Apache Nifi is a Data Flow tool that allows for datat to be pulled or put into Nifi from many different endpoints.  Once the data is inside of Nifi it can then route data based on payload, enrich data, amongst do many other things before landing this data into another data repository (such as Hbase, Solr, HDFS, RDBMs, etc).  There are over 180+ different processors built inside Nifi and the hopes is to show you in this tutorial how to use Nifi as a WebServer and WebSocket to stream data and write data down to a flat file.  The intention of this tutorial is to provide a basic understanding of flexibility, ease of use this open source tool provides.

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
