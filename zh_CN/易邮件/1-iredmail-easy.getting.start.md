# iRedMail Easy: Getting start

[TOC]

!!! attention

    - 部署生成的所有账户和密码都存储在`/root/iRedMail/iRedMail.tips`文件中。
    - 如果要将现有的使用脚本部署的iRedMail版本迁移到iRedMail Easy，请查看教程[从iRedMail迁移到iRedMail Easy平台](./migrate.to.iredmail.easy.html)。

## 关于iRedMail Easy

__iRedMail Easy__ 是基于web的部署和技术支持的云端平台。通过云端部署iRedMail可以更轻松的获得升级和获得iRedMail团队快速专业的技术支持。
我们鼓励所有用户使用云端部署新的iRedMail服务器，使服务器更新更便捷迅速。
* 另请阅读[技术实践](./iredmail-easy.best.practice.html)，以了解如何使用iRedMail Easy轻松进行一键式升级。
* 阅读[发行说明](./iredmail-easy.release.notes.html)以跟踪每个发行版中的更改。
如果喜欢经典的iRedMail脚本安装程序，请阅读安装指南：[iRedMail安装](./index.html#install)。

## 系统要求

!!! 注意
    * iRedMail必须部署在全新的系统。
    * iRedMail将自动安装和配置所有必需的组件。
    * 大部分ISP运营商默认是关闭25端口的，该端口用于邮件服务器之间的通信，请和IPS运营商确认你的25端口是否开放，确保你的服务器25端口在公网上的使用的正常的，否则该服务器不能作为邮件服务器来使用。

          - Amazon AWS EC2。申请[启用25端口](https://aws.amazon.com/premiumsupport/knowledge-center/ec2-port-25-throttle/).
          - Google Cloud Platform。
          - Microsoft Azure。
          - Linode。在[博客](https://www.linode.com/blog/linode/a-new-policy-to-help-fight-spam/),
            有解释，可以申请linode解禁25端口。

### 系统版本支持

iRedMail Easy支持的系统版本：

发行版 | 版本号
--- |---
CentOS | 7, 8
Debian | 9, 10
Ubuntu | 18.04, 20.04
OpenBSD | 6.6, 6.7

如果你需要FreeBSD上安装iRedMail，请改用[安装包](https://www.iredmail.org/download.html) 进行安装。

### 硬件需求

* iRedMail服务器至少需要`2 GB`内存。
* 如果需要运行SOGo Groupware (which offers webmail, calendar (CalDAV),
  contacts (CardDAV) and ActiveSync)组件，则需要更多内存。500个ActiveSync客户端至少需要`16GB`内存。

## 登录注册

部署服务器之前，请使用真实有效的邮箱进行注册:

* [登录注册: https://easy.iredmail.org/](https://easy.iredmail.org)

注册后系统将会发生一封邮件到你的邮箱，以核实邮箱使用的有效性，请登录邮箱点击链接进行确认，确认后才可以登录云端平台。
注册后，平台将可以免费试用一个月，如果你不需要使用云端平台，可以在到期后登录平台，点击左侧属性，删除账号即可。

注册登录页面截图:

![](./images/iredmail-easy/installation/signup.png){: width="350px" }
![](./images/iredmail-easy/installation/login.png){: width="350px" }

## 添加邮件服务器

登录后，页面将自动跳转到控制台，请点击`添加邮件服务器`新增邮件服务器。
After login, you will be redirected to the `Dashboard` page, please click the
`Add a mail server` button to add a new mail server.

![](./images/iredmail-easy/installation/add_mailserver.png){: width="600px" }

新增服务器页面表单说明：

* `完整主机名 (FQDN)`：服务器主机名。
    * 它必须是全限定域名（FQDN），例如`mail.example.com，mx.example.com`。
    * 主机名（FQDN）不能作为虚拟邮件域域名(用于电子邮件的地址，如 ` user@example.com `)，主机名主要用于发送和接收系统账户如`root`的邮件。
* `IP地址`：服务器公网或者内网IP地址。
    * 如果邮件服务器使用于内部网络中，并且不能直接从外部网络访问，则需要一个跳转服务器（或堡垒机服务器），以便我们的部署服务器可以连接到您的邮件服务器。有关堡垒机的更多详细信息，请阅读此简短教程：[什么是堡垒机](./iredmail-easy.what.is.ssh.jump.server.html).
* `SSH端口号`：SSH服务端口，默认22端口。
* `SSH用户`：用于安全登录SSH的用户，默认`root`。
    * 如果使用非`root`用户，那么该用户必须是可以使用`sudo`Linux发行版上或`doas`OpenBSD发行版上权限的用户。
* `SSH密钥`：SSH Key用于登录你的邮件服务器。
    * 如果你选择`生成一个强密钥`，云端将自动生成一个强密钥(4096 bits)给你。
* `操作系统`：选择你邮件服务器的系统发行版。
* `用于实际部署的服务器`：请在列表中选择一个用于部署的服务器。
    * 部署服务器链接到您的服务器执行安装或升级，请选择离得最近的一台以便得到更快的网络连接。
    * 如果服务器位于防火墙后方，请将选择的部署服务器加入防火墙的白名单以允许连接。
* `备注`：添加文本标识，让你更方便识别邮件服务器。

单击添加邮件服务器，添加新服务器后，页面将重定向到邮件服务器配置页面。此页面旨在定制邮件服务器各种属性配置。

Click the button to create mail server, after created, page will be redirected
to mail server profile page.  You're free to update profile here.

![](./images/iredmail-easy/installation/added_mailserver.png){: width="600px" }

## 选择后端

在服务器配置页面单击`Backend`选项。
Click tab `Backend` on the mail server profile page.

iRedMail后端有两种，SQL或LDAP数据库，用于存储邮件域和帐户。我们建议选择自己熟悉的，便于维护。
A backend is a SQL or LDAP database used to store mail domains and
accounts. We suggest you choose the one you're familiar with for easier
maintenance.

![](./images/iredmail-easy/installation/backends.png){: width="700px" }

## 选择需要部署的组件

单击邮件服务器配置页的`Components`选项卡。
Click tab `Components` on the mail server profile page.

配置需要的网络服务需要配置相应的组件。在此页面上，你可以根据需求选择需要部署的组件。
A component is a software (or software group) which implements some network
service(s). On this page you can choose the components you want to deploy on
your mail server.

![](./images/iredmail-easy/installation/components.png){: width="700px" }

## 组件设定

单击邮件服务器配置页面的`Settings`选项卡。
Click tab `Settings` on the mail server profile page.

根据你选择的组件，此页面上的设置可能会有所不同。请填写此页面上所有必填的表单字段。带红色星号的字段为必填字段，其他为可选字段。
Depends on the components you selected, the settings on this page may be
different. Please fill all required form fields on this page.

Fields with red asterisk are required, others are optional.

![](./images/iredmail-easy/installation/settings.png){: width="700px" }

## 部署

!!! attention
    部署生成的所有账户和密码都存储在`/root/iRedMail/iRedMail.tips`文件中。
    All accounts and passwords generated during deployment are stored in
    file `/root/iRedMail/iRedMail.tips` on your server.

单击邮件服务器配置页面的 `Deployment`选项卡。
Click tab `Deployment` on the mail server profile page.

请在邮件服务器上运行网页中提示的的三个命令，命令会帮助你设定`ssh public key`。如果使用非`root`用户，那么该用户必须是可以使用`sudo`Linux发行版上或`doas`OpenBSD发行版上权限的用户。
Please run the commands displayed on this page on your mail server, it will
download a shell script to simplify ssh public key setup. If ssh login user is
not `root`, it will help setup `sudo` (on Linux) or `doas` (on OpenBSD) also.

![](./images/iredmail-easy/installation/deployment.png){: width="900px" }

在命令完成后，即可单击`deployment`选项卡`Perform Full Deployment`按钮开始部署服务器。
After you ran the commands, it's ready to deployment. Click the button
`Perform Full Deployment` to start the deployment.

根据你的网络环境，云端平台会需要几分钟甚至更长的时间来完成部署，请耐心等待。
页面将显示部署任务的log，可以在部署失败时分析部署失败的原因。
Depends on the components you selected, and network connection speed between
your server and our deployment server, it may take few minutes or even longer
to finish. Please be patient.

It will refresh the page every 5 seconds and show you the latest output of
deployment task, you can watch and (hopefully) have some fun. :)

## 工单支持Get techinical support through the ticket system

如果您有任何疑问，请随时提交工单，详细描述问题，支持团队将尽快答复。
If you have any question or issue, feel free to open a new support ticket,
clearly explain the question or issue, support team will try to reply as soon
as possible.

![](./images/iredmail-easy/installation/support.png){: width="600px" }

## 用户资料更改Update account profile

`属性`选项可以修改用户账户资料。
You can update the account profile on the `Profile` page:

- 姓名
- 时区
- 密码
- 订阅版本更新通知

如果你不喜欢使用云端平台，可以点击左侧属性，删除账号即可。
If you do not like this platform, you can find a button on this page to remove
your account.

![](./images/iredmail-easy/installation/account_profile.png){: width="800px" }

## 相关文档链接

* [技术实践](./iredmail-easy.best.practice.html)
* [iRedMail配置DNS记录](./setup.dns.html)
* [申请Let's Encrypt证书](./letsencrypt.html)
* [邮件客户端配置](./index.html#mua)
