---
title: "Doing it with vibes"
url: "/blog/vibes-01"
layout: "single"
tags: ["#blog"]
---
# I'm piestyx, and I'm a vibe-coder

I wasn't too sure how open to be about being a dirty vibe-coder but I think it might have got a bit of a bad rep because of misplaced expectations, let me chuck my story into the ring. 

## From Idea to Install 

It started in March 2025 with a curiosity about what it would take to make an AI home assistant, one that was offline and self-contained and just ever present on my network. That kind of spiraled into a vision of creating an AI entertainer that can narrate and play games with a high potential for rich and engaging lore, like [`Caves of Qud`](https://www.cavesofqud.com/) and [`Dwarf Fortress`](https://www.bay12games.com/dwarves/). In theory this is all stuff that can be done, they're pieces of a jigsaw puzzle and I figured I could just chop off a few knobbly bits to make them fit. Realistically though I have no real experience to even start to put it together, I could start to scaffold out a website...maybe? But like when maths turns into the alphabet, the point languages start turning into animals it gets a bit weird and you start looking at things like Python with wonder at how this must be what aliens use for their UFOs. If it can fly a UFO it can definitely power my AI entertainer. 

So I wrote down a note on my phone about what I wanted this thing to do, I stuck it into `ChatGPT` and it swiftly came back to me with a breakdown of the different parts I would need and then even offered to give it all to me. It was the most surprising moment! To be able to just say "this is what I want" and to have it come back straight away and say "here it is, run this script and it will do everything for you". I could barely sleep. I was a kid at Christmas again. I ran myself downstairs in the morning to get my coffee and set myself up, straightened up the desk and double clicked the script ...

```bash
✅ Install Complete
```

## Simon and Garfunkel's Greatest Hits, Track 5

Hoooooooooly shit. So all I have to do is ask and ye shall receive! It will run and just work! OK we're officially living in the future now. I went to the folder that had been created to start getting to work on understanding what I had just creat ...

![The cupboards were bare](/images/uhoh.png)

Oh.

An unforeseen mishap, I am sure! Maybe it is too complex to have a script run and have it put everything in place for me straight off the bat like that. Let's give it a chance and start looking at what is in there and then do things piece by piece; it's a pretty boring puzzle if you open the box and it's already made for you anyway so this is fine...

## Three ... Months ... Later

I won't bore you with detail of every day over the last 3 months but I can assure you there have been ups and downs, at least twice where I've just said it's not something I can do, but I persisted and adapted to what I was learning. Today I was able to test and confirm a working runtime loop where `Caves of Qud` (by using a mod that I wrote) exports logs to a specified location in a `.txt` file. Those logs are then cleaned, buffered and sent to the LLM as an engineered prompt. This integration provided by [`llama.cpp`](https://github.com/ggml-org/llama.cpp) using a ROCm tailored build (that I also made with `CMake` from their linked repo) provides a response back into the action loop where it is reviewed for "action words" to be mapped against an `action_schema.json` to start injecting the relevant key presses back in to the game. The crazy thing? That's not even the first part of this project I've worked on in these last 3 months, I've done the majority of that within the last couple of weeks.

```bash
[Runtime] 8 events buffered — making decision. 
[Planner] Prompt being sent to model: 

...

Recent activity: 
[SYSTEM] [14:08:01] You identify the bizarre contraption as a fusion pumping station. 
[SYSTEM] [14:08:19] You press the power button on the fusion pumping station. 
[SYSTEM] [14:08:22] A loud buzz is emitted. The unauthorized glyph flashes on the display. 
[SYSTEM] [14:08:28] The way is blocked by some rubble. 
[MOVEMENT] [14:08:31] You pass by a wet small boulder. 
[SYSTEM] [14:08:31] You wade through a pool of salty water. 
[MOVEMENT] [14:08:32] You pass by a small boulder. 
[SYSTEM] [14:08:33] The way is blocked by some shale. 
[STATUS] <user> has 22 / 22 HP (penalty: 0). 
[EFFECT] covered in liquid: wet 
[LOCATION] <user> is currently in salt marsh, surface (Z:10). 

...

[Runtime] Decision: I should take a moment to assess my surroundings and consider my next steps carefully. The fusion pumping station 
I encountered seems to have malfunctioned, and the unauthorized glyph on its display suggests there may be security measures in place. 
I`m also hindered by the rubble blocking my path forward. Given these factors, the most logical and thematic action for me to take next 
would be to: "Carefully inspect the fusion pumping station for any clues or controls that might help me safely interact with it and clear 
the path forward." 

[Runtime] Not enough events yet, waiting...
```

The above block is some of the actual output from today's test. There's contextualising prior events and providing assessment and reasoning for the `glyph` being a security measure; presenting internal monologue for the narration, shows goal orientation. All things that I had dreamed of 3 months' ago were now staring me in the face, it actually works, and it was all done with viiiibes, maaaan. 

Not quite. 

## A Note on Vibes

I said at the start about misplaced expectations, and that would very much be on the user. I didn't really expect to have it all handed to me on a plate with a single script to run that would do it all for me, but I did expect it to be easier than it has been to get to this point. It was absolutely a naivety on my part about the tools that were in front of me and how best to actually use them. Once that barrier is overcome it does start to get a bit easier to bend things more to your will but expect things to not work, expect to see trace back errors and debug logs and to get intimately acquainted with them all, expect something to work perfectly and then break it because you opened a new `ChatGPT` tab and lost context.... 

With all that said though if you have the right mindset for it then it is very likely that you would also succeed in and enjoy creating your "dream thing" whatever that may be. You'll need resilience to keep going but also to accept when something exceeds your current limits; I spent 8 hours during one early day just trying to fight through multiple levels of networking, WSL, Docker, VPN, DHCP to end up on the same [`stack overflow`](https://stackoverflow.com) answer I had seen 4 hours earlier. I thought I understood what "fail fast" meant before then but suddenly it clicked. 

Will vibe-coding replace experienced software developers? Absolutely **not** any time soon. The training data used for all these models isn't 100% perfect data, in fact it's probably made up of 80% unoptimised shitty code and if you train on that then that's what you get out. That's like simple thermodynamics or something. What vibe-coding will allow is for people who might have an idea about something but don't necessarily possess the technical expertise to start to actually put their ideas into something. To know the languages that I have been using would have surely saved me lots of time, but it doesn't necessarily help with abstracting out a problem and being able to reason a solution for it. 

If you’ve been wondering whether vibe-coding might be your path, then maybe walk with me for a bit. You might just surprise yourself too. 

piestyx