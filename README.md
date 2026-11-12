# Agent profiles

[UCP](https://ucp.dev) agent profiles for the automated tools run by
[Bards & Cards](https://bardsandcards.com). Stores that speak UCP fetch these to
see who is calling and which capabilities the caller supports.

| Profile | Used for |
|---|---|
| [`catalog-reader.json`](https://agents.bardsandcards.com/catalog-reader.json) | Reading supplier catalogs: product search and lookup only. No carts, checkouts or orders. |

A profile's URL is its identity, so add a new file rather than renaming one
that is in use.

## Hosting

The files in `public/` are served at `agents.bardsandcards.com` by a Cloudflare
Worker that has no script, only static assets. UCP requires profiles to be
served without redirects and with `Cache-Control: public` and a `max-age` of at
least 60 seconds; `public/_headers` sets that.

```sh
npm ci
npm run dev      # serve locally
npm run deploy   # needs CLOUDFLARE_API_TOKEN and CLOUDFLARE_ACCOUNT_ID
```

The deploy token needs Workers Scripts: Edit on the account, plus Workers
Routes: Edit and DNS: Edit on the `bardsandcards.com` zone.
