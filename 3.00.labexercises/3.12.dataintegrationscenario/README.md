# 数据集成场景

|  |  数据集成场景 |
| :--- | :--- |
| 数据 | 温哥华市开放数据（见下表） |
| 总体目标 | 使用您的FME技能整合来自多个来源的数据以回答问题。 |
| 演示 | 内容转换，结构转换，模式编辑 |
| 启动工作空间 | C:\FMEData2018\Workspaces\DataIntegration\ScenarioBegin.fmw  |
| 结束工作空间 | 教师可以要求访问的最后工作空间 [在这里](https://goo.gl/forms/jWeso3OY6RVe6PJG3)。 |

## 介绍

在之前的练习中，您学习了如何使用FME转换和变换数据。现在让我们使用这些知识吧！正如我们在[讲座部分](https://github.com/safesoftware/FMETraining/blob/FME-Desktop-Data-Integration-2018/Integration3LabExercises/..%5CIntegration1Lecture%5C1.00.Lecture.md)所述，数据集成是现代组织的关键要求。在本练习中，您将开发一个工作空间，以解决城市政府场景中的数据集成问题。

您会：

* 检查您的数据
* 合并您的数据集
* 查询您的数据以回答问题或解决问题
* 回答有关整合数据过程的实验室问题

本练习将提供将三个数据集集成到中央数据库的示例。之后，您可以按照类似的步骤选择一个额外的数据集来回答另一个问题。如果您在执行这些步骤时遇到问题，可以参考 [“附加程序”](https://github.com/safesoftware/FMETraining/blob/FME-Desktop-Data-Integration-2018/Integration3LabExercises/..%5CIntegration3LabExercises%5C3.14.AdditionalProcedures.md)部分，FME Workbench帮助（也可在我们的[文档](https://support.safe.com/KnowledgeDocumentation)中在线获取）或社区[知识中心](https://knowledge.safe.com/)。

请继续参考[实验室问题](https://github.com/safesoftware/FMETraining/blob/FME-Desktop-Data-Integration-2018/Integration3LabExercises/..%5CIntegration3LabExercises%5C3.15.LabQuestions.md)，因为有些问题涉及场景。

## 练习目标

* 使用单个写模块上的多个要素类型将数据集成到单个数据库中
* 使用转换器在目标数据库中创建所需的模式。
* 使用Overlayer转换器合并数据
* 使用ChartGenerator进行分析整体数据
* 选择另一个数据集并将其添加到工作空间以回答问题。

## 检查数据

首先，检查您给出的数据。有各种各样的主题和格式可供选择。按照[练习3](https://github.com/safesoftware/FMETraining/blob/FME-Desktop-Data-Integration-2018/Integration3LabExercises/..%5CIntegration3LabExercises%5C3.04.Exercise3.md)的说明，在FME Data Inspector中打开其中一些文件，以查看它们具有的属性。

在本演练中，我们将使用以下数据集:

* 自行车路径
* 街区
* 公共艺术品

更多数据可从[温哥华市开放数据目录中获得](http://data.vancouver.ca/datacatalogue/index.htm)。

| 主题 | 格式 | 位置（FMEData2018\Data...） |
| :--- | :--- | :--- |
| 地址 | Esri地理数据库 | Addresses\Addresses.gdb |
| 建筑足迹 | SpatialLite数据库或AutoCAD DWG | Engineering \ BuildingFootprints \ building\_footprints.sl3或C：\ FMEData2018 \ Data \ Parcels \ BuildingFootprints.dwg |
| 自行车路径 | Esri Shapefile | Transportation\Cycling\BikePaths\*.shp |
| 商业许可证 | Excel电子表格 | Planning\BusinessLicenses.xlsx |
| 城市网格 | 地理标记语言 | Boundaries\CityGrid.gml |
| 城市物业 | Esri Shapefile | Parcels\CityProperties\CityProperties.shp |
| 沿海地带 | 地理标记语言 | Boundaries\CoastalZones\CoastalZones.gml |
| 社区资源 | Esri地理数据库 | CommunityMapping \ CommunityMap.gdb |
| 犯罪 | 逗号分隔值 | Emergency\Crime.csv |
| 饮用喷泉 | 逗号分隔值 | Engineering\DrinkingFountains.csv |
| 选举结果 | Excel电子表格 | Elections\ElectionResults.xls |
| 选举投票区 | 地理标记语言 | Elections\ElectionVoting.gml |
| 海拔 | 数字高程模型 | ElevationModel \ DEM-Full.dem |
| 划分区域的消防站 | 地理标记语言 | Emergency\FireHallsWithZones.gml |
| 转发分拣区域（用于邮政编码） | Esri Shapefile | Addresses\ForwardSortationAreas.shp |
| 陆地边界 | Esri Shapefile | Boundaries\LandBoundary\VancouverLandBoundary.shp |
| 街区 | Google Keyhole标记语言 | Boundaries\VancouverNeighborhoods.kml |
| 正射影像\(校正比例航空照片\) | TIFF | Orthophotos\*.tif |
| 包裹 | AutoCAD DWG | Parcels\Parcels.dwg |
| 停车场计价表 | MapInfo TAB | Transportation\Parking\Meters.tab |
| 停车票 | 逗号分隔值 | Transportation\Parking\ParkingTickets.csv |
| 公园 | MapInfo TAB | Parks\Parks.tab |
| 规划限制（商业改善区，历史区域，噪声控制区域和视锥） | OCG Geopackage | Planning\PlanningRestrictions.gpkg |
| 点云（LiDAR） | LAS | PointClouds\CoV\*.laz |
| 公共艺术品 | Excel电子表格 | Culture\PublicArt.xlsx |
| 公共树木 | 逗号分隔值 | Parks\Parks.tab |
| 道路 | AutoCAD DWG或Microstation DGN | Transportation\CompleteRoads.dwg or RoadsDGN.dgn |
| 街道照明 | AutoCAD DWG和Microstation DGN | Engineering\StreetLighting.dwg和StreetLightingDGN.dgn |
| 交通信号 | AutoCAD DWG和Microstation DGN | Engineering \ TrafficSignals.dwg和TrafficSignalsDGN.dgn |
| 分区 | MapInfo TAB | Zoning\Zones.tab |
| 分区描述 | Adobe PDF | Zoning\ZoneDescriptions.pdf |

