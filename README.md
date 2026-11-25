# ScraperAPI vs Bright Data: What Each Actually Costs, Which One Gets Past Cloudflare, and the Page Count Where You Switch (Plan and Price Tables)

Under 500,000 pages a month against sites that don't sit behind Cloudflare or DataDome, ScraperAPI is the cheaper pick, starting at $49/month for 100,000 credits. Past a million pages a month, or on targets like LinkedIn where basic CAPTCHA solving stops working, Bright Data's Web Unlocker is what actually returns data, at roughly $300–500/month for that workload. What follows is the arithmetic behind those two sentences: the full ScraperAPI plan table, what a credit buys once JavaScript rendering and hard domains enter the picture, how Bright Data's per-gigabyte meters behave at small volume, and where the two products trade places.

> Most teams should start on Hobby at $49/month. It gives you 100,000 credits, 20 concurrent connections and US/EU geolocation, which is enough to find out whether your scraper survives production traffic. If your targets sit outside the US or EU, your floor is Business at $299/month, because global geolocation isn't sold on the cheaper tiers.
>
> 👉 [Start on the $49 Hobby plan](https://www.scraperapi.com/?fp_ref=coupons)

## ScraperAPI plans and prices

ScraperAPI sells one product with tiered credit allowances. You send a URL, it routes the request through its proxy pool, optionally renders JavaScript in a headless browser, handles basic CAPTCHA, and hands back HTML. Parsing, storage and scheduling stay on your side.

| Plan | Monthly price (annual) | Credits/month | Concurrency | Geolocation | Get it |
| --- | --- | --- | --- | --- | --- |
| Free | $0 | 1,000 | 5 | — | [ Start free](https://www.scraperapi.com/?fp_ref=coupons) |
| Hobby | $49 ($44.10) | 100,000 | 20 | US / EU | [ Hobby at $49/mo](https://www.scraperapi.com/?fp_ref=coupons) |
| Startup | $149 ($134.10) | 400,000 | 50 | US / EU | [ Startup at $149/mo](https://www.scraperapi.com/?fp_ref=coupons) |
| Business | $299 ($269.10) | 1,000,000 | 100 | Global | [ Business at $299/mo](https://www.scraperapi.com/?fp_ref=coupons) |
| Scaling | $475 ($427.50) | ~3,000,000+ | Higher | Global | [ Scaling at $475/mo](https://www.scraperapi.com/?fp_ref=coupons) |
| Enterprise | Quoted | 3M+ / custom | Custom | Global, dedicated pools | [ Request an Enterprise quote](https://www.scraperapi.com/?fp_ref=coupons) |

Annual billing takes 10% off every plan. The free tier runs 1,000 credits a month with 5 concurrent connections, and new accounts get a 7-day trial with 5,000 credits and no credit card. ScraperAPI also sells larger self-serve tiers above Scaling and negotiates Enterprise contracts, but credit allowances at that end change often enough that quoting them here would be guesswork.

## How many pages 100,000 credits actually buys

On a simple HTML page, one request costs one credit. ScraperAPI's own documentation prices everything else separately: JavaScript rendering takes 5 to 10 credits per request, Amazon costs 5 credits, Google and Bing cost 25, LinkedIn costs 30, and any page behind Cloudflare, DataDome or PerimeterX adds 10 credits when the bypass is used.

That multiplier is where budget plans go wrong. Hobby's 100,000 credits is 100,000 pages only if every request is plain HTML. At 5–10 credits per rendered page it covers 10,000 to 20,000 pages. Point the same plan at LinkedIn and you get roughly 3,300 requests before it stops.

Run the numbers on a real job. Watching 400 Amazon product pages once a day for a month costs 400 × 30 × 5 = 60,000 credits, which fits inside Hobby at $49. Check them twice a day and you need 120,000 credits, which pushes you to Startup at $149, even though you'd use less than a third of the 400,000 credits you're now paying for. Startup's 400,000 credits is 80,000 rendered pages at 5 credits each. Business at $299 gives 1,000,000 credits and 100 concurrent connections, and that's the tier most teams land on once rendering runs on every request.

👉 [Compare what each ScraperAPI tier includes](https://www.scraperapi.com/?fp_ref=coupons)

## The geolocation gate that moves your floor from $49 to $299

Hobby and Startup route through US and EU IPs. Country-level targeting outside those regions, which is what you need for a Brazilian retailer, a Japanese marketplace or an Indian classifieds site, starts at Business for $299/month. There's no add-on and no per-request surcharge that unlocks it earlier.

That one line decides more budgets than credit volume does. A team pulling 30,000 pages a month from German sites is fine on Hobby at $49. The same team adds a Mexican price comparison site and lands on Business at $299, six times the spend for the same page count.

👉 [See the Business tier's global targeting at $299/mo](https://www.scraperapi.com/?fp_ref=coupons)

## What Bright Data charges, line by line

Bright Data doesn't sell a single plan with a single credit pool. Each product has its own meter, which is why flat comparisons against ScraperAPI's $49 tend to fall apart.

- **Web Scraper API:** about $1 per 1,000 requests pay-as-you-go, with 5,000 free records a month shared across the API products.
- **Per-record pricing:** $1.50 per 1,000 records on pay-as-you-go, falling to roughly $0.84 at the $999/month tier (about 1.2 million records) and $0.79 at $1,999/month.
- **Scraping Browser:** $5–8 per GB, with the entry plan around $499/month for roughly 71GB.
- **Residential proxies:** $8–15 per GB pay-as-you-go, down to about $3 per GB on committed volume.
- **Datacenter proxies:** $1–2 per GB.
- **Managed datasets:** $500 to $5,000+ per dataset.

Per-GB pricing punishes small jobs. A $499 Scraping Browser plan used for 50GB still costs $499, and unused commitment doesn't carry into the next month. Bandwidth is metered in both directions, every product bills separately, and zone-level spend caps update on a delay, so a pipeline that touches residential proxies, the Unlocker and the Browser API pays three meters and can overshoot all of them. At 100,000 pages a month this is expensive next to a $49 or $149 credit plan. At 2 million pages the same per-GB rate compresses and the arithmetic reverses.

## ScraperAPI vs Bright Data, side by side

|  | ScraperAPI | Bright Data |
| --- | --- | --- |
| What you're buying | Rendering API: URL in, HTML out | Proxy network, cloud browser, managed datasets |
| Hard-target unblocking | Basic CAPTCHA solving; Cloudflare bypass adds 10 credits | Web Unlocker for Cloudflare, DataDome, Imperva, plus fingerprint handling |
| Geolocation | US/EU on Hobby and Startup, global from Business | Country, city and ASN targeting on every plan |
| Billing unit | Monthly credits, per request | Per GB of bandwidth or per record |
| Cheapest paid entry | $49/month (Hobby, 100K credits) | Pay-as-you-go; about $499/month for the Scraping Browser plan |
| Fits | Small to mid volume, drop-in proxy layer | Hard targets, 1M+ pages, prebuilt datasets |

Third-party review aggregation puts Bright Data at 4.9/5 from more than 2,850 reviews against 4.6/5 from 850+ for ScraperAPI. Success-rate claims deserve more suspicion. ScraperAPI's own comparison pages cite 99.99% against 99.79% for Bright Data, while a benchmark run by Scrape.do across 11 providers placed Bright Data first on average success rate. Both figures come from someone selling something, and they measure different things: ScraperAPI's number is about completed scrapes, Bright Data's 99.99% is an uptime SLA.

## Which one fits your workload

1. **Under 100,000 pages a month, mostly plain HTML, US/EU targets.** Hobby at $49. Nothing else in this comparison is close on price.
2. **100,000 to 500,000 pages with rendering on most requests.** Startup at $149 covers about 80,000 rendered pages; past that you're on Business. The commonly quoted 500,000-page crossover assumes plain HTML fetches, and rendering cuts it by a factor of five to ten.
3. **Any target outside the US and EU.** Business at $299 is the floor regardless of volume.
4. **LinkedIn, Cloudflare-heavy retail, logged-in flows.** Bright Data's Web Unlocker, budgeted at $300–500/month. A $100–150 ScraperAPI setup against LinkedIn is likely to fail.
5. **A million pages a month and up.** Bright Data wins on cost per page as per-GB pricing compresses. Between 500,000 and a million the two are close enough that you should choose on unblocking, not price.
6. **Mixed target lists.** Send the simple 80% through ScraperAPI and the hard 20% through Bright Data. The combined bill usually lands below moving everything to Bright Data.

## Where each one falls short

ScraperAPI has no prebuilt datasets, no cloud browser, no mobile or ISP proxies and no fingerprint spoofing. If you need a browser, you run your own Playwright. CAPTCHA handling is basic, so Cloudflare and DataDome targets fail often even though the credit surcharge exists. Credit costs shift with your domain list, which makes forecasting awkward. Pay-as-you-go overage only exists from Scaling upward; on Hobby and Startup your options when credits run out are pause or auto-upgrade. The 7-day refund is the vendor's stated policy rather than a statutory right.

👉 [Compare the Hobby and Startup allowances at $49 and $149](https://www.scraperapi.com/?fp_ref=coupons)

Bright Data's KYC is strict. You'll be asked to justify your use case, and residential or mobile traffic waits for compliance clearance before it flows. The dashboard assumes you buy proxies by the terabyte, and new users get lost in it. Per-GB billing runs away without spend caps, and the caps themselves update on a 15-minute cycle. Users report occasional Cloudflare bypass failures even with the Unlocker in front. There's no refund guarantee.

## Moving later costs an afternoon

Switching doesn't mean rewriting your scraper. The proxy layer is a URL and a set of parameters; your Scrapy spiders, Playwright scripts and parsers stay as they are. Teams typically start on ScraperAPI because the integration is one API call, move the hard 20% of targets to Bright Data when blocks become the bottleneck, and shift the rest once page volume passes a million a month and per-GB pricing starts to win.

## FAQ

**Which is cheaper, ScraperAPI or Bright Data?**
At 100,000 to 500,000 pages a month, ScraperAPI. Hobby at $49 and Startup at $149 are hard to beat per page on simple and moderately protected sites. At a million pages and up, Bright Data's per-GB rates compress and usually come out ahead. Between 500,000 and a million, treat price as a tie and decide on unblocking.

**Can ScraperAPI get past Cloudflare?**
Sometimes. It charges 10 extra credits when it does, and its documentation lists Cloudflare, DataDome and PerimeterX among the protections it targets. Third-party write-ups report failures on aggressively defended sites. If Cloudflare is the main obstacle in your pipeline, budget for Bright Data instead.

**Is there a free trial?**
Yes. The free plan gives 1,000 credits a month and 5 concurrent connections, and new accounts get a 7-day trial with 5,000 credits, no credit card required.

**Is annual billing worth it?**
It takes 10% off every tier: $44.10 instead of $49, $134.10 instead of $149, $269.10 instead of $299, $427.50 instead of $475. If you're still testing whether your target list is scrapeable, stay monthly. Credits reset each cycle and don't roll over.

**Can I buy just proxies from ScraperAPI?**
No. It's an API, and the proxy rotation comes bundled with request handling. Bright Data sells standalone residential, datacenter, ISP and mobile proxies if raw IPs are all you need.

**What happens when credits run out?**
Scraping pauses until the next cycle unless you enable auto-upgrade, which moves you to the next plan automatically. Pay-as-you-go overage is available from Scaling upward.

## Before you pick

US/EU targets, mostly plain HTML, under 500,000 pages a month: take Hobby at $49 and step up to Startup when rendering eats the credits. Any target that needs an IP outside the US or EU: start at Business. LinkedIn, Cloudflare or a million pages a month: Bright Data is the product that finishes the job.

Two questions to answer before you pay. Does every domain on your list resolve from a US or EU IP? And what share of your monthly requests need JavaScript rendering? Those two answers move the bill by a factor of six, from $49 to $299, more often than raw page count does.

👉 [Start with the $49 Hobby plan and its 5,000 trial credits](https://www.scraperapi.com/?fp_ref=coupons)
