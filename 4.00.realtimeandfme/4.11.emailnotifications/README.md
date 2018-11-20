# 电子邮件通知

通过详细介绍电子邮件通知非常重要，因为它们是FME Server上最常用的通知类型之一。

“电子邮件”是发布和订阅组件可以使用的协议。电子邮件发布从外部客户端接收传入电子邮件，电子邮件订阅发送传出电子邮件

## 电子邮件协议

实际上，电子邮件不是单一协议。存在几种协议（电子邮件传输方法）。FME Server支持以下两种与电子邮件相关的协议：**SMTP**和**IMAP**。

SMTP（简单邮件传输协议）是通过FME Server内置的电子邮件服务器直接接收电子邮件，或通过SMTP服务间接发送电子邮件的功能，例如Gmail帐户。

IMAP（Internet消息访问协议）是一种间接过程，可连接到其他服务器上的电子邮件帐户。当该帐户收到电子邮件时，IMAP协议会将其传递给FME Server。
