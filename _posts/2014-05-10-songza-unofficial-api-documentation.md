---
layout: post
title: Songza Unofficial API Documentation
date: 2014-05-09
updated: 2014-05-09
categories: code songza music api
---

A rough documentation of the Songza API.

If you would like to improve the contents of this page, please do! Send a pull request on the GitHub repo for this site: https://github.com/trevorsenior/tsenior_static (located in source/_posts/2014-05-10-songza-unofficial-api-documentation.md)





## Cookies & Authentication

Songza uses a `sessionid` cookie that should me maintained on requests to the API (e.g. for "next" to work properly in stations / etc.). I'm not 100% sure on this though.

Some routes require a user account to play around with.





## Songs

### details (GET)

```
http://songza.com/api/1/song/<song id>
http://songza.com/api/1/song/12442598
```

**response**

```json
{
    "album": "Simple Things",
    "artist": {
        "image_url": "http://songza.com/api/1/artist/511ace89e9e23d724def2fd7/image",
        "id": "511ace89e9e23d724def2fd7",
        "name": "Zero 7"
    },
    "external_media": {
        "youtube": {
            "id": "Z0Xcn_OrPq0"
        }
    },
    "title": "Give It Away",
    "cover_url": "http://images.mndigital.com/albums/005/165/437/a.jpeg",
    "genre": "Electronica/Dance",
    "pa": false,
    "formats": [
        {
            "available": true,
            "format": "aac"
        },
        {
            "available": true,
            "format": "mp3"
        }
    ],
    "duration": 317,
    "id": 12442598
}
```





## Search

### artist (GET)

Get artists based on a query.

```javascript
// Query parameters
query="search"
limit=<int>
```

```
http://songza.com/api/1/search/artist?query=spears
```

**response**

```json
[
    {
        "image_url": "http://songza.com/api/1/artist/511acdf2e9e23d724deed520/image",
        "id": "511acdf2e9e23d724deed520",
        "name": "Britney Spears"
    },
    {
        "image_url": "http://songza.com/api/1/artist/511acad5e9e23d724decd91e/image",
        "id": "511acad5e9e23d724decd91e",
        "name": "Burning Spear"
    },
    {
        "image_url": "http://songza.com/api/1/artist/529ab2eb0ab1960e1f25bf4a/image",
        "id": "529ab2eb0ab1960e1f25bf4a",
        "name": "Jamie Lynn Spears"
    }
]
```

### situation (GET)

Get "situations" based on a query.

```javascript
// Query parameters
query="search"
style="flat-220" // styling stuff - icon size. optional, defaults to 70
```

```
http://songza.com/api/1/search/situation?query=snoop&style=flat-220
```

**response**

```json
[
    {
        "title": "Mellowing Out with Snoop",
        "situations": [],
        "selected_message": "Pick one of deez playlists, curated by Snoop D-O-Double-G.",
        "station_ids": [
            1725331,
            1718546,
            1710403
        ],
        "id": "534c2c2fc9df2535a663ff52",
        "icon": "http://d2t03vq6udg69j.cloudfront.net/api/1/situation/id/534c2c2fc9df2535a663ff52/image?d=1397502018&size=220"
    }
]
```

### station (GET)

Get stations based on a query.

```javascript
// Query parameters
query="search"
limit=<int>
```

```
http://songza.com/api/1/search/station?query=snoop
```

**response**

```json
[
    {
        "dasherized_name": "puff-puff-snoop-snoop_dogg",
        "status": "NORMAL",
        "global_station": null,
        "name": "Puff, Puff, Snoop",
        "creator_name": "Snoop Dogg",
        "url": "http://songza.com/listen/puff-puff-snoop-snoop_dogg/",
        "song_count": 52,
        "cover_url": "http://d2t03vq6udg69j.cloudfront.net/api/1/station/1710403/image",
        "featured_artists": [
            {
                "name": "Kendrick Lamar"
            },
            {
                "name": "OutKast"
            },
            {
                "name": "Big Krit"
            },
            {
                "name": "A$AP Rocky"
            },
            {
                "name": "Snoop Dogg & Wiz Khalifa"
            }
        ],
        "creator_id": 13167920,
        "type": "basic",
        "id": 1710403,
        "description": "Mellow out with this playlist of chill-ass rap and R&B, all hand-picked by Snoop. Fo shizzle."
    }
]
```

