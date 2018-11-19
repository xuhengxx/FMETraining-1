# 练习1.3：每日数据库更新：共享和定时

|  练习1.3 |  每日数据库更新：共享和定时 |
| :--- | :--- |
| 数据 | 消防站Firehalls（GML） 街区Neighborhoods（KML） |
| 总体目标 | 创建工作空间以读取和处理部门数据并将其发布到FME Server |
| 演示 | 在FME Server中共享和定时转换 |
| 启动工作空间 | 无 |
| 结束工作空间 | 无 |

您已经（在练习1和练习2中）创建了一个工作空间来执行此转换，将其发布到FME Server，并运行它以确认它是否有效。

作为日常任务，您定时在下班后每天运行转换。但是...如果你不在那里或早退，或其他人迟到，会发生什么。谁会运行它呢到时？

首先，您应该确保其他用户可以访问工作空间来运行它，但您也可以将其设置为以自动定时运行。

  
**1）连接到服务器**  
浏览到FME Server界面的登录页面，方法是通过开始菜单上的Web 界面选项启动它，或者如果您已经登录则注销。

这次，使用通用用户帐户登录，该帐户是任何FME Server安装上的默认帐户。用户名是_**user**_，密码也是_**user**_！

您会注意到的第一件事是该帐户的菜单和功能受到更多限制：

