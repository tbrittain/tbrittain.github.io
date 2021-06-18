---
layout: post
title: vaultbot update 1
---

VaultBot has been an ambitious ongoing project of mine. Since [I last outlined my planned changes to the project](https://tbrittain.com/vaultbot/), I have made pretty decent progress towards achieving those goals.

The first step I took toward updating VaultBot was normalizing the PostgreSQL database. I went into this in more detail in my previous post, but I essentially went about this by dumping the tables from the old database and editing the data in Excel to fit the schema of some of the new tables. This was not possible for the `artists_genres` table. Also, in preparation of the React app frontend, I wanted each song to have an associated album art and preview URL (if applicable), and for each artist to have their art (usually an image of the band) associated with them.

I then copied the modified data from Excel into the new tables. To approach the `artists_genres` table and the missing columns, I first handled the missing columns by going back and querying that missing data from Spotify's API and added the corresponding data to the new database. For the `artists_genres` table, I took each unique artist ID and queried the artist information from Spotify's API, which provided the genres.

Significant refactoring took place in the existing VaultBot Discord bot code. As per my goals for the project, I eventually want to set up a dynamic React app for the frontend rather than generating static websites that present playlist data, so I got rid of the R and Rmarkdown code that generated those static sites. I did preserve an image of what the site looked like before deleting it, so you can check that out [here](https://web.archive.org/web/20210618053632/http://vaultbot.tbrittain.com/).

Additionally, I tried to reduce the amount of API calls that were made to the Spotify API. There were a number of functions that relied on retrieving playlist data by pulling it from Spotify rather than the playlist data present in the database, so I refactored quite a few functions to instead pull from the database.

The overall file structure of the project also had some major changes. I compartmentalized the VaultBot Discord bot into its own directory and created two additional directories for the Express backend and React frontend, which are the next steps in the project. I am also wanting to Dockerize the entire application, so I created Dockerfiles and a `docker-compose.yml` file in the parent directory in preparation of this step.

One change that I did not explicitly plan for but welcomed was the addition of was so-called "aggregate playlists." Given that the archive song data had been sitting around mostly untouched for the duration of the project, I wanted to create a new feature to utilize this data. The general idea behind these aggregate playlists was for each of them to have a theme, and then try to isolate songs using the existing song characteristics to match each playlist.

The aggregate playlists I decided to create were as follows:
1. A playlist tracking the top 50 tracks (in terms of number of times added to the dynamic playlist, i.e. by number of occurrences in the archive playlist),
2. A party playlist of high-tempo, energetic songs,
3. A chill playlist of downtempo, atmospheric or acoustic songs,
4. A "light" playlist of happy, easy-listening songs,
5. and a "moody" playlist of more emotional, complex, ruminating songs.

In practice, what this meant was querying the database using the song characteristics to pull songs that fulfilled the criteria weighted by their count. I am pretty happy with the tuning of the characteristics for each playlist, but one aspect that I want to experiment with would be integrating genre data into the query.

Genre information would be particularly helpful for if I wanted to split the party playlist into a party and a get-together playlist. The get-together playlist is currently how the party playlist is, with lots of upbeat indie and alt rock, but the party playlist (in my opinion) should weigh some rap and EDM genres more heavily.

Here are the playlists for you to check out:

<iframe src="https://open.spotify.com/embed/playlist/1b04aMKreEwigG4ivcZNJm?theme=0" width="100%" height="380" frameBorder="0" allowtransparency="true" allow="encrypted-media"></iframe>

<iframe src="https://open.spotify.com/embed/playlist/6ksVLVljYiEUpjSoDh8z0w?theme=0" width="100%" height="380" frameBorder="0" allowtransparency="true" allow="encrypted-media"></iframe>

<iframe src="https://open.spotify.com/embed/playlist/65PiacgUM34qS9EtNgbr5r?theme=0" width="100%" height="380" frameBorder="0" allowtransparency="true" allow="encrypted-media"></iframe>

<iframe src="https://open.spotify.com/embed/playlist/5gsgXQu45m0W06WkmWXQBY?theme=0" width="100%" height="380" frameBorder="0" allowtransparency="true" allow="encrypted-media"></iframe>

<iframe src="https://open.spotify.com/embed/playlist/0jiEtmsU9wRGrAVf7O5YeT?theme=0" width="100%" height="380" frameBorder="0" allowtransparency="true" allow="encrypted-media"></iframe>