---
title: Obtain a refresh token at Google OAuth2 Playground
categories:
  - Google
  - OAuth2.0
  - Nodemailer
tags:
  - Token
date: 2018-01-05 10:54:03
---

1.- Go to the [Google Oauth2.0 Playground](https://developers.google.com/oauthplayground).

2.- Click the Gear Button on the right-top. Set your Client ID and Client Secret obtained from the [Google Developers Console](https://code.google.com/apis/console/), and select Access token location as Authorization header w/ Bearer prefix. Close this configuration overlay.

<a href="https://imgur.com/7Bcg7sM"><img src="https://i.imgur.com/7Bcg7sM.png" title="source: imgur.com" /></a>

3.- You will need to list the URL https://developers.google.com/oauthplayground as a valid redirect URI in your [Google APIs Console](https://code.google.com/apis/console/)'s project. Then enter the client ID and secret assigned to a web application on your project below:

4.- Set up the scopes. Use https://mail.google.com/ as it’s the one need by nodemailer. Then click the Authorize APIs button.

<a href="https://imgur.com/V8vMd06"><img src="https://i.imgur.com/V8vMd06.png" title="source: imgur.com" /></a>

5.- After OAuth2.0 authorization, exchange authorization code for tokens and your refresh token is ready-to-use.

<a href="https://imgur.com/Xr2Cvvj"><img src="https://i.imgur.com/Xr2Cvvj.png" title="source: imgur.com" /></a>

6.- Finally you can use above credentials to send emails via [nodemailer](https://nodemailer.com/about/) without including passwords, as below:

```JavaScript
// Create the STMP transporter using the Gmail API and OAuth 2.0.
const transporter = nodemailer.createTransport({
  service: 'Gmail',
  pool: mailConfig.gmail.pool,
  auth: {
    clientId:     mailConfig.clientID,
    clientSecret: mailConfig.clientSecret,
    type:         mailConfig.gmail.type,        // 'OAuth2'
    user:         mailConfig.gmail.user,
    refreshToken: mailConfig.gmail.refreshToken
  }
})
```