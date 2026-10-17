# Build plan: context-reactive ads that can't lie

Hackathon: AMD Developer Hackathon Act III, track "Create a New Kind of Experience". The build closes on **18 October**. The friend should check the exact closing hour on lablab.

## The concept (Gemini's vision merged with ours)

A brand supplies three things once: a **real product photo** cut out as a transparent PNG, a **one-page brand book**, and a list of **approved claims**. When someone views the ad, the engine reads their context and builds a finished micro-commercial for them. The context is a persona, a city, the local time and live weather, and the device.

- **Scene:** the background is generated per context (rainy neon desk at 11pm, sunny beach ledge at 7am). The product photo is composited on top, never regenerated, so the logo and packaging physically can't warp. This is stronger than ControlNet and much simpler to build.
- **Copy and voice-over:** Gemma writes the headline, body text and voice-over script as strict JSON, and every claim has to cite an approved claim ID.
- **Music:** the director model picks a mood, which maps to a small library of royalty-free loops. We don't generate music, which is cheaper and safer.
- **Quality gate:** code rules (banned words, required legal line, claim IDs that exist, length) plus a Gemma judge (tone, invented claims) approve or reject each ad. Rejected copy is regenerated once. The rejection log shows on screen, which is the demo moment.
- **Cost meter:** shows tokens and euros per ad. Background plates are cached per weather × time-of-day × persona bucket, so the cost per view is mostly text and voice.

**The demo:** split screen. A Gen-Z gamer in Milan at 11pm in the rain on one side, a runner in Rome at 7am in the heat on the other. It's the same can, with a different scene, copy, voice and music. Then a third run where the model tries "clinically proven to boost focus" and the gate blocks it live.

**Who pays:** D2C brands and retail media networks. They pay per thousand views plus a subscription, because contextual creative performs better than static banners and the gate removes legal-review cost.

## AMD and Gemma usage

- All language and vision calls go to the AMD Token Factory (friend's account). We use Gemma if it's listed there; otherwise the best open model on the list, with the reason stated in the pitch.
- Background images and voice should also run on AMD if the Token Factory offers image or speech models. If it doesn't, we pre-generate the plates and say so honestly.

## Who does what

**Friend (AMD account plus Gemini)**
1. **Now:** send the Token Factory **base URL and model list**, without the key. We need text, vision, image and speech model names. Is Gemma there?
2. Make the brand: a name, a one-page brand book, about 8 approved claims, banned words and a legal line. Gemini can draft these; a human picks the final set.
3. Photograph a real can or bottle with a plain label and cut it out to a transparent PNG.
4. Collect 4 to 6 royalty-free music loops (lo-fi, upbeat, calm, epic).
5. Generate or collect the background plates for the demo contexts.
6. Tomorrow: demo video, slides, cover image and the lablab submission form.

**Joseph plus Claude**
1. **Now:** connect GitHub so Claude can create and push the repo: https://claude.ai/connect-github
2. Claude builds the app: a Python backend (context to director to copywriter to gate to cost) and a web page (split-screen player, compositor, voice, gate log, cost meter).
3. Joseph runs it with the API key on his machine and tests it with the friend's assets.

## Timeline

- **Tonight:** text pipeline working end to end on AMD, plus a first split-screen page.
- **Tomorrow morning:** visuals, voice, music and polish. **Feature freeze at midday.**
- **Tomorrow afternoon:** record the video, write the slides and submit early.

## Rules

- **Never paste the API key in chat or commit it.** The app reads it from an environment variable (`AMD_API_KEY`).
- If time runs short, cut images and voice in that order. The gate and the split-screen copy are the core.
