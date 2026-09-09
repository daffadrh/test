# XR Teardown — [Name of the application or device]

**[Your NRP] — [Your full name]** · [S1 Informatics / S1 AI Engineering] · Individual Assignment 1

|                          |                                                                    |
| ------------------------ | ------------------------------------------------------------------ |
| Subject                  | [Application or device name]                                       |
| Publisher / manufacturer | [Who ships it]                                                     |
| Release or major update  | [Month Year — must be 2023 or later]                               |
| Platform(s)              | [e.g. Meta Quest 3, Pico 4 Ultra, visionOS, WebXR, Android XR]     |
| How I examined it        | [Hands-on on a lab Quest 3 / documentation and spec sheets / both] |
| Hands-on date(s)         | [when you actually put the headset on, or "documentation only"]    |

> **My claim in one sentence.** [State the argument this teardown defends. Not a summary — a claim someone could disagree with. This is also how you open your 3-minute presentation.]

---

## 1. Device class

[Which hardware class does it target? Name it precisely — degrees of freedom, standalone or tethered, opaque or passthrough, colour or monochrome, controllers shipped or not.]

[Where does it sit on the reality–virtuality continuum, and why there rather than one step either side?]

[What does that class make possible, and what does it rule out? If it depends on a capability our lab hardware lacks — eye tracking, depth-aware colour passthrough below Quest 3 / Pico 4 Ultra — say so and say what breaks without it.]

![Caption that makes a point, not "screenshot of the app"](assets/fig1.png)

> **One of your three figures must be your own** — a photo or capture of your own hands-on session on a lab headset, or your own measurement, with a visible date. Mark it clearly in the figure credits below.

## 2. Input modality

**What the user does:** [The modalities actually used — controllers, hand tracking, gaze-and-pinch, voice, gesture, dwell, physical props, room-scale locomotion.]

**Why this and not that:** [Argue the choice against a named alternative the product did not take. What did it buy, and what did it give up?]

**Where it fails:** [At least one concrete failure mode — precision, arm fatigue, discoverability, occlusion, lighting, standing vs seated, small rooms, accessibility.]

**What I would change:** [One substantiated remedy. Say why it would work, not just that it would be nicer.]

![Caption](assets/fig2.png)

## 3. Use of AI

[Go through the pipeline and report only what you can evidence. Delete the rows you find nothing for — an honest short table beats a padded one.]

| Where                | What it does                                                    | On-device or cloud | Cost it carries                                   | Source + the line I am relying on |
| -------------------- | --------------------------------------------------------------- | ------------------ | ------------------------------------------------- | --------------------------------- |
| Perception           | [hand/body pose, scene mesh, relocalisation]                    |                    | [latency / battery / thermal / network / privacy] | [link] — "[quote the sentence]"   |
| Content              | [text- or image-to-3D, upscaling, texture synthesis]            |                    |                                                   | [link] — "[quote]"                |
| Interaction          | [STT, TTS, LLM agent, translation]                              |                    |                                                   | [link] — "[quote]"                |
| Rendering & delivery | [foveation, frame interpolation, super-resolution, split/cloud] |                    |                                                   | [link] — "[quote]"                |

> Every row needs the **quoted sentence**, not just the link. A claim with a bare URL behind it is an unsupported claim.

[Then the paragraph that actually earns the marks: what is the AI *for* here — is it load-bearing, or is it decoration? If you concluded there is no meaningful AI, this is where you show where you looked and why absence is plausible.]

## 4. Impact

**Intended benefit:** [Concrete enough that someone could check whether it is true.]

**Privacy, security, or ethics:** [Tie this to sensor data the device really captures — hand and body pose, room scans and scene meshes, passthrough camera frames, voice. What is collected, where does it go, and who is exposed — including bystanders who never consented.]

**Accessibility / human factors:** [Who cannot use this, and why? Height, one-handed use, vision, motion sensitivity, cybersickness, language, cost.]

## 5. What I take from this

[Two or three sentences. What does this teardown tell you about where XR design is heading — or where it is stuck? Do not summarise the sections above.]

---

## References

1. [Primary source — developer documentation, specification, technical paper, or your own measurement. At least one of these is required.]
2. [Author/Publisher. (Year). *Title*. URL — accessed DD Mon 2026]
3. [ ]
4. [ ]

## Figure credits

- Fig. 1 — [my own screenshot, Quest 3, 8 Sep 2026 / source and licence]
- Fig. 2 — [ ]
- Fig. 3 — [ ]

## AI-assistance disclosure

**What I used, and for what.** [Name the tools and the tasks — e.g. "Claude to tighten the prose in §2; all sources located and read by me." If you used none, write "None."]

### What I disagreed with my AI assistant about

[One paragraph, and it is marked. Where did the tool tell you something you decided was wrong, shallow, or unsupported — and what did you do instead? Be specific: name the claim, name your reason. If you used no tools, write instead about a source you decided not to trust, and why.]
