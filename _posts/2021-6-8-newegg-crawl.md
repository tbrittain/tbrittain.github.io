---
layout: post
title: newegg-crawl
---

NVidia and AMD graphics cards have been in short supply these past two years (massive understatement). I have been wanting to upgrade by old Evga GTX 1060 card for a while now, but any GeForce 20 or 30 series and Radeon 60 series cards seem to be perpetually out-of-stock, to the dismay of loads of gamers and hobbyists worldwide (including myself). One solution is to pay the scalpers their 50+% upsale on the cards they manage to buy, but ethically I am strongly against supporting them. The other solution, of course, is to code my own bot to notify when cards I am interested in are available. As the old saying goes, "if you can't beat them, join them." (Although I would not be "joining them" necessarily, as I'm not trying to scalp cards, only trying to get one for myself)

That is where [newegg-crawl](https://github.com/tbrittain/newegg_crawl) comes in. I love the retailer Newegg and generally prefer to purchase my computer components from them over other retailers. I found a [generic graphics cards results page on their site](https://www.newegg.com/p/pl?N=100007709) and wanted to scrape the product results from it, with the end goal of notifying myself whenever a product of interest is detected in stock.

Given a generic graphics card results page, I used Selenium with Firefox's Gecko webdriver to crawl through the webpage results. Within the configuration file, I made it so there are a list of keywords that each item title is compared against, and the items that match one or more of the keywords are saved to a log.xlsx file.

Since buying graphics cards nowadays requires timing when the item is in stock, I didn't want to solely log the results to an xlsx file to look at later. Since I primarly use Windows, I utilized the [win10toast package](https://pypi.org/project/win10toast/) to notify me on my desktop whenever an item I am looking for is detected in stock.

This solution works for when I am at my computer, but I wanted there to be a way to remotely detect when an item is in stock as well. I had a few options. I considered using [Twilio](https://www.twilio.com/) for text message notifications, but the service only has a free trial period, and after that I would need to pay for text messages. Furthermore I did not really want to set up a Flask server to connected to the Twilio API.

Since I use [Discord](https://discord.com/) both on my computer and mobile (and have experience using [Discord.py](https://github.com/Rapptz/discord.py) to code bots), I ultimately went with setting up the crawler as a Discord bot. This allowed me to receive Discord notifications whenever a product was in stock, which is the next best thing to text messages. I also considered creating a Groupme or WhatsApp bot, but I just don't really use those services as often as I do Discord.

One other alternative I have been considering is setting up a method to email myself results from the searches. I don't check my email often enough for it to be a viable way to know when products are in stock, but I am considering setting this up to receive daily emails about price fluctuations, and perhaps deduce the time at which products are placed in stock. I may do this in conjunction with an SQlite database to store historical product information. That is in the works!
