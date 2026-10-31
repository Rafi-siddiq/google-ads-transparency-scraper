<!-- Landing README for a public GitHub repo. The Actor runs on Apify; this repo is for discovery and issues. -->
[![Run on Apify](https://img.shields.io/badge/Run%20on-Apify-0d9488?style=for-the-badge)](https://apify.com/rsiddiq95/google-ads-transparency-scraper)

# Google Ads Transparency Scraper

See every Google ad a competitor runs. Enter a **website**, an **advertiser name**, or an **advertiser ID**, and get each ad from the [Google Ads Transparency Center](https://adstransparency.google.com/) with its **actual ad copy**, images, format, platform, and the dates it ran.

## What can this Google Ads scraper do?

- 🔍 **Find ads three ways.** By the website the ads link to (`nike.com`), by verified advertiser name (`Nike, Inc.`), or by advertiser ID or URL.
- ✍️ **Get the ad copy.** Headlines, descriptions, and extension text are pulled from Google's ad previews, so you can read competitors' messaging without opening each ad.
- 🖼️ **Images and previews.** Archived ad images and a link to every ad in the Transparency Center.
- 📅 **Run dates.** When each ad was first and last shown, and for how many days.
- 🎯 **Filters.** Country, format (text, image, video), platform (Search, YouTube, Shopping, Maps, Play), and date range.
- 🌍 **Countries and variations.** Optionally, every country an ad ran in and all of its variations.
- 💸 **Fair billing.** You pay per ad returned. Lookups that fail or find nothing are free.

## Who uses Google Ads Transparency data?

- **Marketers and agencies** tracking competitors' messaging, offers, and creative tests.
- **PPC specialists** collecting ad copy ideas for a niche.
- **Brand protection teams** spotting advertisers who use their brand or domain.
- **Researchers** studying advertising over time.

## How to scrape Google ads

1. Click **Try for free**.
2. Add one or more **advertiser websites**, **names**, or **IDs**.
3. Optionally choose a **region**, **format**, **platform**, and **dates**.
4. Set **Max ads per advertiser or website** (newest ads come first).
5. Click **Start** and download the results as JSON, CSV, Excel, or HTML, or use the API.

## Input example

```json
{
    "advertiserDomains": ["nike.com"],
    "advertiserNames": ["Adidas AG"],
    "region": "US",
    "adFormat": "TEXT",
    "platform": "SEARCH",
    "dateFrom": "2026-10-01",
    "maxAdsPerTarget": 200,
    "extractAdCopy": true
}
```

## Output example

```json
{
    "resultType": "ad",
    "query": "nike.com",
    "advertiserId": "AR16735076323512287233",
    "advertiserName": "Nike, Inc.",
    "advertiserLegalName": "Nike, Inc.",
    "advertiserCountry": "US",
    "creativeId": "CR14390493293404225537",
    "format": "TEXT",
    "firstShownAt": "2023-11-17T00:26:00.751Z",
    "lastShownAt": "2026-10-30T00:29:17.265Z",
    "daysShown": 911,
    "landingDomain": "nike.com",
    "imageUrl": "https://tpc.googlesyndication.com/archive/simgad/8844930400868124295",
    "adText": [
        "Nike",
        "nike.com",
        "Nike® Official Site",
        "Las Vegas",
        "2010 Festival Plaza Drive Suite 100",
        "Shop exclusive new styles crafted with the latest Nike® technology & innovations now."
    ],
    "region": "US",
    "adUrl": "https://adstransparency.google.com/advertiser/AR16735076323512287233/creative/CR14390493293404225537?region=US",
    "scrapedAt": "2026-10-30T00:49:19.147Z"
}
```

With **Include variations and regions** turned on, each ad also has `variationCount`, `variationImageUrls`, and `regionsShown` (country codes).

If a name, website, or ID finds nothing, you get a free row with `resultType: "error"` explaining why. For names, it also lists similar advertisers.

## How much does it cost?

You pay per ad returned. See the **Pricing** tab for current prices. Apify's free plan includes monthly credit to try it out.

## Tips

- **Websites find more.** A website search returns ads from every advertiser account that links to it, including resellers and agencies.
- **Exact names.** Advertiser names must match the verified name exactly (case and punctuation don't matter). Turn off **Exact advertiser name match** to include every advertiser whose name contains your text.
- **Ad copy availability.** Google shows a text preview for many ads but stores some only as images. When there is no text preview, `adText` is `null` and the image is still provided.
- **Platform filter.** Google only tracks platforms for ads shown since September 2023.

## Limitations

- This Actor reads the public Ads Transparency Center website, which has no official API. Google can change it at any time; we monitor the Actor and update it when that happens.
- Google limits how fast the site can be read, so the Actor paces itself. Large runs (thousands of ads) take longer.
- Google reports the total number of ads as a range, for example "7000-8000".

## Works well with

- **[Google Sheets Sync](https://apify.com/rsiddiq95/google-sheets-sync):** schedule this Actor daily and upsert by `creativeId`, so your competitor-ads sheet updates existing ads and adds only new ones.
- **[Google Trends Scraper](https://apify.com/rsiddiq95/google-trends-scraper):** check search interest for the products and offers your competitors are advertising.

## FAQ

**Is it legal to scrape the Google Ads Transparency Center?**
Google publishes this data publicly so anyone can see who is advertising. This Actor collects only that public information about advertisers and their ads, not data about people. Make sure your use complies with Google's terms and the laws that apply to you.

**Can I schedule it or connect it to other tools?**
Yes. Schedule runs to track competitors over time, call it through the Apify API, or send results to Google Sheets, Make, Zapier, n8n, and more through Apify integrations.

**Something isn't working.**
Open an issue on the **Issues** tab with your input, and we'll respond quickly.

## Links

- Apify Store page: https://apify.com/rsiddiq95/google-ads-transparency-scraper
- Questions and bug reports: open an issue here or on the Actor's Issues tab.
