# 允许用户无需SMTP验证发送邮件

[TOC]

!!! 注意

    该教程使用于1.0或更高版本. 如果
    你使用的是旧版本, 请改用
    [本教程](./allow.send.without.smtp.auth.html) 代替.

## Postfix

新增文件: `/etc/postfix/sender_access.pcre`, 在文件中录入无需SMTP身份验证的用户。
本文使用 `user@example.com` 为例:

```
/^user@example\.com$/ OK
```

也可以使用IP地址代替，例如:

> 更多格式, 请查看postfix手册: [access(5)](http://www.postfix.org/access.5.html).

```
/^192\.168\.1\.1$/ OK
/^192\.168\.2\./   OK
/^172\.16\./       OK
```

将`sender_access.pcre`添加到 `/etc/postfix/main.cf` :

```
smtpd_sender_restrictions =
    check_sender_access pcre:/etc/postfix/sender_access.pcre,
    [...OTHER RESTRICTIONS HERE...]
```

重启/重新加载postfix服务:

```
# /etc/init.d/postfix restart
```

## iRedAPD

iRedAPD 的 `reject_sender_login_mismatch` 插件用于检查伪造的发件人地址。
如果发件人是托管在你的服务器上, 但没有SMTP身份验证, 那他将被当成伪造的邮件。这种情况下, iRedAPD 将拒绝该邮件
(附带相关提示: `Policy rejection not logged in`), 所以我们需要绕过发件人地址检查。如果邮件需要从局域网设备发送（如打印机、传真机之类），我们可以直接放行该设备IP地址。

* 如需添加用户 `user@example.com` 绕过SMTP身份验证， 请修改 `/opt/iredapd/settings.py` 添加以下内容:

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

## 参考文档

* Postfix 手册:
    * [check_sender_access](http://www.postfix.org/postconf.5.html#check_sender_access)
    * Manual page: [access(5)](http://www.postfix.org/access.5.html)
    * Manual page: [pcre_table(5)](http://www.postfix.org/pcre_table.5.html)
