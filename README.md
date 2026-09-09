# XR Teardown — Cubism (Mixed Reality Update)

**[NRP Anda] — Daffa Rafif H.** · S1 Informatics · Individual Assignment 1

| | |
|---|---|
| Subject | Cubism (Mixed Reality Update) |
| Publisher / manufacturer | Thomas Van Bouwel (Vanbo LLC) |
| Release or major update | October 2023 (Quest 3 Passthrough MR update) |
| Platform(s) | Meta Quest 3, Pico 4 Ultra, Android XR |
| How I examined it | Documentation and spec sheets only |
| Hands-on date(s) | Documentation only |

> **My claim in one sentence.** Cubism's tabletop mixed reality design proves that controller-free manipulation of 3D objects is highly intuitive for beginners, but analysis of its tracking pipeline exposes the severe ergonomic cost of sustained mid-air pinching and optical tracking occlusion.

---

## 1. Device class

Cubism targets a **6DoF standalone headset with colour passthrough**, specifically platforms like the Meta Quest 3 and Pico 4 Ultra. This places it directly on the **Mixed Reality (MR)** segment of the reality-virtuality continuum. Rather than transporting the user to a fully simulated environment (VR), it brings virtual puzzle pieces into the physical world, anchoring them to a real-world desk or table.

This hardware class forces a specific design envelope. Colour passthrough with depth awareness is absolutely critical here. If run on older hardware like the Quest 2 (monochrome, low-res passthrough without accurate depth projection), the illusion of the puzzle sitting seamlessly on a physical table breaks down, and the user's hands appear awkwardly superimposed or misaligned due to latency and poor tracking resolution as documented in the developer's update logs.

![Diagram beranotasi buatan sendiri yang menjelaskan bagaimana sensor Quest 3 memetakan tangan dan ruang fisik untuk Cubism](assets/fig1.png)

