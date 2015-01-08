---
layout: post
title: TrainerRed & Recomm - projects using Snoocore
date: 2014-10-15
categories: github reddit api snoocore netsec
---

Others are slowly starting to discover the reddit API wrapper [Snoocore](https://github.com/trevorsenior/snoocore). I haven't publicly announced it anywhere yet (short of posting it on [this list](https://github.com/reddit/reddit/wiki/API-Wrappers) and well, on this site) because it still feels like it could use a little more work. It would also be nice to announce the library with a useful project of my own that uses Snoocore however it seems that I have been beaten.

## TrainerRed

The first release of a project using Snoocore that I know of is [TrainerRed](https://github.com/damianb/trainerred) made by [damianb](https://github.com/damianb) for the subreddit [/r/netsec](http://www.reddit.com/r/netsec).

It should be noted that damianb has been invaluable on GitHub opening issues & pull requests on Snoocore helping it get to where it is today. Throttling requests, the new "path syntax" of `reddit('/api/v1/me')` vs the "dot syntax" `reddit.api.v1.me`, a way of calling undocumented endpoints with `reddit.raw`, and the [listings feature](http://tsenior.com/snoocore/listings.html) of Snoocore were all suggested and implemented because of the discussions we had.

## Recomm

According to /u/xiongchiamiov "[Embeddable comments are] something that's fairly high up on our list" <sup>[1](http://www.reddit.com/r/ideasfortheadmins/comments/2iqk4h/please_make_reddit_posts_comments_easily/cl4spx4)</sup> mentioned in [this post](http://www.reddit.com/r/ideasfortheadmins/comments/2iqk4h/please_make_reddit_posts_comments_easily/) in [/r/ideasfortheadmins](http://www.reddit.com/r/ideasfortheadmins). There seems to be at least some support for embedded reddit comments which my project [Recomm](https://github.com/trevorsenior/recomm) will solve, at least for the comment section part.

I've been working on this project for around 2 months now, and it's starting to take shape and has been a great test of my library Snoocore because it uses both the browser and Node.js versions of it. I've been learning a lot about [React.js](http://facebook.github.io/react/) and quirks of the Reddit API as I go along. There are a few hurtles to get over such as the limit on [/api/morechildren](http://www.reddit.com/dev/api#POST_api_morechildren) and defining the details on how to embed the comments into an actual webpage with as little friction as possible (avoiding account registrations like other platforms) but these will be figured out over time.



