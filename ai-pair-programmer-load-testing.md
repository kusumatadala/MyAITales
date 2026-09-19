# When Your AI Pair Programmer Becomes Your Load Testing Team

Here's a confession: I improved a project's performance by 6x this week, and I didn't touch a single "official" performance testing tool to prove it.

## The problem: I needed proof, not just a hunch

I'd been refactoring — decoupling some data structures that had gotten tangled together over time. I believed it was faster. But "I think it's faster" doesn't hold up in a standup, and it definitely doesn't hold up in a design review. I needed numbers: a before-snapshot and an after-snapshot, benchmarked against each other.

The "correct" way to do this at most companies involves enterprise tooling — in my case, BlazeMeter. Except getting access meant tickets, approvals, and installs I didn't have time to wait on. What I did have was Claude, VS Code, two deployed environments running my two code snapshots, and an afternoon.

## Attempt one: brute-force it myself

My first instinct was low-tech: fire up Postman, hit each API a bunch of times manually, average the response times, call it a day. Reasonable in theory. Excruciating in practice — nobody wants to be a human for-loop.

## Attempt two: delegate it

So I handed the tedium to Claude. What started as "just run these calls for me" turned into something bigger: Claude built out a full API performance testing lab — generating test scripts for every endpoint I cared about.

Then I got ambitious. Instead of running everything through chat, I asked for a UI — something I could click into, drop a JWT token and base URL, and hit "run" like an actual tool instead of a script I babysat.

## The wall: a JWT token that wouldn't cooperate

And it worked — eventually. The first version didn't even run: syntax errors everywhere. Second pass, it ran clean. Progress. But then it hit a wall that took what felt like a hundred iterations to clear: the UI couldn't reliably decode the JWT token into the test scripts. Same failure, over and over, no matter how many times we tweaked it.

That was the real lesson of the week: a polished UI is great, but it's brittle when something context-dependent like auth is involved. So I abandoned the UI and went back to plain chat-based iteration — where Claude could actually reason about why the token wasn't parsing instead of just executing a fixed script.

## The payoff

Back in chat, after a genuinely absurd number of runs (a thousand? might be exaggerating, but it felt like it), I had two clean performance snapshots to compare, each with solid metrics behind it.

The result: **the refactored system is 6x faster than before.**

Not "I think," not "it feels snappier" — an actual measured, reproducible number, generated without ever getting BlazeMeter access.

## The bigger takeaway

What struck me wasn't just the speedup — it was how the shape of the collaboration had to change. The UI felt like the "grown-up" solution, but the flexible, conversational chat interface was actually better at debugging a genuinely tricky problem. Sometimes the fancier tool isn't the right tool for getting unstuck.

That said, the UI isn't dead — it's just parked. Clicking a button beats burning tokens every time you want to re-run a test suite, so fixing that JWT decoding issue and getting the UI working properly is still on my list. Chat was the right tool for debugging; a button is still the right tool for repeating.

So — how are you using AI in your own workflow? Are you building tools with it, or leaning on the conversation itself to get unstuck? I'd love to hear what's worked (and what's quietly failed) for you.