### song (GET)

Get songs based on a query

```javascript
// Query parameters
query="search"
limit=<int; 200>
```

```
http://songza.com/api/1/search/song?query=britney%20spears&limit=1
```

**response**

```json
{
    "songs": [
        {
            "album": "Britney",
            "artist": {
                "image_url": "http://songza.com/api/1/artist/511acdf2e9e23d724deed520/image",
                "id": "511acdf2e9e23d724deed520",
                "name": "Britney Spears"
            },
            "title": "Lonely",
            "cover_url": "http://images.mndigital.com/albums/027/961/515/a.jpeg",
            "genre": "Pop",
            "pa": false,
            "formats": [
                {
                    "available": true,
                    "format": "aac"
                },
                {
                    "available": true,
                    "format": "mp3"
                }
            ],
            "duration": 199,
            "id": 4579913
        }
    ]
}
```





## Stations

### details (GET)

Get details for a station.

```
http://songza.com/api/1/station/<station id>
http://songza.com/api/1/station/1399111
```

**response**

```json
{
    "dasherized_name": "downtempo-instrumentals-tenmillionsounds",
    "status": "NORMAL",
    "global_station": null,
    "name": "Downtempo Instrumentals",
    "creator_name": "Jesse Sussman",
    "url": "http://songza.com/listen/downtempo-instrumentals-tenmillionsounds/",
    "song_count": 66,
    "cover_url": "http://d2t03vq6udg69j.cloudfront.net/api/1/station/1399111/image",
    "featured_artists": [
        {
            "name": "Tycho"
        },
        {
            "name": "Hiatus"
        },
        {
            "name": "Emancipator"
        },
        {
            "name": "Bonobo"
        },
        {
            "name": "Air"
        }
    ],
    "creator_id": 1080874,
    "type": "basic",
    "id": 1399111,
    "description": "Hypnotic breaks and pensive soundscapes from today's greatest electronica artists: the perfect soundtrack for reading, working, or just relaxing."
}
```

### similar (GET)

Get similar stations.

```
http://songza.com/api/1/station/<station id>/similar
```

**response**

