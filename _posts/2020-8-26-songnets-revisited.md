---
layout: post
title: songnets revisited
---

Since my original days tinkering with SpotifyR and exporting my playlist data using other tools, I wanted to create a more streamlined way of generating the type of data that I desired to visualize in my so-called "songnets". After experimenting with Python, I designed a workflow to do just that. Thus, [spotify-netviz](https://github.com/tbrittain/spotify-netviz) was born.

The readme on the project page explains it in detail, but the general idea of the tool is to be an all-encompassing way to generate graph data for your Spotify library in the form of an edges table, a nodes table, and a spreadsheet with specific song detail information for each song in your playlists. It has the ability to read from your "Liked" songs, and additionally any playlists that you manually denote.

Using this project, I generated a new version of my song library using a similar workflow as [my other songnet project](https://tbrittain.com/songnets/), which you can check out [here](https://tbrittain.com/new-viz-library/). The data itself is visualized using [this viewer](https://github.com/raphv/gexf-js). A couple of cool features that I added that weren't present in my previous project were album art previews on albums and songs within an album, song previews (for songs that had previews available), and links to the genres on [EveryNoise](https://everynoise.com/engenremap.html). The connections between artists and genres is incredibly cool to observe in detail, so I hope you have enjoy it as much as I have!

[<img src="{{ site.baseurl }}/images/spotify-networks/networkv3.jpg" style="width: 800px;"/>]