[![](../.gitbook/assets/img1.227.ex3.usermenu.png)](https://github.com/xuhengxx/FMETraining-1/tree/f1cdae5373cf9425ee2d148732792713c9043d44/ServerAuthoring1Basics/Images/Img1.227.Ex3.UserMenu.png)

实际上，如果您尝试运行一个工作空间，您会发现这个帐户能够访问的惟一仓库是sample仓库;不是现有工作空间所在的Training仓库:

[![](../.gitbook/assets/img1.228.ex3.userrepository.png)](https://github.com/xuhengxx/FMETraining-1/tree/f1cdae5373cf9425ee2d148732792713c9043d44/ServerAuthoring1Basics/Images/Img1.228.Ex3.UserRepository.png)

  
**2）共享仓库**  
注销用户帐户并以管理员身份（admin / admin）重新登录。

现在，您拥有完整的菜单条目集，单击菜单上的“仓库”。在仓库列表下，找到Training仓库。单击右侧的“共享”图标：

[![](../.gitbook/assets/img1.229.ex3.sharebutton.png)](https://github.com/xuhengxx/FMETraining-1/tree/f1cdae5373cf9425ee2d148732792713c9043d44/ServerAuthoring1Basics/Images/Img1.229.Ex3.ShareButton.png)

在“共享选项”对话框中，选择fmeuser作为要共享的角色，并允许它们运行工作空间：

[![](../.gitbook/assets/img1.230.ex3.sharedialog.png)](https://github.com/xuhengxx/FMETraining-1/tree/f1cdae5373cf9425ee2d148732792713c9043d44/ServerAuthoring1Basics/Images/Img1.230.Ex3.ShareDialog.png)

通过选择_fmeuser_角色（而不是单个_user_帐户），我们允许任何被标记为用户的人访问工作空间; 并且只允许它们运行，我们阻止它们下载并对我们的工作空间进行编辑。

  
**3）检查共享**  
退出管理员帐户并使用用户帐户（user/user）重新登录到FME Server。

这一次，您应该可以访问Training仓库。单击“运行工作空间”，在“Training ”仓库中选择您的工作空间并运行它。检查“已完成的作业”页面，当工作空间以用户身份运行时，您将看到该工作空间的一个条目。检查“作业”页面，当工作空间以用户身份运行时，您将看到该工作空间的一个条目。只有一个条目，因为用户没有查看任何其他用户作业所需的权限：

[![](../.gitbook/assets/img1.231.ex3.completedjobuser.png)](https://github.com/xuhengxx/FMETraining-1/tree/f1cdae5373cf9425ee2d148732792713c9043d44/ServerAuthoring1Basics/Images/Img1.231.Ex3.CompletedJobUser.png)

再次注销并以管理员身份重新登录。现在，在Jobs \| Completed 窗口，您应该能够看到管理员的工作和用户的工作

[![](../.gitbook/assets/img1.232.ex3.multiuserjobslist.png)](https://github.com/xuhengxx/FMETraining-1/tree/f1cdae5373cf9425ee2d148732792713c9043d44/ServerAuthoring1Basics/Images/Img1.232.Ex3.MultiUserJobsList.png)

这是因为管理员组确实有权查看所有作业。

  
**4）创建测试定时**  
现在我们允许其他用户按需运行工作空间，但我们也应该将转换设置为按定时运行。

首先，为了确认调度确实有效，让我们设置一个测试定时。单击菜单上的“定时”，然后在“定时”页面中，单击“新建”按钮以启动该过程。

设置测试定时的名称，并通过在“类别”字段中键入“培训\(Training\)”将其添加到“培训\(Training\)”类别：

[![](../.gitbook/assets/img1.233.ex3.newschedule.png)](https://github.com/xuhengxx/FMETraining-1/tree/f1cdae5373cf9425ee2d148732792713c9043d44/ServerAuthoring1Basics/Images/Img1.233.Ex3.NewSchedule.png)

对于时间设置，将定时设置为立即启动并每30秒运行一次。取消选中Schedule Is Not Expire旁边的复选框，并将结束时间设置为未来后约30分钟（这样的话，如果我们忘记取消定时安排，它不会永远持续下去!）

[![](../.gitbook/assets/img1.234.ex3.setschedule.png)](https://github.com/xuhengxx/FMETraining-1/tree/f1cdae5373cf9425ee2d148732792713c9043d44/ServerAuthoring1Basics/Images/Img1.234.Ex3.SetSchedule.png)

请注意，时间以24小时格式给出，因此1:30表示AM，13：30表示PM。同样重要的是要注意，此时间是运行连接到FME Server的Web浏览器的计算机的本地时间。如果您的FME服务器位于与您正在访问FME Server的计算机不同时区的计算机上，请记住这一点。

在“工作空间设置”下，选择“Training库”，然后选择之前上载的工作空间（Basics-Ex1-Complete.fmw）：

[![](../.gitbook/assets/img1.235.ex3.newscheduleworkspace.png)](https://github.com/xuhengxx/FMETraining-1/tree/f1cdae5373cf9425ee2d148732792713c9043d44/ServerAuthoring1Basics/Images/Img1.235.Ex3.NewScheduleWorkspace.png)

我们不需要为此工作空间更改任何用户参数，因此可以忽略任何用户参数。

现在单击“确定”以添加新定时。

  
**5）检查作业页面**  
打开“作业”页面。将打开以前运行的作业列表。您将发现\(如果设置正确\)将有一些作业正在以定时运行:

[![](../.gitbook/assets/img1.236.ex3.newschedulejobs.png)](https://github.com/xuhengxx/FMETraining-1/tree/f1cdae5373cf9425ee2d148732792713c9043d44/ServerAuthoring1Basics/Images/Img1.236.Ex3.NewScheduleJobs.png)

请注意，用户名设置为admin; 因为那是创建定时的用户，即用于运行作业的用户名。

  
**6）创建实际定时**  
现在我们确信我们知道如何使用界面，让我们设置实际定时。我们希望工作空间在一周中的每一天都运行。也应该没有结束日期。

因此，请返回“定时”页面。您现在可以：

* 单击测试定时并将其编辑为所需的值
* 删除测试定时并创建具有所需值的新定时

[![](../.gitbook/assets/img1.237.ex3.changedschedule.png)](https://github.com/xuhengxx/FMETraining-1/tree/f1cdae5373cf9425ee2d148732792713c9043d44/ServerAuthoring1Basics/Images/Img1.237.Ex3.ChangedSchedule.png)

此设置将在每天晚上8:00运行工作空间。别忘了单击“确定”按钮！

您可能希望在此培训期间定期检查以确保工作空间按预期运行。

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
          <li>在FME Server中共享一个仓库，并进行测试，以确保它对正确的用户可用</li>
          <li>在FME Server中定时安排转换</li>
          <li>检查作业历史记录以确保进行定时的转换</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>