```json
[
    {
        "dasherized_name": "blissed-out-beats-tenmillionsounds",
        "status": "NORMAL",
        "global_station": null,
        "name": "Blissed-Out Beats",
        "creator_name": "Jesse Sussman",
        "url": "http://songza.com/listen/blissed-out-beats-tenmillionsounds/",
        "song_count": 66,
        "cover_url": "http://d2t03vq6udg69j.cloudfront.net/api/1/station/1682151/image",
        "featured_artists": [
            {
                "name": "Taku"
            },
            {
                "name": "Apollo Brown"
            },
            {
                "name": "Oddisee"
            },
            {
                "name": "Handbook"
            },
            {
                "name": "Emancipator"
            }
        ],
        "creator_id": 1080874,
        "type": "basic",
        "id": 1682151,
        "description": "Hypnotic instrumental beats from new artists who blend the funky, sample-based approach of J Dilla with the soothing, electronic flourishes of downtempo producers."
    },
    {
        "dasherized_name": "keep-dreaming-morning-downtempo-tenmillionsounds",
        "status": "NORMAL",
        "global_station": null,
        "name": "Keep Dreaming: Morning Downtempo ",
        "creator_name": "Jesse Sussman",
        "url": "http://songza.com/listen/keep-dreaming-morning-downtempo-tenmillionsounds/",
        "song_count": 48,
        "cover_url": "http://d2t03vq6udg69j.cloudfront.net/api/1/station/1713666/image",
        "featured_artists": [
            {
                "name": "Helios"
            },
            {
                "name": "Goldmund"
            },
            {
                "name": "Max Richter"
            },
            {
                "name": "Explosions In The Sky"
            },
            {
                "name": "The Album Leaf"
            }
        ],
        "creator_id": 1080874,
        "type": "basic",
        "id": 1713666,
        "description": "This playlist is designed for that perfect moment between consciousness and unconsciousness -- when you're awake but still dreaming -- because sometimes a \"snooze\" should last much longer than nine minutes."
    },
    {
        "dasherized_name": "wayfarer-soul-adawar",
        "status": "NORMAL",
        "global_station": null,
        "name": "Wayfarer Soul",
        "creator_name": "Annu Dawar",
        "url": "http://songza.com/listen/wayfarer-soul-adawar/",
        "song_count": 68,
        "cover_url": "http://d2t03vq6udg69j.cloudfront.net/api/1/station/1721420/image",
        "featured_artists": [
            {
                "name": "FM Attack"
            },
            {
                "name": "College"
            },
            {
                "name": "Lazerhawk"
            },
            {
                "name": "Miami Nights 1984"
            },
            {
                "name": "Kavinsky"
            }
        ],
        "creator_id": 12524443,
        "type": "basic",
        "id": 1721420,
        "description": "What would Sonny Crockett listen to today as his cigarette boat grazed the Miami shoreline? These neo-'80s, retro-electro dance songs offer a clue."
    },
    {
        "dasherized_name": "3am-airport-tenmillionsounds",
        "status": "NORMAL",
        "global_station": null,
        "name": "3am Airport",
        "creator_name": "Jesse Sussman",
        "url": "http://songza.com/listen/3am-airport-tenmillionsounds/",
        "song_count": 74,
        "cover_url": "http://d2t03vq6udg69j.cloudfront.net/api/1/station/1380616/image",
        "featured_artists": [
            {
                "name": "Burial"
            },
            {
                "name": "Submotion Orchestra"
            },
            {
                "name": "Boxcutter"
            },
            {
                "name": "Thievery Corporation"
            },
            {
                "name": "Emancipator"
            }
        ],
        "creator_id": 1080874,
        "type": "basic",
        "id": 1380616,
        "description": "Ambient, melancholic trip-hop and IDM that evokes the feeling of being stranded in a large airport late at night."
    },
    {
        "dasherized_name": "mellow-electro-songza",
        "status": "NORMAL",
        "global_station": null,
        "name": "Mellow Electro",
        "creator_name": "Songza",
        "url": "http://songza.com/listen/mellow-electro-songza/",
        "song_count": 106,
        "cover_url": "http://d2t03vq6udg69j.cloudfront.net/api/1/station/1393994/image",
        "featured_artists": [
            {
                "name": "Röyksopp"
            },
            {
                "name": "Goldfrapp"
            },
            {
                "name": "Múm"
            },
            {
                "name": "Air"
            },
            {
                "name": "M83"
            }
        ],
        "creator_id": 1000000,
        "type": "basic",
        "id": 1393994,
        "description": "Not all electro acts aim for the dance floor. Explore the low-key, laid-back side of the style through these well-known names and under-the-radar indie acts."
    }
]
```

### next (GET/POST)

Request the next song in a station play list. This will return a `listen_url` field that can be used to download / stream the song for a short period of time as denoted by the `e` query parameter (unix time when the song expires / it no longer accessible).

```
http://songza.com/api/1/station/<station id>/next
http://songza.com/api/1/station/1399111/next
```

**request**

```javascript
// Parameters
cover_size="g" // ??
format="aac" // or mp3
buffer=0
```

**response**

```json
{
    "vote": "",
    "version": "aac",
    "listen_url": "http://fp-limelight.musicnet.com/mp3/mn_mp3_09_01/downloads/a090/022/227/22227387_3_019.mp4?e=1399650821&h=10e3146482f879a2f38fb67cd11f2aef",
    "skippable": true,
    "song": {
        "album": "Simple Things",
        "status": "ADD",
        "artist": {
            "image_url": "http://songza.com/api/1/artist/511ace89e9e23d724def2fd7/image",
            "id": "511ace89e9e23d724def2fd7",
            "name": "Zero 7"
        },
        "external_media": {
            "youtube": {
                "id": "Z0Xcn_OrPq0"
            }
        },
        "title": "Give It Away",
        "cover_url": "http://images.mndigital.com/albums/005/165/437/a.jpeg",
        "genre": "Electronica/Dance",
        "pa": false,
        "formats": [
            {
                "available": true,
                "format": "aac"
            },
            {
                "available": true,
                "format": "mp3"
            }
        ],
        "duration": 317,
        "new": false,
        "id": 12442598,
        "added_by": null
    }
}
```

If a play list is unreleased you will receive:

```json
{
	"message": "You've reached the end of this playlist. Try the Discover section for more music.",
	"code": "end"
}
```

### downvote (POST)

Downvote (thumbs down) a song in a station.

```
http://songza.com/api/1/station/<station id>/song/<song id>/vote/down
```

