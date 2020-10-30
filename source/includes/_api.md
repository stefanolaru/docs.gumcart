# API Reference

Welcome to the GumCart API. You can use this to access GumCart API endpoints, which can get information about your shop & orders.

## Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "https://api.gumcart.com"
  --header 'X-APIKEY: yourapikey' \
  --header 'Content-Type: application/json' \
```

> Make sure to replace `yourapikey` with your API key.

GumCart uses API keys to allow access to the API. To obtain an API key please go to https://www.gumcart.com

We expect for the API key to be included in the majority of API requests in a header that looks like the following:

`X-APIKEY: yourapikey`

<aside class="notice">
You must replace <code>yourapikey</code> with your API key.
</aside>
