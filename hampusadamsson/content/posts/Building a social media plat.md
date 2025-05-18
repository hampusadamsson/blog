---
title: Building a social media management platform
date:
---

### How I Built a Social Media Management Platform in One Week

![](https://ci3.googleusercontent.com/meips/ADKq_NYWG0uvZ-Xchb6Av-LE-Zw0T5186xTvT3gq4EimE6gWM-8iZbLiQ5ggZWydV3JDJ0W7neCg5D8HUzE2199NJRuZ3mz2xaNLdQoVuKL13Oq9H48QSouX5Rcjkd4=s0-d-e1-ft#https://cdn-images-1.medium.com/max/1000/1*AzXlMNF70rJpnSczVsLcXw.png)Social Badger — my one week social media management platform

Backtrack a few months, to a time when I had just finished an app, a stock brokerage called Playtrader (see my other posts). I was quite proud with the result, but faced one big problem, it did not draw any traffic. It turns out that generating traffic is way more difficult than creating an app.

“Marketing can’t be that hard, I’ll make a marketing app”

Challenge accepted.

_Edit: This post is actually written using the app._

### How I Got Started

It is tempting to just start coding, but some planing was warranted. Especially given the time frame.

I turned to ChatGPT and asked for a roadmap, and it supplied me with a clear plan — day one was for setting up backend and frontend, day two for user management and UI, day three to integrate Twitter, and day four to get AI running. The schedule was ambitious, but I felt like giving it a shot.

I looked at some competition and what they were doing. [Hootsuite](https://www.hootsuite.com/), [Buffer](https://buffer.com/), and S[proutsocial](https://sproutsocial.com/) were the highest ranking hits on Google, and they gave me a good grasp of what was _must have, nice to have,_ and _out of scope_.

![](https://ci3.googleusercontent.com/meips/ADKq_NaMBDKShDh9JBRvumhNP2jfSAspWn3oOWOVitNj0EFpg1YO60DMbTbLnDA0eUleWHZss-zmmXsnVyRC5_wmFo6zrLBvDK_QPoOGNcF6Tah8m50PWcHylH8O1Lk=s0-d-e1-ft#https://cdn-images-1.medium.com/max/1000/1*5ChHpt5kxSsiU3LvM5YQpQ.png)Creating content and keeping track of schedules

It is always nice to have something to aim for, and I knew roughly how i wanted the content overview to look like, followed by the content creation prompt. To be honest, I was mostly aiming for “a neat modal”, but you know what I mean.

### Tech Stack: Go and Svelte

I used Go for the backend, specifically PocketBase, a lightweight alternative to Firebase. It handles collection management, user management, and custom code. Plus, it comes pre-configured with SQLite. Simple, efficient, and a great fit for a one-week project.

For the frontend, I went with Svelte. I’ve used React and Angular before, but Svelte is leaner and faster for projects like this. I added Flowbite for pre-built UI components and Tailwind for styling. The result? A polished, professional look without spending ages on UI.

Here is the first page I ended up creating, a user management route with login, create account, and forgotten password.

![](https://ci3.googleusercontent.com/meips/ADKq_NaUniBDT_83gHw1u9P8AkIYllM_X-Xi11a296xl7cmK4a5p8nCza20m8C4fYXQrN4uobS9lMm2cqpi4VS3VEwBJyqPc9pJqhNGtnzYmpYp3bvRC1-EvEpXRu0c=s0-d-e1-ft#https://cdn-images-1.medium.com/max/1000/1*t0nZNT0AWUe72gJauOtgxQ.png)User management with Pocketbase, Svelte, Flowbite, and Tailwind

### Basic content management

Can’t have a social media management platform without managing content somehow. And settings. And metadata. And probably a lot of other stuff. So I set about creating a nice DDD domain object, which mostly ended up being me prototyping in Javascript.

![](https://ci3.googleusercontent.com/meips/ADKq_NaA7B9iPcb4i-OZB8wQxL7Gv-pFp0V79D-XdTMI4ldrrO12IMnVwCft-sglKp7WIhtG8fmzUhVu8eF5f3Y2_o0RQgnMAm9BHMaPh-SDnOO6zoD6n047A5ku758=s0-d-e1-ft#https://cdn-images-1.medium.com/max/1000/1*bQOb3ICm4ukF945-mhsJvw.png)Creating content with keywords, schedules, platforms, etc.

### Integrating Twitter, Medium, WordPress, and Mastodon

Most platforms use OAuth2 for integration, which made it easier to add Twitter, Medium, and Mastodon after setting up Twitter first. Medium was a bit of a snowflake, needing a custom token. OAuth2 was tricky at first, especially with the back-and-forth with the token passing. A publicly available endpoint for callbacks is one of those big blockers for a hobby project on a schedule. Luckily, I had a Raspberry Pi with a static IP from my previous project, Playtrader, so that gave me a running start.

![](https://ci3.googleusercontent.com/meips/ADKq_Nbzut8CFc4tWxh9wk_ZtbPJy3xq-t0SgERzxYDZpbXZl9fPBAdcUyAakWEh77YoUoaUv54QEL5H8j74Acbw6vi0cMYVHXU9YJiCGwhNF8tjGGUiA7hdfYc9erc=s0-d-e1-ft#https://cdn-images-1.medium.com/max/1000/1*n9JxMIRbn3L2qVDIvfF21w.png)Twitter, Medium, Wordpress, and Mastodon (Oauth2)

### Adding AI-Powered Content with Gemini

I thought AI integration would be tough, but it wasn’t. Gemini’s Go client and API were easy to set up. I integrated it for content creation, review, and even fully automated campaign scheduling. The app can post unique content on its own.

At first, Gemini repeated itself a lot. So I had it check previous posts and avoid writing anything similar. Problem solved.

![](https://ci3.googleusercontent.com/meips/ADKq_NaU-i2RlftKxe0NMq7nwOeWPM1uPCMb0nBpuytdym-jF4EwQkqaR521T4D6D4B3CWPKZMmgFTfCwNgWig1vS1HbFvmo3uzSrYULcjTXT20VjHKzH0_osT4IhEw=s0-d-e1-ft#https://cdn-images-1.medium.com/max/1000/1*wGnzy6o7Fvg7z5PLYT80Sg.png)

### Simplifying Image Sourcing with Pexel

Turns out that people like images. No images, no readers. Who could have thought?

I considered using AI to generate them but went with Pexel instead. It’s simple and has an easy API, unlike Unsplash, which requires OAuth2 (and I’d had enough of that). Pexel gave me everything I needed to add high-quality images to posts. One week is not a whole lot of time.

![](https://ci3.googleusercontent.com/meips/ADKq_Nbds2pNnDiwIcERx5aS9jYcyvrg0bS1i7KzZiBcSkkxonNB1wBDjLDwMUbd78PQLm3ms5NlNWvp4QgEhPKEg5LpcktdrhCCubiKRrTvY8jqqm67Vlsth_-_50M=s0-d-e1-ft#https://cdn-images-1.medium.com/max/1000/1*590vMi-S4Q_Q10H9_T91fQ.png)Images from Pexel are automatically added based on content

### But what about the Autopilot thing?

Automatic post creation. AI assisted writing. Scheduling. This was nice, but I still wanted more of an … automated solution. An Autopilot. Something that could generate everyting by itself. So I created Campaigns; basically scheduled jobs with predefined instructions not to repeat itself, to follow a prolonged, coherent, thread; sort of like an ongoing marketing campaign.

![](https://ci3.googleusercontent.com/meips/ADKq_NYVGtjluV-oWx5dqPeAkdBpetnofUI8-iZ9pErk3HNS8AMPK119Ec2MU2cf3o7FojWnD_Iss8TndLYFuBHCPYoR5fGEwhezCYACwY_mtKoTnwnJvFy24g8AD0c=s0-d-e1-ft#https://cdn-images-1.medium.com/max/1000/1*NbMxPZl5SFICBkuPnm-VvQ.png)Cron scheduled auto posting with Autopilot

### Lets test it! Turns out it knows Swedish?

I activated the autopilot, created a campaign, and instructed it to tweet “writing tips for aspiring writers” on Twitter/X daily. As you can see below, it managed to get the job done. A rather unexpected feature was the built in multi language support. I honestly did not see that coming.

![](https://ci3.googleusercontent.com/meips/ADKq_NZFVj4Zkq6v4gJ83m3LxZUfN_cgEztGIbOhS5jMzwcs1pEFBHRfquIbivLS8zcvi1JzaKa35J8nICaSLoNMZjMhoKru4Xxm9D_8Uo2coTMwWSlIuA_923jVIwE=s0-d-e1-ft#https://cdn-images-1.medium.com/max/1000/1*1kCTHG-kmVszkZAh9yhhTg.png)Posting on Twitter/X using Social Badger

### Challenges and Lessons Learned

Even building a platform to generate traffic is hard. I might need to build a marketing app for my marketing app. SEO, images, and keywords are still a work in progress.

There is also subtle differences in content cration for each platform. Medium supports markdown and HTML. The others are more into plain text and images. Twitter has the 200 chars requirement. Mastodon has a 500 chars requirement. Wordpress needs a blog ID for the API to work. It is not much, but for each new integration, the “base integration” suffers. The list goes on.

OAuth2 is powerful but time-consuming. It takes public endpoints and a lot of support code. Managing integrations is the core challenge of building a platform like this. It also means you have to keep up with breaking changes (heavy sigh).

Getting AI to work consistently was another hurdle. It felt much like a flaky test. Gemini would sometimes return unusable data, bad format, and the occasional hallucination was annoying. Still, it worked well enough to automate most content creation.

### What’s Next?

Analytics would be a great addition — tracking how posts perform across different platforms on a dashboard. But not all platforms support that. Medium, for instance, doesn’t offer much in the way of analytics.

More integrations could come, like Threads, Instagram, and Facebook. I’m also toying with the idea of automatic interactions, but flooding social media with auto-responses makes me feel uneasy.

That’s where I am — one week, one platform, and a whole lot of possibilities ahead.