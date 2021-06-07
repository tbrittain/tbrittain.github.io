---
layout: post
title: vaultbot
---

*Copied from [about Vaultbot](http://vaultbot.tbrittain.com/about.html).*

>I create too many playlists. What usually happens is:
>1. I make a playlist,
>2. I add songs to the playlist,
>3. and I listen to the playlist for some amount of time.
>
>Inevitably, the playlist starts to become stale, so I consider it archived and move on to a new playlist ad infinitum.
>
>What if there were a playlist that didn't become stale? I'm a fan of the Spotify-curated playlists and the similar ones for Spotify genres by EveryNoise, but my ideal playlist is one that I have control over as well.
>
>VaultBot is the solution to both of these problems. [VaultBot](http://vaultbot.tbrittain.com/) is a Discord bot that moderates a dynamic and an archive playlist. When a user provides a Spotify track to VaultBot, it adds the song to both the dynamic and archive playlists. After two weeks, VaultBot removes the track from the dynamic playlist.
>
>Additionally, VaultBot keeps track of every song added and reports various statistics for each track in the form of an interactive table, some 'high scores', and more advanced statistical analyses.
>
>I created this project not only for my own sake, but also for it to be a new way to share and think about music with friends. If you are in a Discord server with VaultBot, you are welcome to add songs to the playlists. VaultBot is not currently available for public use, but may be one day.
>
>In the meantime, if you are able to make use of VaultBot, I hope it brings some new musical joy to your life. It sure has for me! :)

[<img src="{{ site.baseurl }}/images/vaultbot/site-preview.jpg" style="width: 800px;"/>](https://tbrittain.github.io/vaultbot/)

Overall, VaultBot is the solution to my desire for a dynamically-evolving playlist that I (and any of my friends) have complete control over. Additionally, it also fulfills my desire for listening statistics that Spotify does not currently offer users to directly view.

As of this writing, there have been a total of 3,060 songs that have been added to VaultBot. I have every intention of keeping VaultBot alive and well, and I am excited to analyze how my musical tastes change over time.

[<img src="{{ site.baseurl }}/images/vaultbot/archive.jpg" style="width: 800px;"/>](https://tbrittain.github.io/vaultbot/)

Currently, the VaultBot stack includes a Python backend (via the Discord bot), a PostgreSQL database to store song data in the forms of the Dynamic and Archive playlists, and Rmarkdown files that run as subprocesses of the Python backend to render the statistical analysis webpages as static HTML, which are uploaded to a Google Cloud bucket for [vaultbot.tbrittain.com](vaultbot.tbrittain.com).

This was a tolerable design for a rudimentary build of the project, but I have since been brainstorming ways to improve what I already have. The first big step is to normalize the Postgres database:

[<img src="{{ site.baseurl }}/images/vaultbot/normalization.jpg" style="width: 800px;"/>](https://tbrittain.github.io/vaultbot/)

In doing this, I will be able to much more easily perform interesting queries upon the data, including analyzing genre information over time, as well as all sort of other fun joins. I also want to containerize the entire VaultBot process using Docker and fully host it it on the cloud. I am also planning on completely revamping the VaultBot website as a single-page web application using React. In doing so, I also want an Express backend to handle querying the Postgres database. It would also make sense to refactor much of the existing Python code to minimize the number of HTTP requests made to the Spotify API, as well as updating the Discord bot portion to the most recent version. This is going to be a long-term goal of mine, but it will be very worth it for a dynamic web site and performant backend structure.
