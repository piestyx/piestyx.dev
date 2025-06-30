---
title: Website Updated
url: /blog/changelog-01
layout: single
tags:
  - "#blog"
  - "#changelog"
date: 2025-06-30T08:00:00
summary: >
  Just a quick little update on the changes made to the website in the most recent push…
---
## I finally did it

Not gonna lie, this website stuff was a whole world of "woah…" when I first looked into it. The process is surprisingly clean using [Hugo](https://gohugo.io/) and [GitHub](https://github.com/). It lets me test everything locally on a home instance before pushing changes live so once a commit goes through, it stays put unless I keep finding typos or want to update something.

I’ve spent the last few days properly digging into Hugo and I’m starting to feel a lot more comfortable with it. With that, I’ve made some pretty "yuge" changes.

![tyson-yuge](/images/tyson-yuge.gif)

## Changelog

1. Reverted to using global `:root` variables in the CSS for easier theme management
2. Simplified shortcode use by switching back to `_default` layout templates and page-specific overrides
3. Light and dark mode now properly toggle (no more dark mode vs. even darker mode)
4. Updated the *Packages* section to link to the GitHub repo for the game-mods
5. Added a tag-based filter to the Blog page for easier navigation
6. ECHO content updated to include initial project details and introduce Orielle
7. New page `Playground` added:
    - Provides an interactive front-end to test LLM prompts
    - Hooks into a local API that routes to self-hosted models (e.g. DeepSeek-Coder and Qwen3)
    - No account or login required—completely local and private
    - Sends structured prompt templates to a running `llama-server` backend
    - Qwen3 mode highlights structured reasoning in a more deliberate “thinking” style
    - The backend supports dynamic model switching based on user selection. No reloads needed...But also not working yet
8. Blog backlog updated to page

## Future

I plan to make some small iterative tweaks here and there, but for now I’m pretty happy with how it all feels. Most updates going forward will focus on deeper integration with the Playground and expanding the Blog.

If you're curious about prompting and want to see how local LLMs perform, head over to the <a href="/playground/">Playground</a> and try it out.

piestyx