**response**

```json
{
    "vote": "DOWN",
    "time": "2014-05-09T21:48:16Z",
    "station": {
        "dasherized_name": "a-chorus-of-angels-songza",
        "status": "NORMAL",
        "global_station": null,
        "name": "A Chorus of Angels",
        "creator_name": "Songza",
        "url": "http://songza.com/listen/a-chorus-of-angels-songza/",
        "song_count": 114,
        "cover_url": "http://d2t03vq6udg69j.cloudfront.net/api/1/station/1393503/image",
        "featured_artists": [
            {
                "name": "The King's Singers"
            },
            {
                "name": "The Hilliard Ensemble"
            },
            {
                "name": "King's College Choir Of Cambridge"
            },
            {
                "name": "Stile Antico"
            },
            {
                "name": "Johann Sebastian Bach"
            }
        ],
        "creator_id": 1000000,
        "type": "basic",
        "id": 1393503,
        "description": "Soothing voices in lovely choral arrangements make for transcendent musical experiences. Choral music, both sacred and secular, can't help but invoke the best of feelings and help create a slice of heaven on Earth."
    },
    "id": "10942882:1393503:5003159",
    "song": {
        "album": "Brahms, Bernstein, & The Boys!",
        "artist": {
            "image_url": "http://songza.com/api/1/artist/511ac3b6e9e23d724de8609e/image",
            "id": "511ac3b6e9e23d724de8609e",
            "name": "San Francisco Gay Men's Chorus"
        },
        "title": "To Thee, Soul Of The Universe, K. 429 - Freemason's Cantata, K. 623 (Sung In German)",
        "cover_url": "http://images.mndigital.com/albums/029/657/769/a.jpeg",
        "genre": "Classical/Opera",
        "pa": false,
        "formats": [
            {
                "available": true,
                "format": "aac"
            },
            {
                "available": true,
                "format": "mp3"
            }
        ],
        "duration": 290,
        "id": 5003159
    }
}
```

### upvote (POST)

Upvote (thumbs up) a song in a station.

```
http://songza.com/api/1/station/<station id>/song/<song id>/vote/up
```

**response**

```json
{
    "vote": "UP",
    "time": "2014-05-09T21:53:26Z",
    "station": {
        "dasherized_name": "a-chorus-of-angels-songza",
        "status": "NORMAL",
        "global_station": null,
        "name": "A Chorus of Angels",
        "creator_name": "Songza",
        "url": "http://songza.com/listen/a-chorus-of-angels-songza/",
        "song_count": 114,
        "cover_url": "http://d2t03vq6udg69j.cloudfront.net/api/1/station/1393503/image",
        "featured_artists": [
            {
                "name": "The King's Singers"
            },
            {
                "name": "The Hilliard Ensemble"
            },
            {
                "name": "King's College Choir Of Cambridge"
            },
            {
                "name": "Stile Antico"
            },
            {
                "name": "Johann Sebastian Bach"
            }
        ],
        "creator_id": 1000000,
        "type": "basic",
        "id": 1393503,
        "description": "Soothing voices in lovely choral arrangements make for transcendent musical experiences. Choral music, both sacred and secular, can't help but invoke the best of feelings and help create a slice of heaven on Earth."
    },
    "id": "10942882:1393503:6007456",
    "song": {
        "album": "Lost In The Stars",
        "artist": {
            "image_url": "http://songza.com/api/1/artist/511acd25e9e23d724dee54c1/image",
            "id": "511acd25e9e23d724dee54c1",
            "name": "Chanticleer"
        },
        "title": "I Can Dream, Can't I?",
        "cover_url": "http://images.mndigital.com/albums/000/113/773/a.jpeg",
        "genre": "Classical/Opera",
        "pa": false,
        "formats": [
            {
                "available": true,
                "format": "aac"
            },
            {
                "available": true,
                "format": "mp3"
            }
        ],
        "duration": 335,
        "id": 6007456
    }
}
```

### create (POST)

Create a new station (playlist of songs)

```
http://songza.com/api/1/station/create
```

**request**

```json
{
    "status": "UNRELEASED",
    "genres": [
        {
            "type": "genre",
            "id": "5156ed2fe9e23d6625cc0995",
            "parent": {
                "type": "genre",
                "id": "5156ed2be9e23d6625cc094b",
                "parent": null,
                "name": "Country"
            },
            "name": "Americana"
        }
    ],
    "advertising": {
        "interstitial_ad": false,
        "display_ad": false
    },
    "name": "Playlist in Progress"
}
```

