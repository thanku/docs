**ThankU for Business** - https://www.thanku.business

# ThankU Verify Business API Endpoint (Version 1)

This endpoint is used to check if a business users is already registered via the given email address. A confirmation email containing a confirm button will be send to the user. Hitting the confirm button redirects the user to the given callback URL for further processing. This endpoint can also be used to resend the confirmation email after registration.

## Usage

### Request: `POST https://app.thanku.business/api/verifyBusiness`

Headers:
* `Content-Type`: `application/json`
* `X-ThankU-API-Key`: a SHA256 hash value (this is a secret key which should only be used for server-side calls)

Body (JSON): 
* `email` [string] - e.g. `foo@example.com`
* `callbackUrl` [string] - URL to redirect to after successful confirmation (replacing `THANKU_POSTPAID_TOKEN` in the URL with a __BASE64__ representation of the users's postpaid token)

### Response

#### Success case (status: `200`)

Body (JSON):
* `nickname` [string] - the ThankU wallet name, e.g. `Foo Bar`
* `slug` [string] - the ThankU wallet address part after `https://thx.to/:` e.g. `foo-bar`
* `language` [string] - the base language of the user, only `en` and `de` available
* `confirmed` [boolean] - indicates if the user is already confirmed
  
#### Error case (status: `400`)

Body (JSON):
* `error` - the error name (e.g. `user not found`, `no business user`, `invalid request body data`)

#### Error case (status: `403`)

Body (JSON):
* `error` - the error name (e.g. `API key invalid`, `API key missing`)

---

(c) 2024 In the Now GmbH - www.thanku.business - support@thanku.business
