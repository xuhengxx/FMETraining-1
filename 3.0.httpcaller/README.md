### 第3章.使用HTTP调用程序来调用服务器

现在您已了解REST API是什么以及调用和响应如何工作; 是时候开始与FME Server进行交互了。

出于本培训课程的目的，我们将使用名为Postman的外部工具，可在此处下载：[https://www.getpostman.com/apps](https://www.getpostman.com/apps) _\(这已经在培训计算机上）_。

如果您熟悉另一个REST客户端工具，则可以使用它作为替代方法，但本手册中的说明将参考Postman接口。

---

#### 为什么要使用REST客户端工具？

REST客户端是练习调用的媒介。客户端接受REST调用，并将直接与FME Server通信。用户使用REST客户端工具有几个原因：

* 易于使用的界面来输入调用
* 可以保存调用并稍后使用
* 可以从调用中生成代码片段用于应用程序

---

|  Ricky RESTless说... |
| :--- |
|  我使用Postman测试调用，然后在FME Workbench的HTTPCaller转换器中使用它们。通过在FME Workbench中使用REST API调用，我可以自动执行许多FME Server进程。 |

