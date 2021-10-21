**ThankU for business** - https://www.thanku.social/en/business

# ThankU Postpaid Widget Integration for Shopify

1. Create a ThankU page: https://www.thanku.social/en/app/personal-link
2. Contact us via business@thanku.social to become a ThankU Business Partner and to get your Secret Token
3. Open the following page in your Shopify admin area: https://YOUR-SHOP.myshopify.com/admin/settings/checkout 
4. Adapt the following snippet to your needs and add it to the `Additional scripts` section:

```liquid
{% assign secret = "*****ADD*SECRET*TOKEN*HERE******" %}
{% assign slug = "freshfarm-shop" %}
{% assign cause = "ProtectWildlife" %}
{% assign impact = 10 %}
{% assign message = "Dear " | append: checkout.customer.name | append: ", thank you for shopping with us! We really appreciate you as a customer. Your " | append: shop.name | append: " team." %}
{% assign lang = "en" %}
{% assign pid = checkout.id | append: checkout.order_name %}

{% assign sig = slug | append: "+" | append: cause | append: "+" | append: impact | append: "+" | append: message | append: "+" | append: lang | append: "+" | append: pid | hmac_sha256: secret %}

<link href="https://www.thanku.social/fonts/exo.css" rel="stylesheet" />
<script type="module" src="https://unpkg.com/@thanku/postpaid-widget"></script>

<thanku-postpaid-widget slug="{{ slug }}" cause="{{ cause }}" impact="{{ impact }}" message="{{ message }}" lang="{{ lang }}" pid="{{ pid }}" sig="{{ sig }}" style="display:block;margin-top:20px">
  <p>{{ message }}</p>
</thanku-postpaid-widget>
```

5. Make your customers happy by saying ThankU and doing good! 💚

---

(c) 2021 thxto gUG - www.thanku.social - business@thanku.social
