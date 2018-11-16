# 练习3.2：数据流系统

|  练习2 |  数据流系统 |
| :--- | :--- |
| 数据 | 正射影像（GeoTIFF） |
| 总体目标 | 为正射影像创建FME服务器数据流系统 |
| 演示 | 数据流 |
| 启动工作空间 | C:\FMEData2018\Workspaces\ServerAuthoring\SelfServe1-Ex2-Begin.fmw |
| 结束工作空间 | C:\FMEData2018\Workspaces\ServerAuthoring\SelfServe1-Ex2-Complete.fmw |

作为一个城市的GIS部门的技术分析师，您刚刚创建了一个系统，允许其他部门下载正射影像数据，而不是要求您为他们创建它。

有时最终用户将数据下载为JPEG只是为了在浏览器或图像查看器中打开它来检查它。您意识到，在这种情况下，他们可能能够使用数据流服务，而不是数据下载。

  
**1）打开工作空间**  
从练习1或上面列出的开始工作空间打开工作空间。

  
**2）发布到FME服务器**  
  
将工作空间重新发布到FME Server。

在发布向导的最后一个对话框中，选中复选框以使用数据下载和数据流注册工作空间（但不要单击“完成”）：

[![](../.gitbook/assets/img3.205.ex2.publishtostreamservice.png)](https://github.com/xuhengxx/FMETraining-1/tree/f1cdae5373cf9425ee2d148732792713c9043d44/ServerAuthoring3SelfServeBasics/Images/Img3.205.Ex2.PublishToStreamService.png)

单击Data Streaming服务的Edit按钮。确保服务正在使用JPEG写模块的输出（现在我们将数据流限制为JPEG格式）：

[![](../.gitbook/assets/img3.206.ex2.streamingparameters.png)](https://github.com/xuhengxx/FMETraining-1/tree/f1cdae5373cf9425ee2d148732792713c9043d44/ServerAuthoring3SelfServeBasics/Images/Img3.206.Ex2.StreamingParameters.png)

  
**3）运行工作空间**  
在FME Server Web界面中找到新发布的工作空间并运行它。在工作空间的参数中，请确保将Web服务设置为数据流而不是数据下载

[![](../.gitbook/assets/img3.207.ex2.selectstreamingservice.png)](https://github.com/xuhengxx/FMETraining-1/tree/f1cdae5373cf9425ee2d148732792713c9043d44/ServerAuthoring3SelfServeBasics/Images/Img3.207.Ex2.SelectStreamingService.png)

此转换的结果不是流式JPEG文件。相反，转换返回一个zip文件：

[![](../.gitbook/assets/img3.208.ex2.streamedzipfile.png)](https://github.com/xuhengxx/FMETraining-1/tree/f1cdae5373cf9425ee2d148732792713c9043d44/ServerAuthoring3SelfServeBasics/Images/Img3.208.Ex2.StreamedZipFile.png)

如果您打开zip文件，您会看到它包含JPEG文件和wld（World）文件。这就是FME返回一个zip文件的原因。只要结果是多个文件，它就会压缩数据流服务的结果。

|  2018.1的新变化 |
| :--- |
|  额外的World文件不再影响2018.1中的数据流。如果您正在FME Server 2018.1+上完成此练习，那么如果数据按预期流式传输，您可以在此处结束。如果您收到了下载文件，请继续执行步骤4。 |

  
**4）关闭世界文件创建**  
  
要真正流式传输数据，我们应该关闭工作空间中的世界文件创建。检查JPEG写模块的要素类型的属性，并将Generate World File参数设置为No：

[![](../.gitbook/assets/img3.209.ex2.turnoffworldfile.png)](https://github.com/xuhengxx/FMETraining-1/tree/f1cdae5373cf9425ee2d148732792713c9043d44/ServerAuthoring3SelfServeBasics/Images/Img3.209.Ex2.TurnOffWorldFile.png)

  
**5）发布和运行工作空间**  
  
重新发布工作空间并在FME Server上运行它。您应该会发现转换结果将作为流式JPEG文件返回。很可能它会直接在您的网络浏览器中打开：

[![](../.gitbook/assets/img3.210.ex2.jpegopenedinbrowser.png)](https://github.com/xuhengxx/FMETraining-1/tree/f1cdae5373cf9425ee2d148732792713c9043d44/ServerAuthoring3SelfServeBasics/Images/Img3.210.Ex2.JPEGOpenedInBrowser.png)

<table>
  <thead>
    <tr>
      <th style="text-align:left">恭喜</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p>通过完成本练习，您已学会如何：
          <br />
        </p>
        <ul>
          <li>设置工作空间以在数据流服务中使用</li>
          <li>将工作空间发布到数据流服务</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>