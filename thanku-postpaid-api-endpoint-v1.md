**ThankU for business** - https://www.thanku.social/en/business

# ThankU Postpaid API Endpoint (Version 1)

The **ThankU Postpaid API Endpoint** can be used to automatically create a new ThankU. The request is secured by a signature, which can be created using a secret `token` only known to the user and the ThankU system.

This endpoint is used by the **ThankU Postpaid Widget**: https://github.com/thanku/postpaid-widget

To be able to use this endpoint, please create your ThankU wallet first: https://www.thanku.social/create-wallet and get in contact with us via business@thanku.social to get your secret `token`.

## Usage

This endpoint is idempotent, which means that same requests result in same ouput (ThankU ID). Repeated requests do not change or modify the ThankU system. Using the same `pid`/`slug` combination for different requests is not allowed and will result in HTTP status `400`.

**Request:** `POST https://www.thanku.social/api/donate/postpaid`[`?simulate=true`]

**Request Headers:**

- `Content-Type`: `application/json`
- `x-sig`: `babf8368069f1800e87c547b11b56d1ec24fc923c4b8846558140b2933f0f08e`

**Request Body:**

```json
{
  "slug": "foo-shop",
  "donateeGroup": "PlantTrees",
  "impactValue": 2,
  "message": "Dear Mrs. Smith, thank you for buying the Smeg 50's Style Toaster, your Foo Shop team",
  "language": "en",
  "pid": "abcd1234",
  "orderId": "A-21-13"
}
```

**Response Status:**

- `201` when created (1st request)
- `200` on repeated request
- `400` invalid data or signature, or `pid`/`slug` combination already used

**Response Body:**

```json
{
  "id": "sUiS29M3t0CbhOvATxnS",
  "link": "https://www.thanku.social/thanks/sUiS29M3t0CbhOvATxnS",
  "certificateNum": "328444638561610031954304369211874804",
  "certificateLink": "https://www.thanku.earth/certificate/328444638561610031954304369211874804"
}
```

or when simulated:

```json
{ "id": "00TEST00TEST00TEST00" }
```

The `id` can be used to create a ThankU link, which looks like e.g. `https://thx.to/you/sUiS29M3t0CbhOvATxnS`. Send this ThankU link to your customer to show your gratitude. Klick [here](https://thx.to/you/sUiS29M3t0CbhOvATxnS) to see an example.

## Request JSON Body Attributes

- `slug` - Your ThankU wallet name
- `donateeGroup` - The good cause (possible values: `PlantTrees` | `CleanOcean` | `ProtectWildlife`)
- `impactValue` - The impact value (a positive integer)
  - for `PlantTrees` number of trees
  - for `CleanOcean` kg plastic
  - for `ProtectWildlife` sqm habitat
- `message` - The ThankU message you want to show
- `language` - The language to use (possible values: `de` | `en`)
- `pid` - The postpaid id (an unique id like e.g. your order id)
- `orderId` - The ThankU Order ID

## Generating the signature (`x-sig` header)

The signature is used to authorize the request. It's a HMAC-SHA256 (hex encoded) hash of message `{slug}+{donateeGroup}+{impactValue}+{message}+{language}+{pid}` (replace `{slug}` etc. and concatenate all values with the `+` sign) with secret `token` (provided by the ThankU platform). It's important to notice that `x-sig` needs to be generated server-side to keep your `token` secret.

When using PHP consider using [`hash_hmac`](https://www.php.net/manual/en/function.hash-hmac.php) like e.g.:

```php
$sig = hash_hmac("sha256", "${slug}+${donateeGroup}+${impactValue}+${message}+${language}+${pid}", $token);
```

## Simulation / Testing

Passing URL parameter `simulate=true` prevents storing any data to the ThankU system. This is great for testing, because no ThankU will be created.

---

(c) 2021 thxto gUG - www.thanku.social - business@thanku.social
