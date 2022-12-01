**ThankU for business** - https://www.thanku.social/en/business

# ThankU Postpaid Widget Integration for Shopify

1. Create a ThankU page: https://www.thanku.social/en/app/personal-link
2. Contact us via business@thanku.social to become a ThankU Business Partner and to get your Secret Token
3. Open the following page in your Shopify admin area: https://YOUR-SHOP.myshopify.com/admin/settings/checkout
4. Adapt the following snippet to your needs and add it to the `Additional scripts` section:

```liquid
{% assign secret = "ADD_SECRET_TOKEN_HERE" %}
{% assign slug = "ADD_YOUR_THANKU_PAGE_NAME_HERE" %}
{% assign cause = "ProtectWildlife" %}
{% assign impact = 10 %}
{% assign message = "Dear " | append: checkout.customer.name | append: ", thank you for shopping with us! We really appreciate you as a customer. Your " | append: shop.name | append: " team." %}
{% assign lang = "en" %}
{% assign pid = checkout.id %}

{% assign sig = slug | append: "+" | append: cause | append: "+" | append: impact | append: "+" | append: message | append: "+" | append: lang | append: "+" | append: pid | hmac_sha256: secret %}

<link href="https://www.thanku.social/fonts/exo.css" rel="stylesheet" />
<script type="module" src="https://unpkg.com/@thanku/postpaid-widget"></script>

<thanku-postpaid-widget slug="{{ slug }}" cause="{{ cause }}" impact="{{ impact }}" message="{{ message }}" lang="{{ lang }}" pid="{{ pid }}" sig="{{ sig }}" style="display:block;margin-top:20px">
  <p>{{ message }}</p>
</thanku-postpaid-widget>
```

5. Make your customers happy by saying ThankU and doing good! 💚

## FAQ

### What is my ThankU page name?

On your ThankU page below your name you'll find your ThankU page short link. The part after the colon (:) is your ThankU page name (or slug), e.g. if `thx.to/:john-doe` is the ThankU page short link, then `john-doe` is the slug.

### Which causes are available?

- `ProtectWildlife` (impact in sqm)
- `CleanOcean` (impact in kg)
- `PlantTrees` (impact in trees)

### Which languages are available?

- `en` - english
- `de` - german

### How does the ThankU Postpaid Widget work?

Find all details here: https://github.com/thanku/postpaid-widget

---

(c) 2022 thxto gUG - www.thanku.social - business@thanku.social
