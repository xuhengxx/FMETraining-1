# 练习：洪水风险评估

<table>
<tr>
<td>
<font style="vertical-align: inherit;">
练习2
</font></td>
<td><font style="vertical-align: inherit;">
洪水风险项目
</font></td>
</tr>
<tr>
<td><font style="vertical-align: inherit;">数据</font></td>
<td><font style="vertical-align: inherit;">公园（MapInfo TAB）</font></td>
</tr>
<tr>
<td><font style="vertical-align: inherit;">总体的目标</font></td>
<td><font style="vertical-align: inherit;">根据海拔和海岸距离评估地址的洪水风险</font></td>
</tr>
<tr>
<td><font style="vertical-align: inherit;">演示</font></td>
<td><font style="vertical-align: inherit;">条件属性值</font></td>
</tr>
<tr>
<td><font style="vertical-align: inherit;">启动工作空间</font></td>
<td><font style="vertical-align: inherit;">C:\FMEData2018\Workspaces\DesktopAdvanced\Attributes-Ex2-Begin.fmw</font></td>
</tr>
<tr>
<td><font style="vertical-align: inherit;">结束工作空间</font></td>
<td><font style="vertical-align: inherit;">C:\FMEData2018\Workspaces\DesktopAdvanced\Attributes-Ex2-Complete.fmw</font></td>
</tr>
</table>

一位同事正在研究工作空间，以计算该市所有地址的海啸洪水风险。风险被判定为靠近海岸线和海拔高度的组合，并使用此表计算：

<table>
<tr><td></td><td></td><td colspan="3"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">海拔（海拔米数）</font></font></td></tr>
<tr><td></td><td></td><td align="center"><font style="vertical-align: inherit;">0-10m</font></td><td align="center"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">10-25m</font></td><td align="center"><font style="vertical-align: inherit;">25-60m</font></td></tr>
<tr><td rowspan="3"><font style="vertical-align: inherit;">距离海岸线（米）的距离</font></td><td align="center"><font style="vertical-align: inherit;">100米</font></td><td align="center"><font style="vertical-align: inherit;">1</font></td><td align="center"><font style="vertical-align: inherit;">2</font></td><td align="center"><font style="vertical-align: inherit;">3</font></td></tr>
<tr><td align="center"><font style="vertical-align: inherit;">200米</font></td><td align="center"><font style="vertical-align: inherit;">2</font></td><td align="center"><font style="vertical-align: inherit;">3</font></td><td align="center"><font style="vertical-align: inherit;">4</font></td></tr>
<tr><td align="center"><font style="vertical-align: inherit;">300米</font></td><td align="center"><font style="vertical-align: inherit;">3</font></td><td align="center"><font style="vertical-align: inherit;">4</font></td><td align="center"><font style="vertical-align: inherit;">5</font></td></tr>
</table>

您的同事已创建工作空间，直到每个点上的地址都有一个海拔高度和距离海岸线的距离为止。现在需要开始计算，他已经请求你帮助完成项目。

  
**1）启动Workbench**  
打开工作空间C：\ FMEData2018 \ Workspaces \ DesktopAdvanced \ Attributes-Ex2-Begin.fmw。这是您的同事到目前为止创建的工作空间。

要找出我们正在处理的数据，请运行工作空间，然后检查各个部分的结果。您可以使用Inspector转换器或要素缓存来执行此操作。

您可能希望检查源要素类型（或Reprojector，因为CDED数据是不同的坐标系）。您还需要检查AttributeRenamer输出。

不要忘记您可以在Inspector的参数中设置Group-By，这可能有助于可视化哪个地址在哪个区域中。

![](../../Images/Img1.218.Ex2.InitialDataProcessed.png)

您将看到如何为地址分配一个区域，表示它们与海岸线的距离，并且还具有海拔。

---

| 分析师女士说...... |
| :--- |
| 在我们完成练习的全套说明之前，请尝试考虑如何执行此任务。你需要考虑：<br><br><ul><li>数据可以直接映射到洪水风险，还是需要先过滤？</li></ul>该区域相当容易映射，因为它是固定值（100,200和300）。然而，海拔是棘手的，因为它们不是固定值; 海拔可以是0到60之间的任何单个值。<br><br><ul><li>你会用哪种转换器？</li></ul>要过滤数据，Tester和TestFilter转换器是最明显的候选者，可能才用AttributeRangeFilter; 来映射数据，亦或AttributeValueMapper或AttributeRangeMapper。或者，为什么不使用带有条件属性的AttributeManager？<br><br><ul><li>你应该结合方法吗？</li></ul>也许组合方法效果最好，您可以部分过滤数据然后映射它？如果是这样，您过滤哪些数据并使用哪些转换器？<br><br><ul><li>哪个会产生最美观（好看）的工作空间？</li></ul>最佳实践应始终在任何工作空间中发挥作用。如果有多种解决方案，那么哪种解决方案能产生最美观（美观）的工作空间？更少的转换器总是更好，还是会影响维护工作空间的需求？  |

---

| Vector小姐说...... |
| :--- |
| 经过考虑，我看到了实施这个项目的三种可能方式。我叫它们：<br><br><ul><li>简单过滤（简单但笨重）</li><li>复杂过滤（复杂性和大小都适中）</li><li>条件值（复杂但紧凑）</li></ul><br>“简单过滤”过滤数据，然后将其映射到所需的值; 因此，这是一个两步过程。它需要更多的转换器，但更容易理解和设置。<br><br>“复杂过滤”只需一步即可过滤数据，因此无需进一步映射。这是一个单步过程，但是 - 因为数据被过滤 - 需要比常备数更多的转换器。它中等复杂<br><br>“条件值”根据一组内置条件直接设置值。所有工作都可以在一个转换器中完成，因此结构紧凑，但设置和维护要复杂得多。<br><br>在接下来的几页中，我们将详细介绍如何设置每个方法。选择您要尝试的项目并按照说明操作。或者，依次进行 - 然后您将能够比较不同的方法并确定您认为哪种方法最好。<br><br><br>**注意！**请务必检查过滤转换器中AND和OR的使用。很容易弄错，但很难跟踪原因！  |
