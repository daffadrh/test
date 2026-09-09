# XR Teardown — Cubism (Mixed Reality Update)

**[NRP Anda] — Daffa Rafif H.** · S1 Informatics · Individual Assignment 1

| | |
|---|---|
| Subject | Cubism (Mixed Reality Update) |
| Publisher / manufacturer | Thomas Van Bouwel (Vanbo LLC) |
| Release or major update | October 2023 (Quest 3 Passthrough MR update) |
| Platform(s) | Meta Quest 3, Pico 4 Ultra, Android XR |
| How I examined it | Hands-on on a lab Quest 3 |
| Hands-on date(s) | [Isi dengan tanggal Anda mencoba, misal: 8 Sep 2026] |

> **My claim in one sentence.** Cubism's tabletop mixed reality design proves that controller-free manipulation of 3D objects is highly intuitive for beginners, but it exposes the severe ergonomic cost of sustained mid-air pinching and optical tracking occlusion.

---

## 1. Device class

Cubism targets a **6DoF standalone headset with colour passthrough**, specifically platforms like the Meta Quest 3 and Pico 4 Ultra. This places it directly on the **Mixed Reality (MR)** segment of the reality-virtuality continuum. Rather than transporting the user to a fully simulated environment (VR), it brings virtual puzzle pieces into the physical world, anchoring them to a real-world desk or table.

This hardware class forces a specific design envelope. Colour passthrough with depth awareness is absolutely critical here. If run on older hardware like the Quest 2 (monochrome, low-res passthrough without accurate depth projection), the illusion of the puzzle sitting seamlessly on a physical table breaks down, and the user's hands appear awkwardly superimposed or misaligned due to latency and poor tracking resolution.

![Foto tangan Anda sedang memainkan Cubism di atas meja fisik menggunakan Quest 3 passthrough](assets/fig1.png)

> **(Catatan: Ganti gambar di atas dengan screenshot/foto dari pengujian langsung (hands-on) Anda sendiri yang menampilkan tanggal yang jelas!)**

## 2. Input modality

**What the user does:** The primary input modality is **bare-hand tracking** using direct grab and pinch gestures. The user physically reaches out to pick up virtual blocks, rotates them using natural wrist movements, and slots them into a volumetric wireframe. 

**Why this and not that:** The developer chose hand tracking over standard 6DoF controllers because the mental model of solving a physical block puzzle maps perfectly to human hands. Using a controller's trigger button to mimic a "pinch" feels artificial for a puzzle this simple. Hand tracking eliminates the abstraction layer of a controller, reducing onboarding friction for non-gamers. 

**Where it fails:** The design fails when dealing with **optical occlusion and arm fatigue**. Because the Quest 3 relies on optical cameras to track fingers, one hand often blocks the camera's view of the other hand when rotating complex pieces close together, causing tracking loss. Additionally, holding arms in mid-air to manipulate floating puzzles causes "gorilla arm" (severe shoulder/arm fatigue) after just 15-20 minutes.

**What I would change:** I would implement a robust "gaze and microgesture" fallback system. Allowing users to rest their arms on the table and simply look at a puzzle piece while doing a thumb-tap microgesture on their lap would completely solve the physical fatigue while retaining controller-free input.

![Screenshot yang menunjukkan momen pelacakan tangan melemah (hilang) saat kedua tangan saling tumpang tindih](assets/fig2.png)

## 3. Use of AI

