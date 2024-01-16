**ThankU for Business** - https://www.thanku.business

# ThankU Register Business API Endpoint (Version 1)

This endpoint is used to register business users, who want to use the Postpaid API endpoint (e.g. via a custom integration like the Shopify App). When the submitted email was not already verified (not trusted), a confirmation email containing a confirm button will be send to the user. Hitting the confirm button activates the user and redirects her/him to the given callback URL for further processing.

## Usage

### Request: `POST https://www.thanku.business/api/registerBusiness`

Headers:
* `Content-Type`: `application/json`
* `X-ThankU-API-Key`: a SHA256 hash value (this is a secret key which should only be used for server-side calls)

Body (JSON): 
* `email` [string] - e.g. `foo@example.com`
* `nickname` [string] - the ThankU wallet name, e.g. `Foo Bar`
* `slug` [string] - the ThankU wallet address part after `https://thx.to/:` e.g. `foo-bar`
* `language` [string] - the base language of the user, only `en` and `de` available
* `callbackUrl` [string] - URL to redirect to after successful confirmation (no additional parameters are added)
* `trustedEmail` [boolean] - indicates if the email was already verified (only when `false` a confirmation email will be send)

### Response

#### Success case (status: `201`)

Body (JSON):
* `token` - the secret token (32 characters alphanumeric) to be used to generate the `signature` for the Postpaid API call

#### Error case (status: `400`)

Body (JSON):
* `error` - the error name (e.g. `slug blacklisted`, `slug already taken`, `email already in use`, `invalid request body data`)

#### Error case (status: `403`)

Body (JSON):
* `error` - the error name (e.g. `API key invalid`, `API key missing`)
* `confirmed` - indicates if the user is already confirmed

---

(c) 2024 In the Now GmbH - www.thanku.business - support@thanku.business
