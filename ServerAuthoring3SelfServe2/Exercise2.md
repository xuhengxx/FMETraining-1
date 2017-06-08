<!--Instructor Notes-->

<!--Exercise Section-->


<table style="border-spacing: 0px;border-collapse: collapse;font-family:serif">
<tr>
<td width=25% style="vertical-align:middle;background-color:darkorange;border: 2px solid darkorange">
<i class="fa fa-cogs fa-lg fa-pull-left fa-fw" style="color:white;padding-right: 12px;vertical-align:text-top"></i>
<span style="color:white;font-size:x-large;font-weight: bold">Exercise 2</span>
</td>
<td style="border: 2px solid darkorange;background-color:darkorange;color:white">
<span style="color:white;font-size:x-large;font-weight: bold">Data Streaming System</span>
</td>
</tr>

<tr>
<td style="border: 1px solid darkorange; font-weight: bold">Data</td>
<td style="border: 1px solid darkorange">Orthophoto images (GeoTIFF)</td>
</tr>

<tr>
<td style="border: 1px solid darkorange; font-weight: bold">Overall Goal</td>
<td style="border: 1px solid darkorange">Create an FME Server Data Streaming system for orthophotos</td>
</tr>

<tr>
<td style="border: 1px solid darkorange; font-weight: bold">Demonstrates</td>
<td style="border: 1px solid darkorange">Data streaming</td>
</tr>

<tr>
<td style="border: 1px solid darkorange; font-weight: bold">Start Workspace</td>
<td style="border: 1px solid darkorange">C:\FMEData2017\Workspaces\ServerAuthoring\SelfServe2-Ex2-Begin.fmw</td>
</tr>

<tr>
<td style="border: 1px solid darkorange; font-weight: bold">End Workspace</td>
<td style="border: 1px solid darkorange">C:\FMEData2017\Workspaces\ServerAuthoring\SelfServe2-Ex2-Complete.fmw</td>
</tr>

</table>

---

As a technical analyst in the GIS department of a city you have just created a system to allow other departments to download orthophoto data, rather than having to ask you to create it for them. 

Sometimes the end-users download data as JPEG just to open it in a browser or image viewer to inspect it. You realize that, in cases like this, they may be able to use a data streaming service, instead of a data download. 


<br>**1) Open Workspace**
<br>Open the workspace from exercise 2, or the begin workspace listed above. You can see that it consists of various readers, writers, transformers, and other functionality. Most importantly there is an unconnected JPEG Writer that could be used to stream data.

Currently the JPEG Writer is disconnected, so connect it back into the workspace, this time to the Clipper:Inside output port:

![](./Images/Img3.206.Ex2.ConnectJPEG.png)


<br>**2) Publish to FME Server**
<br>Now publish the workspace to FME Server.

In the final dialog of the publishing wizard, check the boxes to register the workspace with both Data Download and Data Streaming (but don't click Finish yet):

![](./Images/Img3.207.Ex2.PublishToStreamService.png)

Now click the Edit button for the Data Download service. Ensure that service is using the output of the Generic Writer.

Next click the Edit button for the Data Streaming service. Ensure that service is using the output of the JPEG Writer (for now we're limiting the streaming of data to JPEG format). 


<br>**3) Run Workspace**
<br>In the FME Server web interface locate the newly published workspace and run it. In the parameters for the workspace be sure to set the web service to Data Streaming instead of Data Download:

![](./Images/Img3.208.Ex2.SelectStreamingService.png)

The result of this translation is not a streamed jpeg file. Instead, the translation returns a zip file:

![](./Images/Img3.209.Ex2.StreamedZipFile.png)

If you open the zip file you'll see that it includes both a jpeg file and a wld (World) file. That's why FME returned a zip file. It will zip the results of a Data Streaming service whenever the result is multiple files.


<br>**4) Turn off World File Creation**
<br>To really stream the data we should turn off the world file creation in the workspace. Check the properties for the JPEG Writer's feature type and set the Generate World File parameter to No:

![](./Images/Img3.210.Ex2.TurnOffWorldFile.png)


<br>**5) Publish and Run Workspace**
<br>Re-publish the workspace and run it on FME Server. You should find that the results of the translation are returned as a streamed jpeg file. Most likely it will open directly in your web browser:

![](./Images/Img3.211.Ex2.JPEGOpenedInBrowser.png)

---

<!--Exercise Congratulations Section--> 

<table style="border-spacing: 0px">
<tr>
<td style="vertical-align:middle;background-color:darkorange;border: 2px solid darkorange">
<i class="fa fa-thumbs-o-up fa-lg fa-pull-left fa-fw" style="color:white;padding-right: 12px;vertical-align:text-top"></i>
<span style="color:white;font-size:x-large;font-weight: bold;font-family:serif">CONGRATULATIONS</span>
</td>
</tr>

<tr>
<td style="border: 1px solid darkorange">
<span style="font-family:serif; font-style:italic; font-size:larger">
By completing this exercise you have learned how to:
<br>
<ul><li>Set up a workspace for use in a Data Streaming service</li>
<li>Published a workspace to the Data Streaming service</li></ul>
</span>
</td>
</tr>
</table>   