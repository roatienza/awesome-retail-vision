# Awesome Retail Vision

[![Link Check](https://github.com/roatienza/awesome-retail-vision/actions/workflows/link-check.yml/badge.svg)](https://github.com/roatienza/awesome-retail-vision/actions/workflows/link-check.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

A curated list of **research ideas, papers, datasets and tools for retail vision and embodied retail AI** — building photorealistic virtual retail worlds (SKU-level 3D, shelves, full stores) and training spatial foundation models inside them.

Part of the **Ubiquitous Retail Group (UCL) × UP Diliman Ubiquitous Computing Lab** collaboration, extending [Sari Sandbox](https://github.com/upeee/sari-sandbox-env). Supervised by [Dr. Rowel Atienza](https://github.com/roatienza).

**Start here:** 📋 [Research Tracks](RESEARCH_TRACKS.md) — the open problems we want to work on, from SKU digitization to spatial foundation models. Propose ideas via `IDEA:` issues ([CONTRIBUTING](CONTRIBUTING.md)).

---

## 🆕 What's New (Nov 2026)

- **World models went mainstream:** [Atlas](https://www.worldlabs.ai/blog/atlas) opened to everyone with an API and splat/mesh export (Nov 12) — AMD closed its [$8.2B acquisition](https://www.unite.ai/amd-closes-world-labs-acquisition-and-names-fei-fei-li-chief-scientist/) four days later; [Genie 4](https://deepmind.google/blog/genie-4-a-new-generation-of-world-simulation/) added native audio + real-time steering (Oct 27); [Frameboy](https://www.unite.ai/world-labs-releases-frameboy-for-real-time-atlas-exploration/) streams generated worlds at ~15 fps in a browser (Nov 5).
- **Try-on left the lab:** OpenAI shipped a [virtual try-on mode in ChatGPT](https://www.pymnts.com/news/artificial-intelligence/2026/openai-adds-virtual-try-on-feature-chatgpt/) (Oct 1); Maybelline put real-time makeup try-on [inside ChatGPT](https://www.marketingtechnews.net/news/maybelline-brings-virtual-makeup-try-on-to-chatgpt-as-ai-transforms-beauty-shopping/) (Nov 10); VibeDM brought try-on + agentic checkout [into Instagram DMs](https://finance.yahoo.com/media-advertising/articles/vibedm-brings-agentic-shopping-viral-120000191.html) (Nov 12).
- **Synthetic retail data grew up:** [TwinStore](https://arxiv.org/abs/2610.30909) turns a floor plan or shelf photos into a store twin populated by VLM shoppers whose trips end in receipts (Oct 22); [Spatial Foundry](https://arxiv.org/abs/2611.17318) released 5,280 editable 3D scenes with aligned visual/geometry/temporal data (Nov 12); [ShelfChange3D](https://arxiv.org/abs/2610.01283) shipped 145K synthetic shelf-change scenes (Oct 1).
- **Spatial-FM race is on:** [Iris-Z](https://arxiv.org/abs/2611.16010) argues one generative model should replace specialist geometry models (Nov 11); [Sophon](https://arxiv.org/abs/2611.14838) shows open-weight VLMs collapse to chance on spatial questions once priors are stripped (Nov 10); [WorldFoundry](https://arxiv.org/abs/2611.10771) unifies world-model evaluation across 270 models and 74 benchmarks (Nov 10).
- **Agentic shopping split:** Amazon blocks Meta's Muse agent (10M+ users) while Walmart welcomes it with an [Agent Gateway](https://techcrunch.com/2026/10/21/while-amazon-blocks-ai-agents-walmart-rolls-out-the-welcome-mat/) (Oct 21) — the retail-agent distribution war our Sari Sandbox agents will eventually fight.

---

## 🎯 The Big Picture

**Overarching goal:** create a Just-Walk-Out-like virtual retail environment — near-1:1 3D SKUs, generated shelves and scenes, human clones — produce *many* such worlds, and train **spatial foundation models** on them. Amazon focuses on retail world models; we focus on spatial foundation models.

**Why SKUs first:** if we can generate near-1:1 3D product objects, half the work is done — shelves and scenes are comparatively easy. The hard parts, in order: SKU digitization → scene generation → human clones.

**Target venue:** ICCV 2027 (main paper deadline expected March 7, 2027).

---

## 📑 Contents

- [What's New (Nov 2026)](#-whats-new-nov-2026)
- [Core Research Threads](#-core-research-threads)
  - [Virtual Try-On / Try-Off for Retail](#virtual-try-on--try-off-for-retail)
  - [3D Generation & 3D Gaussian Splatting](#3d-generation--3d-gaussian-splatting)
  - [Texture Generation & Super-Resolution](#texture-generation--super-resolution)
  - [Scene, Store & World Generation](#scene-store--world-generation)
  - [Spatial Foundation Models](#spatial-foundation-models)
  - [Embodied Retail Agents & Benchmarks](#embodied-retail-agents--benchmarks)
  - [Human Clones & Digital Humans](#human-clones--digital-humans)
- [Datasets & Assets](#-datasets--assets)
- [Tools & Pipelines](#-tools--pipelines)
- [Related Surveys](#-related-surveys)
- [Open Problems](#-open-problems)

---

## 🔥 Core Research Threads

### Virtual Try-On / Try-Off for Retail

The inspiration for our texture→3D / 3D→texture SKU tasks: bidirectional garment transfer, applied to retail packaging.

- [Voost: A Unified and Scalable Diffusion Transformer for Bidirectional Virtual Try-On and Try-Off](https://arxiv.org/abs/2508.04825) — jointly learns try-on and try-off with a single DiT; SOTA on both. *Why retail:* try-off is the more learnable direction — the same asymmetry should hold for SKU texture↔3D transfer; bidirectional consistency is the trick worth stealing. [Project page](https://nxnai.github.io/Voost/) (SIGGRAPH Asia 2025). `texture` `sku-3d`
- [RoboTryOn: Synthesizing Dexterous Robot Demonstrations from Human Videos via Virtual Try-On](https://arxiv.org/abs/2611.05163) — treats human-to-robot demonstration synthesis as a try-on problem: dress the robot embodiment into an egocentric human video so the demo reads as robot motion, closing the visual/action gap for high-DoF hands. *Why retail:* the first bridge between our try-on thread and Track E — restocking demos filmed on humans become robot policies without teleop. (Nov 2026). `texture` `embodied`
- [FlexTry-On: A Time-Efficient Framework for Multi-Scenario Virtual Try-on](https://arxiv.org/abs/2610.39646) — one diffusion framework covering cloth-to-person, person-to-person and cross-domain try-on instead of per-scenario pipelines. *Why retail:* a single model that handles catalog photos, customer photos and influencer footage is what a production try-on API needs. (Oct 2026). `texture`
- [ShoeFit: A New Dataset and Dual-image-stream DiT Framework for Virtual Footwear Try-On](https://arxiv.org/abs/2610.18325) — footwear try-on dataset + dual-stream DiT keeping 3D consistency and texture authenticity where garment-centric VTON fails. *Why retail:* try-on beyond garments — shoes are a huge catalog slice and the hardest rigid case. (Oct 2026). `texture` `dataset`
- [TryOnReward: Learning Foveated Consistency for Reinforcement Fine-Tuning of Virtual Try-On](https://arxiv.org/abs/2609.13259) — RL fine-tuning against a VLM reward that looks where humans look (seams, print alignment) instead of global fidelity metrics. *Why retail:* the reward trick transfers directly to SKU re-texturing — reward "does the barcode still scan / does the label still read", not FID. (Sep 2026). `texture`
- [TexTailor: Texture-Preserving Video Virtual Try-On via Adaptive Garment Conditioning](https://arxiv.org/abs/2609.39335) — high-resolution video try-on that keeps garment texture stable across frames via explicit positional garment conditioning. *Why retail:* texture preservation under motion is what 3D→texture re-skinning must survive when a shelf camera pans past a SKU. (Sep 2026). `texture` `sku-3d`

### 3D Generation & 3D Gaussian Splatting

Image/text → 3D assets, and the 3DGS representation our texture work builds on.

- [TRELLIS: Structured 3D Latents for Scalable and Versatile 3D Generation](https://arxiv.org/abs/2412.01506) — unified structured-latent 3D generation decodable to 3D Gaussians or meshes; image-to-3D SOTA. *Why retail:* our candidate SKU 3D generator — image-to-3D from product photos, with local editing for label fixes. [Code](https://github.com/microsoft/TRELLIS) (CVPR 2025 Spotlight). `sku-3d` `3dgs`
- [Hunyuan3D 2.5: Towards High-Fidelity 3D Assets Generation with Ultimate Details](https://arxiv.org/abs/2506.16504) — 10B shape model (LATTICE) + PBR texture painting. *Why retail:* strongest open high-fidelity image-to-3D baseline; PBR output matters for shelf lighting realism. [Code](https://github.com/Tencent-Hunyuan/Hunyuan3D-2) (Tencent, 2025). `sku-3d` `texture`
- [Heat Kernel Textures: the Geodesic Gaussians That Do Not Splat](https://arxiv.org/abs/2609.07557) — UV-free texture representation: anisotropic heat kernels on the mesh surface, no UV unwrapping, no seams. *Why retail:* our candidate texture representation for SKU re-texturing — kills UV seams/distortion on boxy packaging; integrates with PBR rendering. [Project page](https://www.simofoti.com/publications) (ECCV 2026 Oral). `3dgs` `texture`
- [Sprint3D: Accelerating End-to-End 3D Asset Generation through Pipeline Optimization](https://arxiv.org/abs/2611.16701) — profiles a public image-to-3D pipeline and cuts end-to-end asset time several-fold by optimizing mesh processing, not just network sampling. *Why retail:* SKU digitization is a throughput problem — we need thousands of assets per store, and pipeline engineering buys more than model swaps. (Nov 2026). `sku-3d` `tooling`
- [SeMo3D: Unifying 3D Generation, Editing, and Completion via Selective Modeling](https://arxiv.org/abs/2611.02568) — one model that generates, edits and completes 3D assets. *Why retail:* generate-then-fix-labels is our Track A loop; unified edit/completion beats running separate models per fix. (Nov 2026). `sku-3d`
- [Bri3D: Bridging the Object-Scene Gap in Single-Image 3D Generation via Scene-Anchor](https://arxiv.org/abs/2611.07961) — scene-anchored single-image 3D generation that keeps objects consistent with their surroundings. *Why retail:* shelf photos are object-in-scene, not object-on-white; object-only generators misread occluded SKUs. (Nov 2026). `sku-3d` `scene-gen`
- [MIKU: Material Invariance and Knowledge Unification for PBR Generation](https://arxiv.org/abs/2611.07354) — PBR material generation with material invariance. *Why retail:* shelf lighting varies by zone; PBR material priors keep generated packaging plausible under store lighting. (Nov 2026). `sku-3d` `texture`
- [Deformable Texture Maps: Compiling Dynamic Microgeometry into Neural Textures](https://arxiv.org/abs/2611.13677) — compiles deformation-driven microgeometry into a continuous neural texture, no explicit geometry instantiation. *Why retail:* crinkled chip bags and dented cans are deformable-surface problems; texture-level microgeometry is cheaper than simulating it. (Nov 2026). `texture` `3dgs`
- [RouTex: Multi-reference 3D Texture Generation by Reprogramming Rotary Position Encoding](https://arxiv.org/abs/2611.06070) — multi-reference 3D texture generation via RoPE reprogramming. *Why retail:* our SKU re-texturing needs multi-reference conditioning — front + back + nutrition panel as separate references. (Nov 2026). `texture` `sku-3d`

### Texture Generation & Super-Resolution

Getting texture-grade product imagery without buying and scanning every SKU.

- [GarmentZoom: Generating Zoomable Images from Garment Listings](https://arxiv.org/abs/2606.29535) — reference-based super-resolution: full-view photo + unaligned close-up → zoomable 3–20× detail. *Why retail:* exactly our texture-acquisition problem — lift average-quality scraped product photos to texture-grade close-ups using cheap reference material. [Project page](https://jason-31.github.io/garmentzoom/) (UW, 2026). `texture` `sku-3d`

### Scene, Store & World Generation

From single SKUs to whole stores and interactive worlds.

- [Genie 3: A new frontier for world models](https://deepmind.google/blog/genie-3-a-new-frontier-for-world-models/) — text → real-time navigable interactive worlds (24 fps, 720p, minutes of consistency). *Why retail:* the ceiling for what generated worlds can do; our worlds are asset-based and controllable where Genie is prompt-based and not. (DeepMind, Aug 2025). `world-model` `scene-gen`
- [Marble: A Multimodal World Model](https://www.worldlabs.ai/blog/marble-world-model) — text/image/video/3D-layout → persistent 3D worlds, exportable as Gaussian splats or meshes. *Why retail:* the splat/mesh export path is the bridge from prompt-generated worlds to our asset-based pipeline. [Marble Labs](https://www.worldlabs.ai/blog/marble-world-model) (World Labs, Nov 2025). `world-model` `3dgs`
- [Atlas: A World Model for Spatial Intelligence](https://www.worldlabs.ai/blog/atlas) — omni world model (text/image/video/3D in, shared spatial context out) from World Labs; reconstructs real spaces from a handful of photos, generates multiple camera paths through the same scene, and exports to downstream workflows. Opened to everyone with apps (Viewfinder, Chisel, Splats-to-Mesh, Relight), developer API and Blender integration on [Nov 12](https://www.auganix.org/xr-news-world-labs-atlas-world-model-apps-api/); [Frameboy](https://www.unite.ai/world-labs-releases-frameboy-for-real-time-atlas-exploration/) streams its scenes at ~15 fps in-browser (Nov 5); AMD closed its [$8.2B acquisition](https://www.unite.ai/amd-closes-world-labs-acquisition-and-names-fei-fei-li-chief-scientist/) on Nov 16 with Fei-Fei Li as Chief Scientist. *Why retail:* photo-of-your-store → navigable 3D world is now an API call; the splats-to-mesh + relight path is a shortcut for Track B scene bootstrapping — and AMD's compute behind it makes this the default world-model stack. (World Labs, Sep–Nov 2026). `world-model` `3dgs`
- [Genie 4: A new generation of world simulation](https://deepmind.google/blog/genie-4-a-new-generation-of-world-simulation/) — real-time navigable worlds with native audio generated inside the model loop and Gemini-powered reasoning; research preview to trusted testers, coming to Google AI Ultra / Gemini API. *Why retail:* ambient store sound + audio-reactive agents are new data modalities for retail sims; still prompt-based, so it complements rather than replaces our asset pipeline. (DeepMind, Oct 27, 2026). `world-model` `scene-gen`
- [WorldFoundry: Towards Unified Infrastructure for World Intelligence](https://arxiv.org/abs/2611.10771) — open-source infrastructure standardizing generative world-model evaluation: 270 model entries, 74 benchmarks, 62 metrics, reproducible inference + evidence-aware scorecards. *Why retail:* when we claim our generated stores train better spatial FMs, this is the harness that makes the claim reproducible. [Coverage](https://blockchain.news/news/worldfoundry-open-source-generative-world-models) (Nov 10, 2026). `world-model` `tooling`
- [From Video to Digital Twin: World Models and Gaussian Splatting on In-the-Wild Video](https://arxiv.org/abs/2611.10013) — honest study of what world models + 3DGS actually recover from uncurated walkthrough video (a food-bank warehouse) with no scans or site visit. *Why retail:* exactly our "phone video of a sari-sari store → digital twin" dream, with a realistic accounting of what breaks. (Nov 4, 2026). `world-model` `3dgs`
- [OfficeTwin: 3D Reconstruction of Redundant Scenes through Partial Viewpoint Perception](https://arxiv.org/abs/2611.10241) — feed-forward reconstruction turned into robot-usable digital twins (object identity, physical properties, watertight volumes) for weakly-textured repetitive scenes. *Why retail:* supermarket shelves are the canonical redundant scene; the identity+volume enrichment is what manipulation training needs. (Nov 6, 2026). `world-model` `embodied`

### Spatial Foundation Models

The end goal: models with grounded 3D spatial reasoning, pretrained in our generated retail worlds.

- [SpatialRGPT: Grounded Spatial Reasoning in Vision-Language Models](https://arxiv.org/abs/2406.01584) — region-level 3D spatial reasoning via 3D-scene-graph data curation + depth plugin; SpatialRGBT-Bench. *Why retail:* the architecture and benchmark template for our spatial FM — region-aware reasoning is exactly what shelf auditing needs. [Code](https://github.com/AnjieCheng/SpatialRGPT) (NeurIPS 2024). `spatial-fm` `embodied`
- [Iris-Z: Scaling One Generative Model Past Specialist Geometry Models](https://arxiv.org/abs/2611.16010) — the bitter-lesson argument for spatial intelligence: one generative model, one training task, scaling with data/compute — beating specialist geometry models. *Why retail:* informs whether our spatial FM should be a specialist or a generalist trained in many generated worlds. (Nov 11, 2026). `spatial-fm`
- [Sophon: A Procedural Diagnostic for Spatial Reasoning in Vision-Language Models](https://arxiv.org/abs/2611.14838) — open-source procedural diagnostic: open-weight VLMs score 85–94% on spatial benchmarks yet collapse to chance when object/scene/texture priors are stripped. *Why retail:* a warning for Track D — a shelf-auditing FM that aces benchmarks may be riding priors, not doing geometry; Sophon-style stripped diagnostics belong in our eval suite. [Code](https://github.com/tsaabrot/sophon) (Nov 10, 2026). `spatial-fm` `tooling`
- [SpaceMCP: Vision Language Model Spatial Reasoning via Model Context Protocol](https://arxiv.org/abs/2611.15680) — augments a VLM with structured spatial functions over feed-forward 3D reconstructions through an MCP-style tool interface. *Why retail:* a cheap alternative to end-to-end spatial FMs — give a commodity VLM a geometry tool server and let it audit shelves. (Nov 11, 2026). `spatial-fm` `tooling`
- [Spatial Foundry: A Multimodal Dataset for Spatial Intelligence](https://arxiv.org/abs/2611.17318) — 5,280 furnished 3D scene configurations with editable assets and aligned visual, geometric and temporal data (appearance, camera motion, scene changes under one reference). *Why retail:* the closest public template for the "many generated worlds + aligned modalities" dataset Track D needs — residential today, retail-shaped tomorrow. (Nov 12, 2026). `spatial-fm` `dataset`

### Embodied Retail Agents & Benchmarks

Simulators, agents and benchmarks in the retail domain — our home turf.

- [Sari Sandbox: A Virtual Retail Store Environment for Embodied AI Agents](https://arxiv.org/abs/2508.00400) — photorealistic 3D retail sim, 250+ interactive grocery items, VR + VLM agent, SariBench human demos. *Why retail:* the base we extend; its real-scanned SKU textures are the quality bar for generated ones. [Code](https://github.com/upeee/sari-sandbox-env) (ICCV 2025 Workshop). `embodied` `dataset`
- [Sari Sandbox 2: An Embodied AI Agent Platform for Virtual Retail Environments](#) — LiDAR+SLAM scene-graph world model, store builder, multiplayer, 1.8× faster; agent hits 100/91/37% on easy/average/difficult tiers. *Why retail:* the platform this group builds on. (Villa, Baclor & Atienza, UP Diliman, 2026 — preprint). `embodied` `tooling`
- [RoboBenchMart: Benchmarking Robots in Retail Environment](https://arxiv.org/abs/2511.10276) — dark-store manipulation benchmark: procedural layout generator, trajectory pipeline, baselines. *Why retail:* closest robotic-retail benchmark; its 3D SKUs lack real barcode/nutrition-fact textures — the gap our SKU pipeline targets. [Code](https://github.com/emb-ai/RoboBenchMart) (FusionBrain, 2025). `embodied` `scene-gen`
- [WRS Future Convenience Store Challenge (FCSC)](https://f-csc.org/en/wrs-fcsc-2025/) — annual robot competition: restocking and disposal in a simulated convenience store. *Why retail:* the task taxonomy (stocking, FIFO disposal, shelf arrangement) maps directly onto our agent task suite. (WRS, 2024–2025). `embodied`
- [TwinStore: A Synthetic Consumer Platform Using Vision-Language Models](https://arxiv.org/abs/2610.30909) — source-available platform that turns a store into a digital twin (82 ready-made formats, a floor-plan image, or phone photos of shelves) and fills it with VLM synthetic shoppers who plan trips, walk aisles, and buy off rendered shelves with packs, price tags and promo signs — every trip ends in a receipt. *Why retail:* synthetic footfall + receipts is the data engine Track E was missing; also a direct test of whether our generated SKUs survive a shopper's eye. (Oct 22, 2026). `embodied` `dataset`
- [ShelfChange3D: Object-Level 3D Change Detection for Retail Shelf Monitoring](https://arxiv.org/abs/2610.01283) — reformulates out-of-stock detection as object-level 3D change detection between two RGB-D observations, with 145K synthetic scenes + real test data; each change localized with a 3D bounding box for downstream robots. *Why retail:* the metric-3D shelf-audit task our stores can generate training data for at scale. (Oct 1, 2026). `embodied` `dataset`
- [Physical AI Smart Spaces: A Large-Scale Benchmark for Multi-Camera 3D Perception in Smart Spaces](https://arxiv.org/abs/2610.02580) — 280+ hours of synchronized 1080p footage from ~1,800 cameras across warehouses, hospitals and retail venues, with multi-camera 3D annotations. *Why retail:* the real-world counterpart to our synthetic multi-camera store footage — the transfer test for Track D. (Oct 1, 2026). `embodied` `dataset`
- [Supermarket Product Detection and Recognition with Rectified Imagery](https://arxiv.org/abs/2610.08126) — tackles the close-knit rack problem: rectified imagery for product detection/recognition in dense supermarket shelving. *Why retail:* a strong baseline for the shelf-audit task our generated stores will train. (Oct 6, 2026). `embodied`
- [Scoring, Not Learning: Decomposing Catalog-Consolidation Gains in Web-Scraped Retail Product Recognition](https://arxiv.org/abs/2611.08655) — dissects how much of web-scraped product-recognition performance comes from catalog consolidation vs actual learning. *Why retail:* a caution for our Track A evaluation — scraped-photo benchmarks can flatter models via catalog overlap; our 1:1-ness eval must control for it. (Nov 5, 2026). `embodied` `sku-3d`
- [Detecting Defects that Matter: An Application-Driven Benchmark for Anomaly Detection in Manufacturing and Retail Logistics (VAND 4.0 Challenge)](https://arxiv.org/abs/2610.04392) — application-driven anomaly-detection benchmark spanning manufacturing and retail logistics. *Why retail:* damaged-packaging detection is a shelf-audit subtask our worlds can synthesize. (Oct 3, 2026). `embodied`
- [Prototype-Guided Dynamic Domain Modulation + Multi-SKU Shampoo Bottle Defect Benchmark](https://arxiv.org/abs/2610.38194) — large-scale multi-SKU defect dataset with instance-level annotations and product-variant identities across bottle geometry, label layout and reflectance. *Why retail:* SKU-aware defect detection is exactly "1:1-ness under domain shift" — the eval Track A needs for re-textured SKUs. (Oct 28, 2026). `embodied` `dataset`
- [RetailLightNet: Real-Time Smart Retail Analytics through Fog Computing](https://arxiv.org/abs/2610.35871) — lightweight model + fog deployment for latency/privacy-constrained in-store video analytics (customer tracking, shelf inventory). *Why retail:* the deployment endgame for shelf-audit models — edge inference on store cameras, no raw video leaving the building. (Oct 16, 2026). `embodied`

### Human Clones & Digital Humans

Controllable shoppers and staff inside generated stores. *(Track C — least explored, highest risk; help wanted.)*

- [Video Diffusion Avatars: Taming Video Diffusion Models into Controllable 3D Avatars](https://arxiv.org/abs/2610.23772) — photo-realistic, multi-view consistent 3D avatars from a single image by fine-tuning a video diffusion model for camera, expression and upper-body control. *Why retail:* single-photo shoppers for Track C — internet-scale motion/physics priors without 3D capture rigs. (Oct 16, 2026). `human-avatar`
- [ZARA: Zero-shot Animatable and Relightable 3D Avatar Reconstruction from a Single Image](https://arxiv.org/abs/2611.10562) — feed-forward single-image → animatable 3D Gaussian avatar with intrinsic attributes, relightable without person-specific optimization. *Why retail:* shoppers that inherit store lighting instead of looking pasted-in; zero-shot means catalog-scale avatar generation. (Nov 7, 2026). `human-avatar` `3dgs`
- [Single Camera based Simulation and Try-on Ready Avatar Modeling](https://arxiv.org/abs/2610.34223) — try-on-ready avatars from monocular video/single images via layered garment+body representation with distinct motion dynamics. *Why retail:* the garment/body split is what lets Track C shoppers wear arbitrary catalog SKUs. (Oct 25, 2026). `human-avatar` `texture`
- [DualCast: Dual-Image Conditioned Diffusion Transformers for Digital Human E-Commerce Video Generation](https://arxiv.org/abs/2611.05825) — preserves product appearance, human identity and video style by explicitly separating "what is presented" from "who presents it". *Why retail:* the exact conditioning split for product-demo videos — our generated shoppers presenting generated SKUs. (Nov 4, 2026). `human-avatar`
- [Emo-LiveSync: Real-Time Universal Lip Synchronization with Explicit Emotion Control](https://arxiv.org/abs/2611.09074) — real-time lip sync with explicit emotion control, efficient enough for live use. *Why retail:* talking staff avatars for in-store assistant simulations. (Nov 6, 2026). `human-avatar`
- [AVTR-1: Open Stack for Real-Time Interactive Avatars](https://arxiv.org/abs/2609.22913) — open stack for real-time interactive avatar conversations: 153M-param autoregressive flow-matching motion generator, speech synchronization, frame scheduling, interruption handling. *Why retail:* the plumbing for interactive shopper/staff agents — motion generation is solved, integration is the missing piece. (Sep 2026). `human-avatar` `tooling`

---

## 🗃 Datasets & Assets

- **Sample SKU label textures** — [`images/555_TUNA_AFRITADA_155G.jpg`](images/555_TUNA_AFRITADA_155G.jpg) (8192×3618, 7.0 MB) and [`images/ZESTO_ROOT_BEER_500ML_LABEL.jpg`](images/ZESTO_ROOT_BEER_500ML_LABEL.jpg) (4000×1579, 2.1 MB): wrap-around label scans of a canned tuna and a bottled root beer, the concrete target format for Track A — flat label art to be wrapped onto can/bottle geometry, with barcode and nutrition facts intact.

| 555 Tuna Afritada 155g | Zesto Root Beer 500ml |
|---|---|
| [![555 Tuna Afritada 155g label texture](images/555_TUNA_AFRITADA_155G_preview.jpg)](images/555_TUNA_AFRITADA_155G.jpg) | [![Zesto Root Beer 500ml label texture](images/ZESTO_ROOT_BEER_500ML_LABEL_preview.jpg)](images/ZESTO_ROOT_BEER_500ML_LABEL.jpg) |

- [RoboBenchMart Assets](https://huggingface.co/datasets/emb-ai/RoboBenchMart_assets) — 2.4 GB of retail environment assets (shelves, fake shelves, downscaled props) for ManiSkill. *Why retail:* reusable shelf/prop geometry; pair with our SKU textures. `dataset`
- [Spatial Foundry](https://arxiv.org/abs/2611.17318) — 5,280 furnished 3D scene configurations with editable assets and aligned visual/geometry/temporal modalities. *Why retail:* the dataset schema to imitate when we release retail worlds — aligned appearance, camera motion and scene change under one reference. (Nov 12, 2026). `dataset` `spatial-fm`
- [ShelfChange3D](https://arxiv.org/abs/2610.01283) — 145K synthetic shelf-change scenes + real test data for object-level 3D change detection. *Why retail:* ready-made shelf-audit training data; our stores should generate the same task format. (Oct 1, 2026). `dataset` `embodied`
- [Multi-SKU Shampoo Bottle Defect Benchmark](https://arxiv.org/abs/2610.38194) — instance-level defect annotations + product-variant identities across bottle geometry, label layout, reflectance. *Why retail:* the SKU-aware defect eval for re-textured SKUs. (Oct 28, 2026). `dataset` `sku-3d`
- [Physical AI Smart Spaces](https://arxiv.org/abs/2610.02580) — 280+ h synchronized multi-camera 3D perception footage from ~1,800 cameras in warehouses, hospitals, retail. *Why retail:* the real-footage transfer test for synthetic store pretraining. (Oct 1, 2026). `dataset` `spatial-fm`
- Sari Sandbox product scans — 250+ real-scanned SKU textures (from the original Sari Sandbox release; see [repo](https://github.com/upeee/sari-sandbox-env)). *Why retail:* scanner-grade ground truth for evaluating generated textures. `dataset` `sku-3d`

## 🛠 Tools & Pipelines

- [Sari Sandbox Store Builder](https://github.com/upeee/sari-sandbox-env) — in-sandbox store construction (Sari Sandbox 2). *Why retail:* our starting point for procedural planogram generation. `tooling` `scene-gen`
- [ManiSkill](https://github.com/haosulab/ManiSkill) — the simulation backend RoboBenchMart builds on (Vulkan-based, GPU-parallel). *Why retail:* candidate backend if we benchmark manipulation in our stores. `tooling` `embodied`
- [WorldFoundry](https://arxiv.org/abs/2611.10771) — open-source unified infrastructure for world-model evaluation: 270 model entries, 74 benchmarks, 62 metrics; CLI/TUI/Studio workflows with evidence-aware scorecards. *Why retail:* reproducible claims that generated retail worlds actually train better models. (Nov 10, 2026). `tooling` `world-model`
- [Sophon](https://arxiv.org/abs/2611.14838) — open-source procedural spatial-reasoning diagnostic (paired point-cloud stimuli, three coordinate systems, four question types). *Why retail:* strip the priors from our shelf-audit FM and see if geometry survives. (Nov 10, 2026). `tooling` `spatial-fm`
- [SpaceMCP](https://arxiv.org/abs/2611.15680) — MCP-style spatial-function server over feed-forward 3D reconstructions for commodity VLMs. *Why retail:* bolt spatial reasoning onto an off-the-shelf VLM instead of training one. (Nov 11, 2026). `tooling` `spatial-fm`
- [AVTR-1](https://arxiv.org/abs/2609.22913) — open real-time interactive avatar stack: motion generation, speech sync, frame scheduling, interruption handling. *Why retail:* the integration layer for interactive shopper/staff agents. (Sep 2026). `tooling` `human-avatar`
- [Sprint3D](https://arxiv.org/abs/2611.16701) — end-to-end image-to-3D pipeline optimization (mesh processing, not just sampling); several-fold asset-time reduction on a public pipeline. *Why retail:* SKU digitization throughput. (Nov 12, 2026). `tooling` `sku-3d`

## 📚 Related Surveys

- [Spatial intelligence in vision-language models: a comprehensive survey](https://link.springer.com/article/10.1007/s10462-026-11671-x) — unified survey of spatially-enhanced VLMs; empirical study across 37 models, 9 benchmarks. *Why retail:* the map of Track D's landscape. (Artificial Intelligence Review, Aug 2026). `spatial-fm`
- [WorldFoundry: Towards Unified Infrastructure for World Intelligence](https://arxiv.org/abs/2611.10771) — defines generative world models as predictive dynamical systems (persistent state, intervention response, counterfactual trajectories) and catalogs 270 models / 74 benchmarks / 62 metrics. *Why retail:* the definitional paper for what "world model" should mean when we market our stores as training environments. (Nov 10, 2026). `world-model`

## ❓ Open Problems

The live list lives in [RESEARCH_TRACKS.md](RESEARCH_TRACKS.md). Headline questions:

1. **Texture acquisition at scale** — can reference-based super-resolution (GarmentZoom-style) replace buying-and-scanning every SKU?
2. **Texture→3D for packaging** — enforcing box/can/bottle priors so generated SKUs are shelf-ready, with legible barcodes and nutrition facts.
3. **3D→texture (re-texturing)** — UV-free representations (HKTex) vs UV atlases on boxy packaging; consistency across carton faces.
4. **Evaluating 1:1-ness** — barcode decodability, OCR of nutrition panels, texture fidelity vs scanner ground truth.
5. **Synthetic-to-real transfer** — how much does spatial-FM pretraining in generated stores transfer to real store footage?
6. **Human clones** — identity-preserving avatars with garment handling and plausible shopping behavior, at data-generation scale.
7. **Priors vs geometry (new, Nov 2026)** — [Sophon](https://arxiv.org/abs/2611.14838) shows open-weight VLMs collapse to chance on spatial questions once object/scene/texture priors are stripped. Is our future shelf-audit FM doing geometry — or riding priors? Stripped-prior diagnostics must join the eval suite before we trust benchmark scores.
8. **Catalog-consolidation confounds (new, Nov 2026)** — [Scoring, Not Learning](https://arxiv.org/abs/2611.08655) shows web-scraped product-recognition gains can come from catalog overlap rather than learning. Our scraped-photo baselines and Track A evals must control for catalog leakage.
9. **World-model claims need a harness (new, Nov 2026)** — [WorldFoundry](https://arxiv.org/abs/2611.10771) defines world models as predictive dynamical systems with persistent state and intervention response. When we claim our generated stores are "worlds that train models", persistent-state and intervention tests — not visual plausibility — are the bar.

---

## License

MIT © [Rowel Atienza](https://github.com/roatienza) — see [LICENSE](LICENSE).