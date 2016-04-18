# iRedAdmin-Pro: RESTful API

[TOC]

!!! note

    If you need an API which has not yet been implemented, don't hesitate to
    [contact us](../contact.html).

## Summary

iRedAdmin-Pro RESTful API will return message in JSON format.

* If operation succeed, it returns JSON `{'success': true}`.
* If operation failed, it returns JSON `{'success': false, 'msg': '<error_reason>'}`.

## Requirements

* At least iRedAdmin-Pro-SQL-2.4.0 or iRedAdmin-Pro-LDAP-2.6.0. Earlier releases
  didn't offer RESTful API.

## APIs

Notes:

* replace `<domain>` in URL by the real domain name.
* replace `<mail>` in URL by the real email address.

### Domain

URL | HTTP Method | Summary
--- | --- | ---
/api/domain/<domain\> | POST | Create a new domin
/api/domain/<domain\> | DELETE | Delete an existing domain
/api/domain/<domain\> | PUT | Update profile of an existing domain

Possible `PUT` parameters used to update account profile:

Parameter Name | Summary | Sample Usage
--- |--- |---
`cn` | the short description of this domain name. e.g. company name | `cn=iRedMail Project`
`quota` | a integer number for mailbox quota (for whole domain, in MB) | `quota=20480`
`preferredLanguage` | default preferred language for new user | `preferredLanguage=en_US`
`defaultQuota` | default mailbox quota for new user | `defaultQuota=1024`
`maxUserQuota` | Max mailbox quota of a single mail user | `maxUserQuota=2048`
`numberOfUsers` | Max number of mail user accounts | `numberOfUsers=20`
`numberOfAliases` | Max number of mail alias accounts | `numberOfAliases=30`

### User

URL | HTTP Method | Summary
--- |---| ---
/api/user/<mail\> | POST | Create a new mail user
/api/user/<mail\> | DELETE | Delete an existing mail user
/api/user/<mail\> | PUT | Update profile of an existing mail user

Possible `PUT` parameters used to update account profile:

Parameter Name | Summary | Sample Usage
--- |--- |---
`cn` | display name | `cn=My New Name`
`preferredLanguage` | default preferred language for new user | `preferredLanguage=en_US`
`mailQuota` | mailbox quota for this user (in MB) | `mailQuota=1024`

### Mailing List (OpenLDAP only)

URL | HTTP Method | Summary
--- |---| ---
/api/maillist/<mail\> | POST | Create a new mailing list
/api/maillist/<mail\> | DELETE | Delete an existing mailing list
/api/maillist/<mail\> | PUT | Update profile of an existing mailing list

Possible `PUT` parameters used to update account profile:

Parameter Name | Summary | Sample Usage
--- |--- |---
`cn` | display name | `cn=My List Name`

### Mail Alias

URL | HTTP Method | Summary
--- |---| ---
/api/alias/<mail\> | POST | Create a new mail alias
/api/alias/<mail\> | DELETE | Delete an existing mail alias
/api/alias/<mail\> | PUT | Update profile of an existing mail alias

Possible `PUT` parameters used to update account profile:

Parameter Name | Summary | Sample Usage
--- |--- |---
`cn` | display name | `cn=My List Name`

##  Sample code to interact with iRedAdmin-Pro RESTful API

* [iRedAdmin-Pro RESTful API (interact with `curl`)](./iredadmin-pro.restful.api.curl.html)
* [iRedAdmin-Pro RESTful API (interact with Python)](./iredadmin-pro.restful.api.python.html)