**response**

```json
{
    "dasherized_name": "playlist-in-progress-trevorsenior",
    "status": "UNRELEASED",
    "global_station": null,
    "name": "Playlist in Progress",
    "creator_name": "trevorsenior",
    "url": "http://songza.com/listen/playlist-in-progress-trevorsenior/",
    "song_count": 0,
    "cover_url": "http://d2t03vq6udg69j.cloudfront.net/api/1/station/1766718/image",
    "featured_artists": [],
    "creator_id": 10942882,
    "type": "basic",
    "id": 1766718,
    "description": ""
}
```

### update (PUT)

Update an existing station information.

```
http://songza.com/api/1/station/1766718
```

**request**

```json
{
    "status": "UNRELEASED",
    "genres": [
        {
            "type": "genre",
            "id": "5156ed2fe9e23d6625cc0995",
            "parent": {
                "type": "genre",
                "id": "5156ed2be9e23d6625cc094b",
                "parent": null,
                "name": "Country"
            },
            "name": "Americana"
        }
    ],
    "advertising": {
        "interstitial_ad": false,
        "display_ad": false
    },
    "name": "Test",
    "dasherized_name": "playlist-in-progress-trevorsenior",
    "global_station": null,
    "creator_name": "trevorsenior",
    "url": "http://songza.com/listen/playlist-in-progress-trevorsenior/",
    "song_count": 0,
    "cover_url": "http://d2t03vq6udg69j.cloudfront.net/api/1/station/1766718/image",
    "featured_artists": [],
    "creator_id": 10942882,
    "type": "basic",
    "id": 1766718,
    "description": "",
    "notes": ""
}
```

**response**

```json
{
    "dasherized_name": "test-trevorsenior",
    "status": "UNRELEASED",
    "global_station": null,
    "name": "Test",
    "creator_name": "trevorsenior",
    "url": "http://songza.com/listen/test-trevorsenior/",
    "song_count": 0,
    "cover_url": "http://d2t03vq6udg69j.cloudfront.net/api/1/station/1766718/image",
    "featured_artists": [],
    "creator_id": 10942882,
    "type": "basic",
    "id": 1766718,
    "description": "Test"
}
```

### add song (POST)

Add a song to the station.

```
http://songza.com/api/1/station/<station id>/songs/add
```

**request**

```javascript
// Parameters
song_id=<song id>
```

**response**

```json
{
    "deleted": false,
    "play_first": false,
    "stats": {
        "vote_down_count": 0,
        "vote_up_count": 0,
        "skip_count": 0
    },
    "id": "1766718-4431270",
    "song": {
        "album": "Britney",
        "artist": {
            "image_url": "http://songza.com/api/1/artist/511acdf2e9e23d724deed520/image",
            "id": "511acdf2e9e23d724deed520",
            "name": "Britney Spears"
        },
        "title": "Anticipating",
        "cover_url": "http://images.mndigital.com/albums/027/175/407/a.jpeg",
        "genre": "Pop",
        "pa": false,
        "formats": [
            {
                "available": true,
                "format": "aac"
            },
            {
                "available": true,
                "format": "mp3"
            }
        ],
        "duration": 196,
        "id": 4431270
    }
}
```

### station-song (PUT)

Used for updating songs on an existing station.

Sending a request with `"deleted: true"` will remove the song from the station play list.  May be able to change other settings as well?

```
http://songza.com/api/1/station-song/<station id>-<song id>
http://songza.com/api/1/station-song/1766718-4578344
```

**request**

```json
{
    "deleted": true,
    "play_first": false,
    "stats": {
        "vote_down_count": 0,
        "vote_up_count": 0,
        "skip_count": 0
    },
    "id": "1766718-4578344",
    "song": {
        "album": "Britney",
        "artist": {
            "image_url": "http://songza.com/api/1/artist/511acdf2e9e23d724deed520/image",
            "id": "511acdf2e9e23d724deed520",
            "name": "Britney Spears"
        },
        "title": "Cinderella",
        "cover_url": "http://images.mndigital.com/albums/027/961/515/a.jpeg",
        "genre": "Pop",
        "pa": false,
        "formats": [
            {
                "available": true,
                "format": "aac"
            },
            {
                "available": true,
                "format": "mp3"
            }
        ],
        "duration": 219,
        "id": 4578344
    }
}
```

