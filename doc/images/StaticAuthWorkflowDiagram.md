# Static Authorized Workflow Diagram

## Editing the Protocol Diagram

The Protocol Diagram was created using [Web Sequence Diagrams](https://www.websequencediagrams.com/)
and can be edited by pasting in the following.  The resulting diagram is
downloaded and saved as "StaticAuthWorkflow.png".

```text
title Preferences OpenID Connect Flow
actor Resource Owner

Resource Owner->UIO: 1i) Login
UIO->Edge Proxy: 1ii) open local login page (e.g. /login/google)
Edge Proxy->Preferences Server: 1iii) redirect to prefs server login
Preferences Server->Google (SSO): 2i) redirect to Google login
Google (SSO)->Resource Owner: 2ii) request user login and consent
Resource Owner->Google (SSO): 2iii) login and grant consent
Google (SSO)->Preferences Server: 2iv) state (anti-forgery token) and authorization code
note left of Preferences Server: 2v) confirm state (anti-forgery token)
Preferences Server->Google (SSO): 2vi) exchange authorization code
Google (SSO)->Preferences Server: 2vii) access token
note left of Preferences Server: 3i) use session key to authenticate resource owner and grant authorization
Preferences Server->Edge Proxy: 3ii) respond with session key authorization
Edge Proxy->UIO: 3iii) pass session key authorization
UIO->Edge Proxy: 4i) make local authorized requests (e.g. /preferences)
Edge Proxy->Preferences Server: 4ii) redirect to prefs server resource
note right of Preferences Server: 4iii) Verify authorization
Preferences Server->Edge Proxy: 4iv) return response
Edge Proxy->UIO: 4v) return response
```
