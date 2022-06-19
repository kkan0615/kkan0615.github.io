---
title: Node js web crawling with puppeteer and cheerio
author: Youngjin Kwak
date: 2022-06-18 11:36:00 +0800
categories: [Typescript, Javascript]
tags: [typescript, node, javascript]
---
![web-crawler](https://cdn-icons-png.flaticon.com/512/531/531270.png)

> There is error on table
{: .prompt-danger }

# Overview
For Node js, there are two ways to scrap the web pages. One is puppeteer and the other way is cheerio. <br>
Both way has their own advantage and disadvantage. Some developers including me uses both libraries for wb web crawling.

# What is different between cheerio and puppeteer

| Compare     | Cheerio    | Puppeteer    |
|:------------|:-----------|:-------------|
| interaction | Dom phaser | Good for SPA |
| interaction | Impossible | possible     |
| Syntax      | Simple     | Complex      |
| headless    | true       | false        |

| Company                      | Contact          | Country |
|:-----------------------------|:-----------------|--------:|
| Alfreds Futterkiste          | Maria Anders     | Germany |
| Island Trading               | Helen Bennett    | UK      |
| Magazzini Alimentari Riuniti | Giovanni Rovelli | Italy   |

# How to use
We will try to phase the Amazon for example
<br>

[//]: # (# Cheerio)

[//]: # (# Puppeteer)

## Combination
This example will handle both libraries together.

```typescript
import puppeteer from 'puppeteer'
import $ from 'cheerio'

const test = async () => {
  try {
    const browser = await puppeteer.launch()
    const page = await browser.newPage()
    await page.goto('https://www.amazon.ca', {
      waitUntil: 'networkidle2'
    })

    /* Search with input */
    await page.waitForSelector('#twotabsearchtextbox')
    // Add input data to serach input field
    await page.$eval('#twotabsearchtextbox', el => (el as HTMLInputElement).value = 'silent red switches')
    // Press search button
    await page.click('#nav-search-submit-button')
    await page.waitForNavigation({
      waitUntil: 'networkidle2'
    })
    // Screen shot the pages
    await page.screenshot({ path: 'example.png' })

    // Get the page DOM
    const pageHTML = await page.evaluate(() => document.body.innerHTML)
    // Use Cheerio to phaser DOM
    const result: Record<string, any>[] = []
    $('div[data-component-type="s-search-result"]', pageHTML).each((i, el) => {
      // Get price symbol
      const priceSymbol = $(el).find('.a-price-symbol').text()
      // Get sale and original price
      const foundPriceWhole = $(el).find('.a-offscreen')
      const priceWhole = foundPriceWhole.length >= 2 ? foundPriceWhole.last().text() : ''
      const salePriceWhole = foundPriceWhole.length >= 2 ? foundPriceWhole.first().text() : foundPriceWhole.text()
      // Get the tile
      const title = $(el).find('[class="a-size-base-plus a-color-base a-text-normal"]').text()

      result.push({
        title,
        priceSymbol,
        salePriceWhole,
        priceWhole,
      })
    })

    // Close the brower
    await browser.close()
  } catch (e) {
    console.error(e)
    console.error('Fail!', e.message)
    process.exit(1)
  }
}

test()
```

# Important
You are not allowed to scrap all webSites for security. <br>
You are only allow to scrap that mentioned on **"robots.txt"**

```
# robots.txt file for YouTube
# Created in the distant future (the year 2000) after
# the robotic uprising of the mid 90's which wiped out all humans.

User-agent: Mediapartners-Google*
Disallow:

User-agent: *
Disallow: /channel/*/community
Disallow: /comment
Disallow: /get_video
Disallow: /get_video_info
Disallow: /get_midroll_info
Disallow: /live_chat
Disallow: /login
Disallow: /results
Disallow: /signup
Disallow: /t/terms
Disallow: /timedtext_video
Disallow: /user/*/community
Disallow: /verify_age
Disallow: /watch_ajax
Disallow: /watch_fragments_ajax
Disallow: /watch_popup
Disallow: /watch_queue_ajax

Sitemap: https://www.youtube.com/sitemaps/sitemap.xml
Sitemap: https://www.youtube.com/product/sitemap.xml
```
This robots.txt are from Youtube. You are not allowed to scrap the page on "Disallow". <br>
That means it's possible to scrap all pages except them

## How to check robots.txt
It's very simple to check them. just add /robots.txt at the last the url you would like to pharse<br>
Example) https://www.example.com/robots.txt

# Support
[!["Buy Me A Coffee"](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/youngjinkwak)

# Updates
## [06-18-2022]
- Add image