> **(Subject unreachable / Documentation only: This is my own annotated diagram explaining the scene reconstruction and hand-tracking pipeline based on Meta's documentation.)**

## 2. Input modality

**What the user does:** The primary input modality is **bare-hand tracking** using direct grab and pinch gestures. The user reaches out to pick up virtual blocks, rotates them using natural wrist movements, and slots them into a volumetric wireframe, as demonstrated in the official MR update gameplay video. 

**Why this and not that:** The developer chose hand tracking over standard 6DoF controllers because the mental model of solving a physical block puzzle maps perfectly to human hands. Using a controller's trigger button to mimic a "pinch" feels artificial for a puzzle this simple. Hand tracking eliminates the abstraction layer of a controller, reducing onboarding friction for non-gamers. 

**Where it fails:** The design fails when dealing with **optical occlusion and arm fatigue**. Because inside-out optical cameras track fingers, one hand often blocks the camera's view of the other hand when rotating complex pieces close together, causing tracking loss. Furthermore, ergonomic analyses of mid-air spatial interfaces indicate that holding arms unsupported to manipulate floating objects causes "gorilla arm" (severe shoulder/arm fatigue) during extended sessions.

**What I would change:** I would implement a robust "gaze and microgesture" fallback system. Allowing users to rest their arms on the table and simply look at a puzzle piece while doing a thumb-tap microgesture on their lap would completely solve the physical fatigue while retaining controller-free input.

![Tangkapan layar dari video referensi yang menunjukkan pengguna berinteraksi langsung dengan blok virtual di atas meja fisik](assets/fig2.png)

## 3. Use of AI

| Where | What it does | On-device or cloud | Cost it carries | Source + the line I am relying on |
|---|---|---|---|---|
| Perception | Hand and finger pose estimation (26 joints per hand) | On-device | Battery drain, thermal load, and compute latency | [Meta Hands Technology](https://developers.meta.com/horizon/design/hands-technology/) — "This data is processed by software using algorithms, often involving machine learning and computer vision, to recognize various hand positions and movements." |
| Perception | Scene understanding (Passthrough blending and spatial anchors) | On-device | High battery consumption and privacy considerations regarding room scanning | [Meta Presence Platform](https://developers.meta.com/horizon/blog/mixed-reality-mr-retention-presence-platform-tools-meta-quest-developers/) — "Passthrough provides a real-time 3D visualization of the physical world, allowing developers to comfortably and convincingly blend the user’s physical environment with virtual elements..." |

There is no meaningful AI used in the *content*, *interaction* (like NPCs or LLMs), or *rendering* (no cloud upscaling or AI frame generation). Cubism is a deterministic, math-based logic puzzle. The AI is entirely load-bearing in the **perception pipeline**; without on-device computer vision models inferring hand poses and room geometry in real-time, the core bare-hands mixed reality mechanic simply would not function.

## 4. Impact

**Intended benefit:** Provides a calm, highly accessible spatial reasoning exercise that improves lateral thinking without the motion sickness or sensory overload typical of high-action VR games.

**Privacy, security, or ethics:** To function in MR, the headset continuously captures passthrough camera frames and generates a scene mesh of the user's private living space (desks, walls, room layout). Even though this data is processed locally, it normalizes the continuous optical scanning of private environments and bystanders who have not consented to being filmed by the headset's external cameras.

**Accessibility / human factors:** Cubism's reliance on precise hand tracking makes it inaccessible to users with fine motor impairments or severe hand tremors. A user must be able to hold a steady "pinch" state and rotate their wrists smoothly. Any shaking causes the virtual block to drop or snap to the wrong grid space, as the optical tracking reads the tremor as an intentional release gesture.

## 5. What I take from this

Cubism demonstrates that Mixed Reality shines brightest when it respects physical metaphors, like placing a puzzle on an actual desk. However, reviewing its tracking mechanisms highlights that consumer MR hardware still struggles with input ergonomics; until we solve the physical strain of mid-air manipulation and optical occlusion, bare-hand tracking will remain best suited for short sessions rather than extended productivity.

---

## References

1. Meta Horizon OS Developers. (2026). *Hands Technology*. URL: https://developers.meta.com/horizon/design/hands-technology/ — accessed 10 Sep 2026
2. Meta Horizon OS Developers. (2026). *How Developers Are Increasing User Retention with Presence*. URL: https://developers.meta.com/horizon/blog/mixed-reality-mr-retention-presence-platform-tools-meta-quest-developers/ — accessed 10 Sep 2026
3. Van Bouwel, T. (2023). *Cubism - Mixed Reality Update Trailer*. YouTube. URL: https://www.youtube.com/watch?v=F0K8v8s7zF4 — accessed 10 Sep 2026
4. Van Bouwel, T. (2023). *Cubism Press Kit & Update Logs*. URL: https://www.cubism-vr.com/presskit/ — accessed 10 Sep 2026

## Figure credits

- Fig. 1 — My own annotated diagram explaining the passthrough and hand tracking pipeline, created 10 Sep 2026
- Fig. 2 — Screenshot taken from *Cubism - Mixed Reality Update Trailer* (Ref. 3), showing bare-hand interaction
- Fig. 3 — Official press image from *Cubism Press Kit* (Ref. 4) demonstrating passthrough occlusion

## AI-assistance disclosure

**What I used, and for what:** Gemini digunakan secara eksklusif untuk membantu mencari ide (*brainstorming* argumen) dan membantu mencari sumber referensi (*source*) yang relevan untuk mendukung argumen. 

### What I disagreed with my AI assistant about

Saat proses *brainstorming* ide, AI menyarankan agar saya mengkritik Cubism karena tidak menggunakan konten *generative AI* atau NPC berbasis LLM yang sedang populer saat ini. Saya menolak ide tersebut karena itu menunjukkan pemahaman yang dangkal terhadap tujuan utama aplikasi ini. Cubism adalah *puzzle* logika minimalis; menambahkan interaksi AI semacam itu akan merusak inti dari desain aplikasinya yang tenang. Sebagai gantinya, saya memilih untuk memfokuskan kritik murni pada limitasi fisik dan ergonomis dari pelacakan tangan (*optical occlusion* dan *gorilla arm*), yang merupakan klaim teknis yang jauh lebih kuat dan didukung oleh dokumentasi teknis.
