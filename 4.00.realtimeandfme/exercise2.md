|  练习4.2 |  建筑物更新通知系统 |
| :--- | :--- |
| 数据 | 建筑物占地面积（Esri Shapefile） |
| 总体目标 | 对数据库的实时更新 |
| 演示 | 运行工作空间以响应通知 |
| 启动工作空间 | 无 |
| 结束工作空间 | C:\FMEData2018\Workspaces\ServerAuthoring\RealTime-Ex2-Complete.fmw |

作为GIS部门的技术分析师，您已经意识到将手动更新推送到公司数据库的相关开销。阅读完FME Server中的通知后，您认为应该可以设置一个自动执行此过程的系统。

到目前为止，您已经设置了一个系统，用于添加要由FME Server注册的文件通知。现在，您必须创建一个工作空间来处理这些工作空间并将其发布到FME Server。然后，必须通过通知主题触发工作空间。

|  Vector小姐说...... |
| :--- |
|  这个练习在练习1结束的地方继续。你必须完成练习1才能进行这个练习。 |

  
**1）创建工作空间**  
启动FME Workbench并从空工作空间开始。只需添加一个Creator和Logger转换器：

[![](../.gitbook/assets/img4.408.ex2.initialworkspace.png)](https://github.com/xuhengxx/FMETraining-1/tree/f1cdae5373cf9425ee2d148732792713c9043d44/ServerAuthoring4RealTime/Images/Img4.408.Ex2.InitialWorkspace.png)

这将为我们提供一个工作空间来响应新文件; 虽然还没有做多少。我们只是创建它来检查我们是否可以使设置正常工作。

  
**2）保存并发布工作空间**  
保存工作空间并将其发布到FME Server。我们只需要运行它（不做任何特殊操作），所以只能使用Job Submitter服务注册它。

  
**3）创建订阅**  
返回到FME Server Web界面并导航到“通知”页面。单击“订阅”选项卡，然后单击“新建”以创建新的订阅。

调用订阅“Process Building Updates”。订阅ShapeIncomingFile主题：

[![](../.gitbook/assets/img4.409.ex2.createsubscription1.png)](https://github.com/xuhengxx/FMETraining-1/tree/f1cdae5373cf9425ee2d148732792713c9043d44/ServerAuthoring4RealTime/Images/Img4.409.Ex2.CreateSubscription1.png)

现在将协议设置为FME Workspace并选择上一步中上传的工作空间：

[![](../.gitbook/assets/img4.410.ex2.createsubscription2.png)](https://github.com/xuhengxx/FMETraining-1/tree/f1cdae5373cf9425ee2d148732792713c9043d44/ServerAuthoring4RealTime/Images/Img4.410.Ex2.CreateSubscription2.png)

单击“确定”以创建订阅。每次传入的Shape数据集触发ShapeIncomingFile主题时，这将导致工作空间运行。

  
**4）测试订阅**  
在Windows资源管理器中，压缩update002.shp / .dbf / .shx / .prj文件。然后返回FME Server，通过上传update002.zip文件测试订阅。

_**注意：**_ _由于我们将目录监视设置为仅监视新文件，因此上传的Shapefile应与第一个不同 - 或者至少具有不同的名称。_

这一次，不是监视主题（虽然它会再次出现），请检查“作业”页面。您应该看到已运行工作空间以响应新文件：

[![](../.gitbook/assets/img4.411.ex2.joblogshowingtriggeredworkspace.png)](https://github.com/xuhengxx/FMETraining-1/tree/f1cdae5373cf9425ee2d148732792713c9043d44/ServerAuthoring4RealTime/Images/Img4.411.Ex2.JobLogShowingTriggeredWorkspace.png)

这证明工作空间已经运行。

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
          <li>创建新的FME工作空间订阅</li>
          <li>配置订阅以运行工作空间以响应主题触发</li>
          <li>通过在“已完成的作业”页面上验证其成功来测试通知系统</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>