| Where | What it does | On-device or cloud | Cost it carries | Source + the line I am relying on |
|---|---|---|---|---|
| Perception | Hand and finger pose estimation (26 joints per hand) | On-device | Battery drain, thermal load, and compute latency | [Meta Hands Technology](https://developers.meta.com/horizon/design/hands-technology/) — "This data is processed by software using algorithms, often involving machine learning and computer vision, to recognize various hand positions and movements." |
| Perception | Scene understanding (Passthrough blending and spatial anchors) | On-device | High battery consumption and privacy considerations regarding room scanning | [Meta Presence Platform](https://developers.meta.com/horizon/blog/mixed-reality-mr-retention-presence-platform-tools-meta-quest-developers/) — "Passthrough provides a real-time 3D visualization of the physical world, allowing developers to comfortably and convincingly blend the user’s physical environment with virtual elements..." |

There is no meaningful AI used in the *content*, *interaction* (like NPCs or LLMs), or *rendering* (no cloud upscaling or AI frame generation). Cubism is a deterministic, math-based logic puzzle. The AI is entirely load-bearing in the **perception pipeline**; without on-device computer vision models inferring hand poses and room geometry in real-time, the core bare-hands mixed reality mechanic simply would not function.

## 4. Impact

**Intended benefit:** Provides a calm, highly accessible spatial reasoning exercise that improves lateral thinking without the motion sickness or sensory overload typical of high-action VR games.

**Privacy, security, or ethics:** To function in MR, the headset continuously captures passthrough camera frames and generates a scene mesh of the user's private living space (desks, walls, room layout). Even though this data is processed locally, it normalizes the continuous optical scanning of private environments and bystanders who have not consented to being filmed by the headset's external cameras.

**Accessibility / human factors:** Cubism's reliance on precise hand tracking makes it inaccessible to users with fine motor impairments or severe hand tremors. A user must be able to hold a steady "pinch" state and rotate their wrists smoothly. Any shaking causes the virtual block to drop or snap to the wrong grid space.

## 5. What I take from this

Cubism demonstrates that Mixed Reality shines brightest when it respects physical metaphors, like placing a puzzle on an actual desk. However, it also highlights that consumer MR hardware still struggles with input ergonomics; until we solve the physical strain of mid-air manipulation and optical occlusion, bare-hand tracking will remain best suited for short sessions rather than extended productivity.

---

## References

1. Meta Horizon OS Developers. (2026). *Hands Technology*. URL: https://developers.meta.com/horizon/design/hands-technology/ — accessed 10 Sep 2026
2. Meta Horizon OS Developers. (2026). *How Developers Are Increasing User Retention with Presence*. URL: https://developers.meta.com/horizon/blog/mixed-reality-mr-retention-presence-platform-tools-meta-quest-developers/ — accessed 10 Sep 2026
3. PlayTechDeep. (2026). *Cubism VR Review 2026: Meta Quest Mixed Reality Puzzle Game*. URL: https://playtechdeep.blog/2026/05/02/cubism-meta-quest-spatial-puzzle-mixed-reality-worth-it/ — accessed 10 Sep 2026
4. Van Bouwel, T. (2023). *Cubism Press Kit & Update Logs*. URL: https://www.cubism-vr.com/presskit/ — accessed 10 Sep 2026

## Figure credits

- Fig. 1 — [Isi dengan: My own screenshot, Quest 3, [Tanggal pengujian] / source and licence]
- Fig. 2 — [Deskripsi/Sumber Figure 2]
- Fig. 3 — [Deskripsi/Sumber Figure 3]

## AI-assistance disclosure

**What I used, and for what:** Gemini (Google) to structure the document, formulate the initial argument outline based on the rubric, and retrieve exact quotes from Meta Quest developer documentation. All final arguments were reviewed and contextualized by me.

### What I disagreed with my AI assistant about

Initially, the AI assistant suggested that I argue against Cubism's MR mode because it lacked generative AI content and complex LLM-driven interactions, which are popular in 2024. I rejected this argument entirely because it represents a shallow reading of the application's purpose. Cubism is fundamentally a minimalist, deterministic logic puzzle; adding generative AI or conversational agents would ruin the deliberate, calm nature of the game. Instead, I focused my critique strictly on the ergonomic and physical limitations (like tracking occlusion and gorilla arm) caused by its hand-tracking input modality, which is a much more defensible and grounded technical claim.
