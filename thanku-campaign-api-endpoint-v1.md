**ThankU for business** - https://www.thanku.social/en/business

# ThankU Campaign API Endpoint (Version 1)

The **ThankU Campaign API Endpoint** can be used to automatically create a new ThankU based on a previously configured campaign. After creation the ThankU will be sent via email. The request is secured by a `token` only known to the user and the ThankU system.

To be able to use this endpoint, please create your ThankU wallet first: https://www.thanku.social/create-wallet and get in contact with us via business@thanku.social so that we can configure your campaign and provide the final API endpoint URL.

## Campaign setup

The following data needs to be defined for a campaign:

- Impact (e.g. "plant 3 trees" or "protect 100 sqm wildlife habitat")
- Language (english or german)
- Message template (may contain `{{placeholders}}` which will be replaced with the data provided in the API endpoint request body)
- Receiver email template (may contain `{{placeholders}}` which will be replaced with the data provided in the API endpoint request body)

## Usage

This endpoint only allows to create one ThankU per provided email address and per campaign. Using the same email address for different requests is not allowed and will result in HTTP status `400`. This restriction was made to support tools like Google Forms, where users may submit their survey multiple times with the same email address, but should receive only one ThankU.

**Request:** `POST https://www.thanku.social/api/donate/campaign/:id/:token`[`?simulate=true`]

**Request Headers:**

- `Content-Type`: `application/json`

**Request Body:** (example)

```json
{
  "name": "John",
  "email": "john@example.com"
}
```

**Campaign:** (example)

- Message template: `Hello {{name}}, thank you for taking our survey!`
- Receiver email template: `{{email}}`

**Response Status:**

- `201` on successful creation
- `400` invalid token, or email already used for campaign or `{{placeholder}}` not replaced

**Response Body:**

```json
{ "id": "sUiS29M3t0CbhOvATxnS" }
```

or when simulated:

```json
{ "id": "00TEST00TEST00TEST00" }
```

The `id` can be used to create a ThankU link, which looks like e.g. `https://thx.to/you/sUiS29M3t0CbhOvATxnS`. Send this ThankU link to your customer to show your gratitude. Klick [here](https://thx.to/you/sUiS29M3t0CbhOvATxnS) to see an example.

## Simulation / Testing

Passing URL parameter `simulate=true` prevents storing any data to the ThankU system. This is great for testing, because no ThankU will be created.

---

(c) 2023 thxto gUG - www.thanku.social - business@thanku.social
