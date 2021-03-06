# onedrive-nodejs

#What is onedrive-nodejs

Onedrive-nodejs is an open source library to connect your node js application to Microsoft one drive.

Microsoft Onedrive official documentation:

access token -> http://msdn.microsoft.com/en-us/library/hh243649.aspx#authorization_rest

api -> http://msdn.microsoft.com/en-us/library/hh826531.aspx#reading_folders

#How to configure the library

Remember to replace all the parameters on top of onedrive.js 

- client_id
- redirect_uri
- client_secret
- refresh_token

##How to generate all the parametes:

**1.Create your app on:**

https://account.live.com/developers/applications/

When you create your app, get note of:
- ID client (**client_id**)
- Client private key (**client_secret**)
- Web app url (**redirect_uri**)

**2.Get outh code:**

Remember to replace the ID_CLIENT and WEB_APP_URL_ESCAPED with the parameter of your app:

```
GET: https://login.live.com/oauth20_authorize.srf?client_id=ID_CLIENT&scope=wl.offline_access%20wl.skydrive_update%20wl.signin%20wl.basic&response_type=code&redirect_uri=WEB_APP_URL_ESCAPED
```

Response:
```
code=nnnnn-nnnn-nnnn-nnn-nnnnnnnnnn
```

get note of the given code.

**3.Get access token:**

Remember to replace the ID_CLIENT, WEB_APP_URL, CLIENT_PRIVATE_KEY and the code (GENERRATED_CODE) generate to the steps before.

```
POST: https://login.live.com/oauth20_token.srf

Content-Type: application/x-www-form-urlencoded 

Payload: client_id=ID_CLIENT&redirect_uri=WEB_APP_URL/&client_secret=CLIENT_PRIVATE_KEY&code=GENERRATED_CODE&grant_type=authorization_code
```

Response: 

```
token_type: "bearer"
expires_in: 3600
scope: "wl.offline_access wl.skydrive_update wl.signin wl.basic"
access_token: "NNNNNNNN"
refresh_token: "NNNNNNN"
authentication_token: "NNNNNNNN"
user_id: "NNNNNNNN"
}
```

Get note of the **refresh_token** and add it to the relative field in the library.
