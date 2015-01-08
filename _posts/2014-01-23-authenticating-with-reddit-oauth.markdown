---
layout: note
title: Authenticating with Reddit OAuth
date: 2014-01-23
categories: note reddit oauth reference
---

This note is a direct copy of [this post](http://www.reddit.com/r/redditdev/comments/197x36/using_oauth_to_send_valid_requests/c8lz57u) (just in case it gets taken down or deleted for any reason). I found it really helpful as it beautifully describes the steps required to authenticate with the OAuth Reddit API.

- - -

## [/u/awain](http://www.reddit.com/user/awain)

> I'm currently in the process of writing a reddit app (yes, yet another one), which uses OAuth, and it's been a bit of a job trying to set it all up, so I'll try to set out what's needed for each phase.  I've only been working with it for around a week, so you're lucky! I'll also add a bit of detail for those that are starting from scratch.

> **Step 1:**

> Request: Type - **GET**

> **URI**: https://ssl.reddit.com/api/v1/authorize

> Querystring Params:

>* ***state***: unique string for your own use
* ***duration***: optional - default is '*temporary*'.  Use '*permanent*' for a permanent token (still requires new access token after 1 hour)
* ***response_type***: 'code'
* ***scope***: 'identity'
* ***client_id***: The *client_id* assigned by reddit
* ***redirect_uri***: the *redirect_uri* you assigned. Annoyingly, reddit only allows http or https:// so you can't provide a unique pseudo-protocol that your app recognises.  I used the the android package name to build my *redirect_uri*.

>Example:


>     https://ssl.reddit.com/api/v1/authorize?state=[unique string]&duration=permanent&response_type=code&scope=identity&client_id=[assigned client id]&redirect_uri=https://com.mycompany.mypackage

>Response:

>Webpage (HTML) for the login/register page.

>**Step 2:**

>User enters their details and submits.  If your app doesn't utilise the reddit webpage and instead uses a custom form, just get all the input parameters from the source code of that page.

>**Step 3:**

>User accepts (or declines) access to their account.

>**Step 4:**

>reddit redirects back to the *redirect_uri* you specified.  Appended to the response is a querystring containing the *state* and *code*, which is the *authorization_code* needed to get an *access_code*.

>**Step 5:**

>Request:  Type **POST**

>**URI**: https://ssl.reddit.com/api/v1/access_token

>Params:

>* ***state***: unique string for your own use
* ***scope***: 'identity'
* ***client_id***: The *client_id* assigned by reddit
* ***redirect_uri***: the *redirect_uri* you assigned.
* ***code***: the *code* received in step 4.
* ***grant_type***: 'authorization_code'

>Headers:

>You **must** send basic auth with this request.  The username and password are the *client_id* and *client_secret*, assigned by reddit respectively.

>Response:

>A JSON string, which contains either an error message or the params you need after a success.

>Example JSON:

>     {"access_token": "[token string]", "token_type": "bearer", "expires_in": 3600.0, "refresh_token": "[token string]", "scope": "identity"}

>You will only get the *refresh_token* if you request permanent tokens. You will need to store both the *access_token* and the *refresh_token*.

>**Step 6:**

>You can now you the *access_token* to send an OAuth request for an API resource.  To get the user's details for example, you can send:

>Request: type - **GET**

>**URI**: https://oauth.reddit.com/api/v1/me

>Header:

>Authorization : 'bearer [access_token from Step 5 response]'

>**Step 7 (optional):**

>If you request permanent access, then you will need to refresh the tokens after 1 hour.

>Request:  Type **POST**

>**URI**: https://ssl.reddit.com/api/v1/access_token

>Params:

>* ***state***: unique string for your own use
* ***scope***: 'identity'
* ***client_id***: The *client_id* assigned by reddit
* ***redirect_uri***: the *redirect_uri* you assigned.
* ***refresh_token***: the *refresh_token* received in step 5 response.
* ***grant_type***: 'refresh_token'

>Headers:

>You **must** send basic auth with this request.  The username and password are the *client_id* and *client_secret*, assigned by reddit respectively.

>Response:

>Same as Step 5.

>HTH!

