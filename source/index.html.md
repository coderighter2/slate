---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://better.mobi'>Powered by Better Mobile</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Better MTD API!

We introduce basic apis for our customers.

We have language binding in Shell.

This example API documentation page was created with [Slate](https://github.com/lord/slate).


# Authentication

## Login

```shell
curl -X POST https://dev.bmobi.net/api/v1/user/loginUser/ \
    -H "Content-Type: application/json" \
    -d '{"username":"user@gmail.com", "password": "password"}'
```

> The above command returns status code 200 and JSON structured like this:

```json
{
    "access_token": "wuenj66jsOseqIWC4Mnt31brb8DWr-qbr-7CxXg7m1h8lYwKI014PstfNWneQgcTe7QNakDxUfHBKgsvTX_-yzrAnpP4d4AC9kxWlql6cv6KQ02vttRmWyU6r3xVzoYFheiBO-cxOGt8kcilH4KJPMvLs_dh_q9YwXAmFMwxKS-sV89kIsA1N-SnXji9Ug3tz5t8sWOl_MzD8cYv4YcjJL9aEgOc2MYWRKr1x5PMvKlUuY9LA1TU6KuzYiygFq9T74t64jutWd3S9NNcZK5AYypS0kbzLK7-i-bYdHwI2bR0FrWk1cnETt7Kexno3aFmDxrgwKOpe7aIiB6S2a_DXj_4QdxqgiDUPWmIv0B89GVL3XerbmwkliY6j0uBrS1l91yVFRS5NnZsU2Yhdv2HFxt7YPCpTUhHMj86LmiMCkhdnqcBUvd1NfCnrny7oz4i869KIJTzALhzs9N5j5WMmJ9lMhpkffB-8CjhClyzxqMri_U1iZk1tJspvn4U_WN8",
    "token_type": "bearer",
    "expires_in": 7200,
    "userName": "hafizmohammedg@gmail.com1559",
    ".issued": "Sun, 17 Jun 2018 14:09:45 GMT",
    ".expires": "Sun, 17 Jun 2018 16:09:45 GMT",
    "userid": "27",
    "roles": "...",
    "group_name": "Super Admin",
    "PasswordExpired": false,
    "DashConfig": "...",
    "Theme": "{\"passKey\":1,\"showAppDashboard\":1,\"POC\":0}",
    "user_name": "hafizmohammedg@gmail.com",
    "console": "{\"threat\":1,\"configurator\":0,\"analyzer\":1,\"workspace\":0,\"dlp\":1,\"trusted_login\":1,\"public_app\":1,\"onpremise\":1,\"lab\":1}",
    "smb": 0,
    "hasmdm": 1,
    "dev": 1,
    "com_url": null,
    "com_ui_url": null,
    "temp_token": null,
    "company_id": 0,
    "mid": 0,
    "notification": []
}
```

> If the above command fails, returns status code 400 and error message like this:

```json
The user name or password is incorrect
```

This endpoint is used to login.

### HTTP Request

`POST https://<tenant>.bmobi.net/api/v1/user/loginUser/`


### Request Parameters (JSON)

Parameter | Type | Description
--------- | --------- | -----------
username | String | Username
password | String | Password



### Response Parameters

Parameter | Type | Description
--------- | --------- | -----------
access_token | String | Access token. We use Bearer Token Authentication.
expires_in | String | Expiration duration of the token
userName | String | Login username (internal use)
userid | String | User id
group_name | String | Group name this user belongs to. It represents the permission of the user
PasswordExpired | Bool | Indicate whether the password is expired. If this is true, login fails and you need to ask user to change password.
user_name | String | Login username/email
com_url | Dictionary | Tenant endpoint url
com_ui_url | Dictionary | Tenant UI url

# User API

## Create User (Single)

```shell
curl -X POST https://dev.bmobi.net/api/v1/account/register \
    -H "Authorization: Bearer access_token" \
    -H "Content-Type: application/json" \
    -d '{"group_ids":["5659"],"model":{"ConfirmPassword":"","Password":"","UserName":"user@gmail.com","email":"user@gmail.com","first_name":"John","last_name":"Smith","phone_number":"13002019999","role":"users"},"settings":{"AllowAutoUpdate":true,"AllowCreateLocalBlueprint":false,"AllowCreateServerBlueprint":false,"AllowEditServerBlueprint":false,"AllowUpdateServerBlueprint":false,"OrganisationName":""}}'
```

> The above command returns status code 200 and empty response

This endpoint is used to create users for the tenant.

### HTTP Request

`POST https://<tenant>.bmobi.net/api/v1/account/register`

### Request Parameters (JSON)

Parameter | Type | Description
--------- | --------- | -----------
group_ids | String Array | Group array that new user belongs to (refer Get Groups endpoint)
model | Dictionary | New user information
setting | Dictionary | Just use the same data in the sample request


<aside class="notice">
You must replace <code>access_token</code> with your access token get from Login api.
</aside>


## Create User (Bulk)

```shell
curl -X POST https://dev.bmobi.net/api/v1/account/register_bulk \
    -H "Authorization: Bearer access_token" \
    -H "Content-Type: application/json" \
    -d '{"users":[{"group_ids":0, "setting":{"AllowCreateLocalBlueprint":false, "AllowCreateServerBlueprint": false, "AllowEditServerBlueprint": false, "AllowUpdateServerBlueprint": false, "OrganisationName":"", "AllowAutoUpdate":true},"model":{"UserName":"user@gmail.com", "first_name":"John", "last_name":"Smith", "email":"user@gmail.com", "phone_number":"13004009000", "role":"users"}}]}'
```

> The above command returns status code 200

This endpoint is used to create users for the tenant.

### HTTP Request

`POST https://<tenant>.bmobi.net/api/v1/account/register_bulk`

### Request Parameters (JSON)


Parameter | Type | Description
--------- | --------- | -----------
users | Array | JSON array of user objects

#### User object (JSON)

Parameter | Type | Description
--------- | --------- | -----------
group_ids | Number | Value must be 0
setting | Dictionary | Value must be same as the one in the sample request
model | Dictionary | User information, described at below

#### User model object (JSON)

Parameter | Type | Description
--------- | --------- | -----------
UserName | String | Login username, recommend to use email
first_name | String | First name
last_name | String | Last name
email | String | Email
phone_number | String | Phone number. It should contains the country code, without '+'
role | String | User role. Value must be "users"

<aside class="notice">
You must replace <code>access_token</code> with your access token get from Login api.
</aside>


## Get Groups

```shell
curl -X GET https://dev.bmobi.net/api/v1/group/getall \
    -H "Authorization: Bearer access_token"
```

> The above command returns status code 200

```json
{
    "company_id":1111,
    "gid": 111,
    "group_name": "Default",
    "is_deleted":0,
    "mid": null,
    "type": null,
    "vender_ref_id":null
}
```

This endpoint is used to create users for the tenant.

### HTTP Request

`POST https://<tenant>.bmobi.net/api/v1/group/getall`

<aside class="notice">
You must replace <code>access_token</code> with your access token get from Login api.
</aside>


# Device API

## Search Device

```shell
curl -X POST https://dev.bmobi.net/api/v1/device/getnew \
    -H "Authorization: Bearer access_token" \
    -H "Content-Type: application/json" \
    -d '{"CVE":"", "agent_version":"", "carrier":"", "filter":"installed", "filter_agent":[], "filter_incidents":[], "filter_models": [], "filter_pending":[], "filter_platform":[], "filter_risk":[], "filter_status":[],"itemsPerPage":50, "label": 0, "locid":0, "os_version":"", "page":1, "patch_info":"", "reverse": true, "search": "", "sortBy":"last_reported", "totalItems": 0, "udid": "", "vio_type": ""}'
```

> The above command returns status code 200

This endpoint is used to search devices. You can use the search parameters against device's properties.

### HTTP Request

`POST https://<tenant>.bmobi.net/api/v1/device/getnew`

### Request Parameters (JSON)

Parameter | Type | Description
--------- | --------- | -----------
itemsPerPage | Number | Pagination parameter
page | Number | Pagination parameter, starts from 1
sortBy | String | Pagination parameter
reverse | Bool | Pagination parameter
label | Number | Device label id, 0 for unspecified/all
locid | Number | Device organization id, 0 for unspecified/all
os_version | String | OS version.
patch_info | String | Device patch info.
totalItems | Number | Must be 0
udid | Number | Device UDID
vio_type | String | This must be empty string
CVE | String | This must be empty string
agent_version | String | Agent version
carrier | String | Carrier
filter | String Array | Installation status: `installed`, `notinstalled`, `uninstalled`
filter_incidents | Number Array | Incidents id array. Search against incidents happen on the devices
filter_models | Array | Empty array
filter_pending | Array | Empty array
filter_platform | Array | Array of platforms: `Apple`, `Android`, `Windows`
filter_risk | Array | Array of risk levels: `low`, `medium`, `high`
filter_status | Array | Array of device status. Example : `["online"]`


<aside class="notice">
All the request parameters are required.
</aside>

## Activate Device

```shell
curl -X POST https://dev.bmobi.net/api/v1/company/send_activate_email \
    -H "Authorization: Bearer access_token" \
    -H "Content-Type: application/json" \
    -d '[{"id": 1525, "udid":"93f39629393816238e47adde3c10e896", "name":"SAMSUNG SM-G935F", "aw_tenant_id":11, "template_id":"685", "user_name":"purna.bhat@better.mobi"}]'
```

> The above command returns status code 200

This endpoint is used to send an activation code to the device's owner.
If user installs the ActiveShield app, he is asked to enter activation code. This endpoint is used to get the activation code for the device registered at our console.

### HTTP Request

`POST https://<tenant>.bmobi.net/api/v1/company/send_activate_email`

### Request Parameters (JSON)

Request body is a JSON array of device objects

#### Device Object

Parameter | Type | Description
--------- | --------- | -----------
id | Number | Device's id (comes from Service Device endpoint)
udid | String | Device UDID (comes from Service Device endpoint)
name | String | Device name (comes from Service Device endpoint)
aw_tenant_id | String | Tenant id which the device registered at (comes from Service Device endpoint)
template_id | String | Email template id
user_name | String | Owner's email which the activation email is sent to (comes from Service Device endpoint)

# Tenant API

The following endpoints must be made against `aad.bmobi.net`.

## Add Tenant

```shell
curl -X GET https://aad.bmobi.net/api/v1/company/addTenant/ \
    -H "Content-Type: application/json" \
    -d '{"client_id":"860d3ab4-8fd1-45f5-89cd-ecf51e4f92e5", "redirectUri": "https://aad-dev.bmobi.net/redirects/aad", "email":"admin@bettermobiletestenv.onmicrosoft.com", "code":"AD access code"}'
```

> The above command returns status code 200 and JSON structured like this:

```json
{
    "access_token": "wuenj66jsOseqIWC4Mnt31brb8DWr-qbr-7CxXg7m1h8lYwKI014PstfNWneQgcTe7QNakDxUfHBKgsvTX_-yzrAnpP4d4AC9kxWlql6cv6KQ02vttRmWyU6r3xVzoYFheiBO-cxOGt8kcilH4KJPMvLs_dh_q9YwXAmFMwxKS-sV89kIsA1N-SnXji9Ug3tz5t8sWOl_MzD8cYv4YcjJL9aEgOc2MYWRKr1x5PMvKlUuY9LA1TU6KuzYiygFq9T74t64jutWd3S9NNcZK5AYypS0kbzLK7-i-bYdHwI2bR0FrWk1cnETt7Kexno3aFmDxrgwKOpe7aIiB6S2a_DXj_4QdxqgiDUPWmIv0B89GVL3XerbmwkliY6j0uBrS1l91yVFRS5NnZsU2Yhdv2HFxt7YPCpTUhHMj86LmiMCkhdnqcBUvd1NfCnrny7oz4i869KIJTzALhzs9N5j5WMmJ9lMhpkffB-8CjhClyzxqMri_U1iZk1tJspvn4U_WN8",
    "token_type": "bearer",
    "expires_in": 7200,
    "userName": "hafizmohammedg@gmail.com1559",
    ".issued": "Sun, 17 Jun 2018 14:09:45 GMT",
    ".expires": "Sun, 17 Jun 2018 16:09:45 GMT",
    "userid": "645",
    "roles": "...",
    "group_name": "Super Admin",
    "PasswordExpired": false,
    "DashConfig": "...",
    "Theme": null,
    "user_name": "admin@bettermobiletestenv.onmicrosoft.com",
    "console": "{\"threat\":1,\"configurator\":0,\"analyzer\":1,\"workspace\":0,\"dlp\":1,\"trusted_login\":1,\"public_app\":1,\"onpremise\":1,\"lab\":1}",
    "smb": 0,
    "hasmdm": null,
    "dev": null,
    "com_url": "https://newtenant.bmobi.net/",
    "com_ui_url": "https://newtenant-new.bmobi.net/",
    "temp_token": null,
    "company_id": 1659,
    "mid": 118,
    "notification": []
}
```

> If the above command fails, returns status code 400

This endpoint is used to create a tenant. After the Azure AD flow is done, you may need to redirect to `com_ui_url` which is the new tenant UI

### HTTP Request

`GET https://aad.bmobi.net/api/v1/company/addTenant/`

### Request Parameters

Parameter | Type | Description
--------- | --------- | -----------
email | String | Azure AD login email
code | String | Azure AD access code
client_id | String | Client ID of Better MTD app registered at Azure AD Console
redirectUri | String | Redirect uri registered at Azure AD Console


<aside class="notice">
You must save the response of this endpoint for the following steps.
</aside>

## Add Default Security Group

```shell
curl -X POST https://aad.bmobi.net/api/v1/company/add_default_intune_security_group?cid=0&mid=0
```

> The above command returns status code 200 and JSON structured like this:

```json
{
    "value": [
        {
            "displayName": "Default",
            "objectId": 0
        },
        {
            "displayName": "Better Security",
            "objectId": 1
        }
    ]
}
```


After add a tenant, you need to add the default security group. This endpoint is used for this purpose.

### HTTP Request

`GET https://aad.bmobi.net/api/v1/company/add_default_intune_security_group`

### Request Parameters (JSON)

Parameter | Type | Description
--------- | --------- | -----------
mid | String | Id retrieved from the response of Add Tenant endpoint
cid | String | Company Id retrieved from the response of Add Tenant endpoint

<aside class="notice">
You must save the response of this endpoint for the following step - Activate ActiveShield
</aside>

## Search Security Groups

```shell
curl -X GET https://aad.bmobi.net/api/v1/company/search_intune_security_group \
    -d 'mid=0&cid=0&groupName="a"'
```

> The above command returns status code 200 and JSON structured like this:

```json
{
    "value": [
        {
            "displayName": "Default",
            "objectId": 0
        },
        {
            "displayName": "Better Security",
            "objectId": 1
        }
    ]
}
```


After add a tenant, you can add security groups to the new tenant. This endpoint is used to search the security groups to be added.

### HTTP Request

`GET https://aad.bmobi.net/api/v1/company/search_intune_security_group`

### Request Parameters (JSON)

Parameter | Type | Description
--------- | --------- | -----------
mid | String | Id retrieved from the Add Tenant endpoint
cid | String | Company Id
groupName | String | Search keyword

## Add Security Groups

```shell
curl -X POST https://aad.bmobi.net/api/v1/company/add_intune_security_group \
    -H "Content-Type: application/json" \
    -d '{"mid":0,"cid":0,"data":[{"displayName":"Default", "objectId": 0},{"displayName":"Better Security", "objectId":1}]}'
```

> The above command returns status code 200 and JSON structured like this:

```json
{
    "value": [
        {
            "displayName": "Default",
            "objectId": 0
        },
        {
            "displayName": "Better Security",
            "objectId": 1
        }
    ]
}
```

After add a tenant, you can add security groups to the new tenant. This endpoint is used to search the security groups to be added.

### HTTP Request

`POST https://aad.bmobi.net/api/v1/company/add_intune_security_group`

### Request Parameters (JSON)

Parameter | Type | Description
--------- | --------- | -----------
mid | String | Id retrieved from the Add Tenant endpoint
cid | String | Company Id
groupName | String | Search keyword


<aside class="notice">
You must save the response of this endpoint for the following step - Activate ActiveShield
</aside>

## Activate ActiveShield

```shell
curl -X POST https://aad.bmobi.net/api/v1/company/add_intune_app \
    -H "Content-Type: application/json" \
    -d '{"cid":0, "mid":0, "apple": true, "android": true, "groups":[{displayName:"Default", objectId:0}],"client_id":"860d3ab4-8fd1-45f5-89cd-ecf51e4f92e5", "redirectUri": "https://aad-dev.bmobi.net/redirects/aad", "code":"AQABAAIAAADX8GCi6Js6SK82TsD2Pb7reZB-zZ-j-MNuhWSyGZdbZXdTPIVJR5XCvXe5CTkR18r3622jzX0qTIuXdGRGOsRZ2bmv_-x5OV6MBXDgIjlJ2wBOq-Pl0sGXQWBcMxDa6eTbXTpc_GalihM0E7ykBVpTxRgHVUCOsvM6InJpvd_H9nrqlB-gdF3O4zXZnF-55I7oAc73N8oJYBJQU-hq1BY6ITnA30Krs7chaBJA-Ww7G9-dcbHT8go6bzs7TTippvaLPx5O8g_vytS5y-VfegYJxbiiijLPy0FmR7MYBY4qWoIpzYfmcaelJ5Qs10CeRkFEUHEFjwPA-HoX1qW-n749fW5O6-qbgHNjKhF9ZzsNXLb5Fh0KkCe8NRQqR2naYkLx2_c5gskp-nXSDzsKp0ebZ35pDPOmNfFNky8Xk80BPUUFMqAIpF4xac8W_Pl7_FjpplEaKA64eM-1eam5CiQhv0r7gsAIkS8afv5vwjemSUN1PfwIoSW4LlHwS49mv0HvzFFWuWx0wV4bkIcFmr1AHpzGP_5Pe_ihPgk6tdO_78f_QLupJk0enpuwDJJ-RkhZQoRiDSgeJvFFgNWMh0EuIAA"}'
```

> The above command returns status code 200 if success, otherwise 400

This endpoint is used to activate ActiveShield app for the tenant.

Wow! The only thing left is redirect user to new Tenant UI.

### HTTP Request

`POST https://aad.bmobi.net/api/v1/company/add_intune_app`

### Request Parameters (JSON)

Parameter | Type | Description
--------- | --------- | -----------
mid | String | Id retrieved from the Add Tenant endpoint
cid | String | Company Id
groups | String | Security gruops added to the tenant
apple | Bool | Indicate whether iOS app is enabled
android | Bool | Indicate whether Android app is enabled
client_id | String | Client ID of Better MTD app registered at Azure AD Console (use same value used for Add Tenant endpoint)
redirectUri | String | Redirect uri registered at Azure AD Console (use same value used for Add Tenant endpoint)
code | String | Azure AD access code (use same value used for Add Tenant endpoint)

## Login with Azure AD

```shell
curl -X POST https://aad.bmobi.net/api/v1/user/login_aad/ \
    -H "Content-Type: application/json" \
    -d '{"client_id":"860d3ab4-8fd1-45f5-89cd-ecf51e4f92e5", "redirectUri": "https://aad-dev.bmobi.net/redirects/aad", "code":"AQABAAIAAADX8GCi6Js6SK82TsD2Pb7reZB-zZ-j-MNuhWSyGZdbZXdTPIVJR5XCvXe5CTkR18r3622jzX0qTIuXdGRGOsRZ2bmv_-x5OV6MBXDgIjlJ2wBOq-Pl0sGXQWBcMxDa6eTbXTpc_GalihM0E7ykBVpTxRgHVUCOsvM6InJpvd_H9nrqlB-gdF3O4zXZnF-55I7oAc73N8oJYBJQU-hq1BY6ITnA30Krs7chaBJA-Ww7G9-dcbHT8go6bzs7TTippvaLPx5O8g_vytS5y-VfegYJxbiiijLPy0FmR7MYBY4qWoIpzYfmcaelJ5Qs10CeRkFEUHEFjwPA-HoX1qW-n749fW5O6-qbgHNjKhF9ZzsNXLb5Fh0KkCe8NRQqR2naYkLx2_c5gskp-nXSDzsKp0ebZ35pDPOmNfFNky8Xk80BPUUFMqAIpF4xac8W_Pl7_FjpplEaKA64eM-1eam5CiQhv0r7gsAIkS8afv5vwjemSUN1PfwIoSW4LlHwS49mv0HvzFFWuWx0wV4bkIcFmr1AHpzGP_5Pe_ihPgk6tdO_78f_QLupJk0enpuwDJJ-RkhZQoRiDSgeJvFFgNWMh0EuIAA"}'
```

> The above command returns status code 200 and JSON structured like this:

```json
{
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6IlRpb0d5d3dsaHZkRmJYWjgxM1dwUGF5OUFsVSIsImtpZCI6IlRpb0d5d3dsaHZkRmJYWjgxM1dwUGF5OUFsVSJ9.eyJhdWQiOiI4NjBkM2FiNC04ZmQxLTQ1ZjUtODljZC1lY2Y1MWU0ZjkyZTUiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC81NTRhNThlYy0zMDU0LTRjOWMtYjIyZC02ZTdlZjI3MGNkZjUvIiwiaWF0IjoxNTI5Mjg2MjU3LCJuYmYiOjE1MjkyODYyNTcsImV4cCI6MTUyOTI5MDE1NywiYWNyIjoiMSIsImFpbyI6IlkyZGdZQkJ2VGoyNld0YTQzb0d4VTJLZm1IZGoxT3pjV3lFWEgvN2cxOTJTbGlTemlRRUEiLCJhbXIiOlsicHdkIl0sImFwcGlkIjoiODYwZDNhYjQtOGZkMS00NWY1LTg5Y2QtZWNmNTFlNGY5MmU1IiwiYXBwaWRhY3IiOiIxIiwiZmFtaWx5X25hbWUiOiJNb25rZXkiLCJnaXZlbl9uYW1lIjoiVGVuYW50IiwiaXBhZGRyIjoiMTAzLjI1NC4xNTUuMjYiLCJuYW1lIjoiVGVuYW50IE1vbmtleSBBY2NvdW50Iiwib2lkIjoiOWZiY2QxOWUtNTM2Ni00MzFlLTk2YjQtZjA5NTMyM2VjMmMwIiwicHdkX2V4cCI6IjAiLCJwd2RfdXJsIjoiaHR0cHM6Ly9wb3J0YWwubWljcm9zb2Z0b25saW5lLmNvbS9DaGFuZ2VQYXNzd29yZC5hc3B4Iiwic2NwIjoiRGV2aWNlTWFuYWdlbWVudEFwcHMuUmVhZFdyaXRlLkFsbCBEZXZpY2VNYW5hZ2VtZW50Q29uZmlndXJhdGlvbi5SZWFkV3JpdGUuQWxsIERldmljZU1hbmFnZW1lbnRTZXJ2aWNlQ29uZmlnLlJlYWRXcml0ZS5BbGwgVXNlci5SZWFkIiwic3ViIjoicjFXSlB2ZW9yNzMzTTVQczlXcjZvelRYVGRhMzgweXFtQkotZzRsQ3NnMCIsInRpZCI6IjU1NGE1OGVjLTMwNTQtNGM5Yy1iMjJkLTZlN2VmMjcwY2RmNSIsInVuaXF1ZV9uYW1lIjoiYWRtaW5AYmV0dGVybW9iaWxldGVzdGVudi5vbm1pY3Jvc29mdC5jb20iLCJ1cG4iOiJhZG1pbkBiZXR0ZXJtb2JpbGV0ZXN0ZW52Lm9ubWljcm9zb2Z0LmNvbSIsInV0aSI6IkExTVoxaVdIZmtDa0FzR0hkWTFUQUEiLCJ2ZXIiOiIxLjAifQ.R5-qEbU6U_SfcYP_knO7YlyW-vVrRh_sGv413i_gKtMB-ZCD7D9ZJwOzqud3Z5eZ3cgfZQc9AnO5yoOZz9581nEjSgwGc9Wf1XDRHA6EH8rgAos1YCJq9uADuOtVeFijDIv9c3msgv1-CgB4LoJK-qYwW7TafKdLTuHWQwXMSgtEeqob57faj5Om2GcGw1fLNlQq0_3iY2X4lybVgDnxOfWNfMxKOzZkNhFGkBcl9Xm4Frik-0Rq29IzJySzveDJOdjh9cDYnjyW6Bo47JgXY13akQ0DIMgUZzBNQSdceFoF1CR_l2nOihMGV2BdsLsnFlukFHE4YeO7mYL9BC2mjg",
  "token_type": "Bearer",
  "expires_in": 7200,
  "userName": "admin@bettermobiletestenv.onmicrosoft.com",
  ".issued": null,
  ".expires": "1529290157",
  "userid": "698",
  "roles": "{\"device\":{\"view\":1,\"modify\":1,\"add\":1,\"map\":0,\"config\":null},\"policy\":{\"view\":1,\"modify\":1,\"add\":1,\"map\":0,\"config\":null},\"configuration\":{\"view\":1,\"modify\":1,\"add\":1,\"map\":0,\"config\":null},\"user\":{\"view\":1,\"modify\":1,\"add\":1,\"map\":0,\"config\":null},\"report\":{\"view\":1,\"modify\":1,\"add\":1,\"map\":0,\"config\":null},\"dashboard\":{\"view\":1,\"modify\":0,\"add\":0,\"map\":0,\"config\":null},\"threat\":{\"view\":1,\"modify\":1,\"add\":0,\"map\":0,\"config\":null}}",
  "group_name": "Super Admin",
  "PasswordExpired": false,
  "DashConfig": null,
  "Theme": null,
  "user_name": "admin@bettermobiletestenv.onmicrosoft.com",
  "console": "{\"threat\":\"1\",\"configurator\":\"0\",\"analyzer\":\"0\",\"workspace\":\"0\"}",
  "smb": null,
  "hasmdm": null,
  "dev": null,
  "com_url": "https://bettermobiletestenv-dev.bmobi.net",
  "com_ui_url": "https://bettermobiletestenv-dev-new.bmobi.net",
  "temp_token": null,
  "company_id": 0,
  "mid": 0,
  "notification": null
}
```

This endpoint is used to login with Azure AD credentials. After add a tenant, you can call this endpoint to login to the tenant. This endpoint returns the tenant UI url, you just need to redirect user to the url.

### HTTP Request

`POST https://aad.bmobi.net/api/v1/company/login_aad`

### Request Parameters (JSON)

Parameter | Type | Description
--------- | --------- | -----------
client_id | String | Client ID of Better MTD app registered at Azure AD Console (use same value used for Add Tenant endpoint)
redirectUri | String | Redirect uri registered at Azure AD Console (use same value used for Add Tenant endpoint)
code | String | Azure AD access code (use same value used for Add Tenant endpoint)