**response**

```json
{
    "deleted": true,
    "play_first": false,
    "stats": {
        "vote_down_count": 0,
        "vote_up_count": 0,
        "skip_count": 0
    },
    "id": "1766718-4578344",
    "song": {
        "album": "Britney",
        "artist": {
            "image_url": "http://songza.com/api/1/artist/511acdf2e9e23d724deed520/image",
            "id": "511acdf2e9e23d724deed520",
            "name": "Britney Spears"
        },
        "title": "Cinderella",
        "cover_url": "http://images.mndigital.com/albums/027/961/515/a.jpeg",
        "genre": "Pop",
        "pa": false,
        "formats": [
            {
                "available": true,
                "format": "aac"
            },
            {
                "available": true,
                "format": "mp3"
            }
        ],
        "duration": 219,
        "id": 4578344
    }
}
```

### Release & Unrelease (POST)

Make your play list public so it is visible to others on the internet.

```
http://songza.com/api/1/station/<station id>/release
```

**request**

```javascript
// Parameters
released=/(0|1)/
```

Where 1 is released, and 0 is unreleased ("true"/"fasle" should work as well).

**response**

```json
{"message": "", "success": true}
```

Note, requires at least 8 artists and 20 songs, else you will get the following responses:

```json
{"message": "must have at least 8 artists (has 7)", "success": false}
{"message": "must have at least 20 songs (has 19)", "success": false}
```

### song list (GET)

Get a list of songs that a station has.

NOTE: You can only list songs on stations that you have created.

```
http://songza.com/api/1/station/<your station id>/songs
```

### stats (GET)

Get stats (plays, upvotes, etc) for a station.

NOTE: you can only list stats of stations that you have created.

```
http://songza.com/api/1/station/<station id>/stats?start_date=2014-5-5&end_date=2014-5-8
```

**request**

```javascript
// Parameters
start_date="2014-5-5"
end_date="2014-5-8"
```






## Artists

### details (GET)

```
http://songza.com/api/1/artist/<artist id>
http://songza.com/api/1/artist/511ace80e9e23d724def297e
```

**response**

```json
{
	"image_url": "http://songza.com/api/1/artist/511ace80e9e23d724def297e/image",
	"id": "511ace80e9e23d724def297e",
	"name": "Ulrich Schnauss"
}
```





## User

### profile (GET)

Get information about a user.

```
http://songza.com/api/1/user/<user id>
```

```json
{
    "about": "",
    "admin_sites": [

    ],
    "black_planet_id": null,
    "display_name": "<removed>",
    "email": "",
    "facebook_id": null,
    "id": 1,
    "image_default": true,
    "image_url": "http://songza.com/api/1/static/images/profiles/default-large.png",
    "images": {
        "large": "http://songza.com/api/1/static/images/profiles/default-large.png",
        "medium": "http://songza.com/api/1/static/images/profiles/default-large.png",
        "small": "http://songza.com/api/1/static/images/profiles/default-large.png",
        "square": "http://songza.com/api/1/static/images/profiles/default-large.png"
    },
    "is_admin": false,
    "location": "",
    "site": "songza",
    "username": "<removed>",
    "website": ""
}
```

### stations (GET)

Get stations that a user has listened to.

```
http://songza.com/api/1/user/<user id>/stations?limit=<limit>&recent=1
```

**request**

```javascript
// Query parameters
limit=<int>
recent=/(0|1)/
```

**response**

```json
{
    "recent": {
        "count": 38,
        "stations": [
            {
                "cover_url": "http://d2t03vq6udg69j.cloudfront.net/api/1/station/1396145/image",
                "creator_id": 1000000,
                "creator_name": "Songza",
                "dasherized_name": "pop-wake-up-call-songza",
                "description": "Start your morning right with these upbeat contemporary pop hits. Perfect for getting the day started on the right foot.",
                "featured_artists": [
                    {
                        "name": "Maroon 5"
                    },
                    {
                        "name": "Jason Mraz"
                    },
                    {
                        "name": "Colbie Caillat"
                    },
                    {
                        "name": "Katy Perry"
                    },
                    {
                        "name": "Phillip Phillips"
                    }
                ],
                "global_station": null,
                "id": 1396145,
                "name": "Pop Wake-Up Call",
                "song_count": 83,
                "status": "NORMAL",
                "type": "basic",
                "url": "http://songza.com/listen/pop-wake-up-call-songza/"
            }
        ]
    }
}
```





