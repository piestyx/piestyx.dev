---
title: Updates
url: /blog/changelog-02
layout: single
tags:
  - "#blog"
  - "#changelog"
date: 2025-08-14
summary: >
  It's been some time again so here is another update post of what's been going on…
---
## A Quiet Month, A Lot Moved

I didn’t post much in the past few weeks and not because nothing was happening, quite the opposite, but because I was in a bit of a recursive loop. One step forward on HelixNet, then a pause, then a sidestep into infrastructure just to keep momentum up.

It’s all movement, even when it doesn’t feel like progress.

## Changelog

1. **HelixNet production-ready version built**
   - HNX-M is now fully modular, testable, and comparison-ready.
   - Benchmarks against Mamba and Transformer models are running from an initial custom test environment.
   - Broader evaluation now progressing at pace using `minigrid`, `minihack`, and `procgen`.
   - Initial patent filed. Not a bad sentence to finally write.

2. **Planned to resume work on Orielle**
   - The intent was to jump straight back into integrating the final memory modules and finish the stream loop.
   - But right as I did, the GPT-5 update dropped which changed a lot.
   - You may have seen the issues people have raised about their workflows being disrupted……yeah, that happened.

3. **Built a new desktop interface instead**
   - A unified UI that allows for both local and cloud inference.
   - Supports xAI, OpenAI, and Anthropic APIs.
   - The goal? Retain access to older model behavior especially around reasoning chains.
   - Now live on GitHub: [piestyx/gpt_interface](https://github.com/piestyx/gpt_interface) to try it out if you wish.

4. **Orielle now back in focus**
   - Stream control loop is ready.
   - Reasoning + narration modules are lined up.
   - No more excuses. Time to finish the last mile.

5. **AI Home Assistant**
   - Almost forgot — I also uploaded a stripped-back version of Orielle to GitHub:  
     [piestyx/ai-home-assistant](https://github.com/piestyx/ai-home-assistant)
   - It’s a lightweight local inference implementation using `llama.cpp`.
   - Based on Orielle’s codebase but with far fewer modules.
   - Optional TTS using only [edge-tts](https://github.com/rany2/edge-tts)

## A Note on Vibes (Internal, Not Interface)

There’s been a low-level hum of uncertainty this whole time. Not really burnout, not quite fear, more a creeping sense of losing grip on perceived opportunity. It’s felt like wading through molasses at times, but I’ve still been working those quads and getting through it.

The hard bits expose the weak points, and that’s not a bad thing. When you’re learning through unconventional routes, it’s easy to skip fundamentals…but they’re fundamental for a reason. I’ve been trying to reframe the difficulty not as insecurity, but as **priority**: if something challenges me, it’s probably where the reinforcement is most needed.

Now, with fewer distractions, I can hopefully finish off Orielle.

piestyx