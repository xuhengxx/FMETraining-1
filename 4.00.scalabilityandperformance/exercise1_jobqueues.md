# 练习1：作业队列

|  练习1 |  作业队列 |
| :--- | :--- |
| 数据 | N / A |
| 总体目标 | 通过特定的FME引擎发送作业 |
| 演示 | 创建作业队列并将作业分配给队列 |
| 启动工作空间 | 无 |
| 结束工作空间 | C:\FMEData2018\Workspaces\ServerAdmin\Scalability-Ex1-JobQueues-Complete.fmw |

您的GIS部门全部使用FME Server并使用Web界面转换作业，但作业始终排队，即使是快速转换。您想知道是否有办法将其中一个FME服务器引擎留出来进行快速转换，这样您和您的技术分析师就不必等待太长时间来完成较小的工作。使用作业队列，您可以将特定引擎分配给特定任务。

  
**1）创建作业队列**  
在FME Server Web界面中创建作业队列。

登录FME Server Web界面，然后在左侧栏中选择**管理&gt;引擎和许可&gt;配置**。

向下滚动到“引擎和许可”页面的底部，然后选择“ **创建队列”**。

![](https://github.com/xuhengxx/FMETraining-1/blob/Server-Admin-2018/ServerAdmin4Scalability/Images/4.201.Ex1.Create_JobQueue.png)

将其命名为_快速转换_，然后单击OK。

  
**2）分配FME引擎**  
现在已经创建了作业队列，可以将特定的FME引擎 - 和库 - 分配给队列。

单击_编辑按钮_。为作业队列提供“FME Server Engine for Quick Translations”的描述，然后从Engines的下拉选项中选择**&lt;localhost&gt; \_Engine1**。

接下来，将作业优先级指定为1。

![](https://github.com/xuhengxx/FMETraining-1/blob/Server-Admin-2018/ServerAdmin4Scalability/Images/4.202.Ex1.JobQueue_SelectEngine.png)

要保存编辑，请再次单击编辑按钮。

  
**3）创建FME工作空间**  
要确认作业队列是否正常运行，我们可以在FME Server中运行指定_快速转换_队列的工作空间。在本练习中，我们不需要复杂的工作空间，只需要运行的作业。

打开FME Workbench并创建一个新的空白工作空间。

添加**Creator**转换器并将其连接到**Logger**转换器。

![](https://github.com/xuhengxx/FMETraining-1/blob/Server-Admin-2018/ServerAdmin4Scalability/Images/4.203.Ex1.JobQueue_Workspace.png)

  
**4）发布到FME Server**  
通过从FME Workbench的File菜单中选择**Publish to FME Server**，将工作空间**发布到FME Server**：

![](https://github.com/xuhengxx/FMETraining-1/blob/Server-Admin-2018/ServerAdmin4Scalability/Images/4.204.Ex1.PublishToServer.png)

在“发布到FME服务器向导”中提示时，连接到FME Server，然后将工作空间发布到：

* **仓库名称：**Training
* **工作空间名称：** JobQueue\_TestJob.fmw
* **服务：**Job Submitter

|  Vector小姐说...... |
| :--- |
|  如果您已完成Configure for HTTPS练习，请记住，连接到FME Server的URL现在是https：// localhost：8443 / fmeserver而不是http：// localhost / fmeserver！ |

  
**5）在作业队列中分配和运行工作空间**  
返回FME Server Web界面，一旦发布到FME Server，就可以运行**JobQueue\_TestJob**工作空间并设置Job Queue参数。

在FME Server Web界面的左侧栏中选择_“运行工作空间”_。

在“运行工作空间”页面上，填写如下参数：

* **仓库：**Training
* **工作空间：** JobQueue\_TestJob

接下来，展开“ 运行工作空间”页面上的“ **高级”**选项。将_Job Queues_参数设置为**QuickTranslations**（步骤1中创建的队列的名称）：

![](https://github.com/xuhengxx/FMETraining-1/blob/Server-Admin-2018/ServerAdmin4Scalability/Images/4.205.Ex1.RunWorkspace_JobQueue.png)

单击**“**运行工作空间”页面底部的“运行”。

  
**6）验证作业队列配置**  
您希望确保作业已路由到正确的引擎而不仅仅是第一个可用的引擎。

在FME Server Web界面的左侧栏中，选择“ **作业”&gt;“已完成”**。

选择刚刚运行的工作空间以打开“ _作业详细信息”_页面。

单击以展开“ **请求数据（Request Data）”**部分。在**queue**参数旁边，您将看到指定作业队列的名称：

![](https://github.com/xuhengxx/FMETraining-1/blob/Server-Admin-2018/ServerAdmin4Scalability/Images/4.206.Ex1.VerifyJobQueue_Success.png)

返回“ _作业”&gt;“已完成”_以验证作业是否已发送到正确的引擎。

![](https://github.com/xuhengxx/FMETraining-1/blob/Server-Admin-2018/ServerAdmin4Scalability/Images/4.207.Ex1.CompletedJobQueue.png)

在测试时，您可以考虑多次提交作业以进行额外的验证步骤，并且安心，但这当然不是必要的！

<table>
  <thead>
    <tr>
      <th style="text-align:left">恭喜！</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p>通过完成本练习，您已学会如何：
          <br />
        </p>
        <ul>
          <li>创建作业队列</li>
          <li>通过特定引擎成功路由作业</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>
