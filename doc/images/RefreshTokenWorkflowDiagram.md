# Refresh Token Workflow

The Protocol Diagram was created using [Web Sequence Diagrams](https://www.websequencediagrams.com/)
and can be edited by pasting in the following.  The resulting diagram is
downloaded and save as "RefreshTokenWorkflow.png".

```text
title Refresh Token Workflow

UIO->Edge Proxy: 4i) make local authorized requests (e.g. /preferences) passing loginToken in Header
Edge Proxy->Preferences Server: 4ii) redirect to prefs server resource
note left of Preferences Server: 5i) check against stored loginToken and expiry
Preferences Server->Google (SSO): 5ii) refresh access token using /token request
note left of Google (SSO): 5iii) only if access_token and loginToken have expired
Google (SSO)->Preferences Server: 5iv) return new access token response
note left of Preferences Server: 5v) compute new loginToken if old one expired
Preferences Server->Edge Proxy: 4iv) return response; payload contains (new) loginToken
Edge Proxy->UIO: 4v) return response; payload contains (new) loginToken
```