## Situation

### targeted (GET)

**request**

```javascript
// Query parameters
current_date="2014-05-09T12:23:14+04:00" // current date in this format
day=/[1-7]/ // day of week
period=<int; 2> // not sure of it's effect
site="songza" // ??
optimizer="defualt" // ??
max_situations=<int; 5> // the number of situations to get back
max_stations=<int; 3> // max number of stations per situation
style="flat-220" // style related stuff, image sizes, etc.
```

```
http://songza.com/api/1/situation/targeted?current_date=2014-05-09T12%3A23%3A14%2B04%3A00&day=5&period=2&device=web&site=songza&optimizer=default&max_situations=1&max_stations=3&style=flat-220
```

```json
[
    {
        "advertising": {
            "display_ad": true,
            "interstitial_ad": true
        },
        "icon": "http://d2t03vq6udg69j.cloudfront.net/api/1/situation/id/5148d598bf0d693e59082743/image?d=1392408573&size=220",
        "id": "5148d598bf0d693e59082743",
        "image_url": "http://songza.com/api/1/situation/id/5148d598bf0d693e59082743/image",
        "selected_message": "We’ll play you some energetic music. Just pick a genre.",
        "situations": [
            {
                "icon": "",
                "id": "5148d598bf0d693e59082741",
                "selected_message": "Select a playlist of upbeat, happy, and absurdly fun music.",
                "situations": [],
                "station_ids": [
                    1382851,
                    1398070,
                    1401158
                ],
                "title": "Upbeat, Happy, & Absurdly Fun"
            }
        ],
        "station_ids": [],
        "title": "Boosting Your Energy "
    }
]
```





## Tags

### tags (GET)

Get a list of tags.

```
http://songza.com/api/1/tags
```

## Gallery

## tag (GET)

For supported tags that may not be listed here, view the tags endpoint

```
http://songza.com/api/1/gallery/tag/moods
http://songza.com/api/1/gallery/tag/decades
http://songza.com/api/1/gallery/tag/genres
http://songza.com/api/1/gallery/tag/activities
```

**response (mood)**

```json
[
    {
        "just_for_you_eligible": false,
        "name": "Aggressive",
        "tags": [
            {
                "site": "songza",
                "featured": true,
                "name": "Moods",
                "slug": "moods",
                "id": "moods"
            }
        ],
        "site": "songza",
        "id": "_curated-aggressive",
        "station_ids": [
            1733339,
            1733880,
            // ...
        ],
        "keywords": "aggressive, agro, macho, intense, fast",
        "slug": "aggressive"
    },
    {
        "just_for_you_eligible": false,
        "name": "Angsty",
        "tags": [
            {
                "site": "songza",
                "featured": true,
                "name": "Moods",
                "slug": "moods",
                "id": "moods"
            }
        ],
        "site": "songza",
        "id": "_curated-angsty",
        "station_ids": [
            1730553,
            1479723,
            // ...
        ],
        "keywords": "",
        "slug": "angsty"
    },
    // ...
]
```





## Collection

"Stars" / "Favorites" fall into collections. They are groups of stations that seem to be defined by the user. "Coding" is a collection that I made on the old interface - I can't seem to find out how to change it on the new interface however.

### user collections (GET)

```
http://songza.com/api/1/collection/user/<user id>
```

**response**

```json
[
    {
        "user_id": 10942882,
        "station_ids": [],
        "id": 6584230,
        "title": "favorites"
    },
    {
        "user_id": 10942882,
        "station_ids": [
            1399111,
            1727031,
            1713666
        ],
        "id": 5852193,
        "title": "Coding"
    }
]
```

### add station (POST)

Add a station to a collection.

```
http://songza.com/api/1/collection/<collection id>/add-station
```

**request**

```javascript
station=<station id>
```

**response**

```json
{}
```

### remove station (POST)

Remove a station from a collection.

```
http://songza.com/api/1/collection/<collection id>/remove-station
```

**request parameters**

```javascript
station=<station id>
```

**response**

```
// There does not seem to be any response data....
```
