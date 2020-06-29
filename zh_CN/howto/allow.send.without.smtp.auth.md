# 允许某些用户绕过SMTP验证发送邮件

[TOC]

!!! 教程

    本教程适用于iRedMail-1.0或更高版本。iRedMail-0.9.9或之前的版本请移步[本教程 ](./allow.user.to.send.email.without.authentication.html)。

## Postfix

修改`/etc/postfix/sender_access.pcre`(Linux/OpenBSD)或者`/usr/local/etc/postfix/sender_access.pcre`(FreeBSD)，添加允许绕过SMTP验证的用户。我们以 `user@example.com` 为例：

```
/^user@example\.com$/ OK
```

也可以使用IP地址代替，例如:

```
/^192\.168\.1\.1$/ OK
/^192\.168\.2\./   OK
/^172\.16\./       OK
```

!!! 参考文档
      
    * `sender_access.pcre`为pcre格式，如需要了解请查阅Postfix手册：         [PCRE_TABLE(5)](http://www.postfix.org/pcre_table.5.html) 。
    * 如需了解允许IP地址格式，请查阅postfix手册：[access(5)](http://www.postfix.org/access.5.html) 。

重启postfix服务以应用配置：

```
postfix reload
```

## iRedAPD

iRedAPD插件`reject_sender_login_mismatch`用于检查伪造的发件人地址。如果发件域是托管在你的邮件服务器上，但发送的邮件没有经过SMTP验证，将被iRedAPD视为伪造邮件并拒绝该邮件(附加拒绝消息：`SMTP AUTH is required for users under this sender
domain`)。
* 如需添加用户 `user@example.com` 绕过SMTP身份验证， 请在iRedAPD配置文件`/opt/iredapd/settings.py` 中添加以下内容:
    在/opt/iredapd/libs/default_settings.py文件中有相关参数的详细注释。

```
ALLOWED_FORGED_SENDERS = ['user@example.com']
```

* 如需添加IP `192.168.0.1` 或网段 `192.168.1.0/24` 绕过SMTP身份验证, 请修改 `/opt/iredapd/settings.py` 添加如下内容:

```
MYNETWORKS = ['192.168.0.1', '192.168.1.0/24']
```

重启 iRedAPD 服务。

```
service iredapd restart
```
