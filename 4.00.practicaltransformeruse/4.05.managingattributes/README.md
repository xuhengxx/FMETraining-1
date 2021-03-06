# 管理属性

前30个转换器中的很大一部分是用于管理属性的支持类转换器。这些转换器创建新属性，重命名它们，设置值并删除它们。

这些转换器的关键用途是重命名模式映射的属性。

## 属性管理转换器

主要的属性管理任务和可以使用的转换器如下：

|  任务 |  转换器 |
| :--- | :--- |
| 创建属性 | AttributeCreator，AttributeManager |
| 设置属性值 | AttributeCreator，AttributeManager |
| 删除属性 | AttributeKeeper，AttributeManager，AttributeRemover，BulkAttributeRemover |
| 重命名属性 | AttributeManager，AttributeRenamer，BulkAttributeRenamer |
| 复制属性 | AttributeCopier，AttributeCreator，AttributeManager |
| 排序属性 | AttributeManager |
| 更改属性大小写 | BulkAttributeRenamer |
| 添加前缀/后缀 | BulkAttributeRenamer |

这些转换器中的许多都能执行类似的操作，您可以看到AttributeManager完成了许多任务，您几乎可以完全使用它。

|  警告 |
| :--- |
|  不要误解BulkAttributeRenamer。它改变大小写 - 或者添加后缀/前缀 - 作用于属性**名称**，而不是属性值。 |

## 列表

FME中的_**列表**_是一种机制，允许每个属性有多个值。因此，在属性_myAttribute_只能包含单个值的情况下，列表属性_myList{}.myAttribute_可以包含多个值：

```text
myList{0}.myAttribute
myList{1}.myAttribute
myList{2}.myAttribute
```

例如，表示森林区域的单个多边形可能具有list属性来记录该区域中包含的树种：

```text
TreeList{0}.Species = Oak
TreeList{1}.Species = Chestnut
TreeList{2}.Species = Ash
```

各种转换器可以创建列表，其他转换器包括对列表的支持，并且有些转换器专门用于列表属性（例如ListSorter）。

有关进一步阅读，请查看Safe Software博客上[**有关属性管理**](https://blog.safe.com/2015/11/fmeevangelist141/)的文章。

