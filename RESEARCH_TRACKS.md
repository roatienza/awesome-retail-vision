# Research Tracks

Long-horizon research directions for the group, ordered from near-term (SKU assets) to the overarching goal (spatial foundation models trained in virtual retail worlds). Each track lists the open questions we want answers to — pick one and open an `IDEA:` issue.

## Track A — SKU Digitization: Texture → 3D → Texture

**Goal:** near-1:1 3D replicas of real SKUs (barcode, nutrition facts, label typography intact) that can populate shelves at scale.

- **Texture acquisition without buying every product.** The first Sari Sandbox group bought originals and scanned them on a lab scanner; scraped photos are only average quality. Open questions: can GarmentZoom-style reference-based super-resolution lift scraped product photos to texture-grade quality? Can close-up references be sourced cheaply (manufacturer sites, packaging PDFs, user photos)?
- **Reference assets in-repo:** [`images/`](images/) holds two wrap-around label scans — [555 Tuna Afritada 155g](images/555_TUNA_AFRITADA_155G.jpg) (8192×3618) and [Zesto Root Beer 500ml](images/ZESTO_ROOT_BEER_500ML_LABEL.jpg) (4000×1579) — as the concrete target format: flat label art that texture→3D must wrap onto can/bottle geometry, with barcode and nutrition facts surviving the round trip.
- **Texture → 3D:** generate a complete, correctly-proportioned 3D SKU from flat packaging art + a few reference photos. Open questions: how to enforce box/can/bottle priors so generated geometry is shelf-ready; how to keep printed text legible (barcodes, nutrition panels) through the generation pipeline. *(Nov 2026: [Sprint3D](https://arxiv.org/abs/2611.16701) shows pipeline engineering alone buys several-fold throughput on public image-to-3D stacks; [Bri3D](https://arxiv.org/abs/2611.07961) anchors object generation in its scene — relevant since shelf photos are object-in-scene, not object-on-white; [MIKU](https://arxiv.org/abs/2611.07354) adds PBR material priors for shelf-lighting realism.)*
- **3D → texture (re-texturing):** re-skin an existing 3D SKU with new packaging art — the retail analogue of virtual try-on, and the easier direction (cf. try-off being more learnable than try-on in Voost). Open questions: UV-free texture representations (HKTex) vs UV atlases for boxy packaging; editing consistency across the 6 faces of a carton. *(Nov 2026: [RouTex](https://arxiv.org/abs/2611.06070) does multi-reference 3D texture generation via RoPE reprogramming — front + back + nutrition panel as separate references is our case; [TryOnReward](https://arxiv.org/abs/2609.13259) suggests RL against a "does the barcode still scan" reward instead of global fidelity metrics; [Deformable Texture Maps](https://arxiv.org/abs/2611.13677) handle crinkled-bag microgeometry as texture, not geometry.)*
- **Evaluation:** how do we measure "1:1-ness" of a generated SKU? Barcode decodability, OCR of nutrition facts, texture fidelity vs scanner ground truth. *(Nov 2026 caution: [Scoring, Not Learning](https://arxiv.org/abs/2611.08655) shows catalog consolidation can masquerade as recognition gains in web-scraped benchmarks — control for catalog overlap; [V-CAPE](https://arxiv.org/abs/2610.38611) offers a visual-consistency metric for product image editing that may adapt to SKU re-texturing; the [multi-SKU shampoo defect benchmark](https://arxiv.org/abs/2610.38194) is the closest existing SKU-aware eval.)*

## Track B — Store and Scene Generation

**Goal:** procedural, photorealistic store interiors (shelves, fridges, checkout) that accept arbitrary SKU sets.

- Claimed to be easier than SKU digitization once assets exist — but open questions remain: physically plausible shelf packing (planogram-aware placement), lighting variation across store zones, and layout diversity for training-time world variety.
- Candidate approach: start from the Sari Sandbox store builder, automate planogram generation, and render with the same asset pipeline as Track A.
- *(Nov 2026: [Atlas](https://www.worldlabs.ai/blog/atlas) now offers photo-of-a-space → navigable 3D world as an API, with splats-to-mesh export and relighting — a bootstrapping shortcut for real-store scans; [From Video to Digital Twin](https://arxiv.org/abs/2611.10013) honestly documents what world models + 3DGS recover from uncurated walkthrough video; [OfficeTwin](https://arxiv.org/abs/2611.10241) shows how to enrich feed-forward reconstructions into robot-usable twins with object identity and watertight volumes; [Spatial Foundry](https://arxiv.org/abs/2611.17318) is the dataset schema to imitate — 5,280 editable scenes with aligned visual/geometry/temporal modalities.)*

## Track C — Human Clones in the Store

**Goal:** controllable digital humans that shop, restock, and checkout inside the generated stores.

- Open questions: identity-preserving avatars from a single photo/video; garment handling on articulated bodies (virtual try-on applied to 3D avatars, not flat images); plausible shopping behaviors (trajectories, dwell times, grasp poses) for data generation.
- This is the least-explored track and likely the highest-risk one — treat as a stretch goal behind Tracks A/B.
- *(Nov 2026: this track is no longer empty — see the new [Human Clones & Digital Humans](README.md#human-clones--digital-humans) section: [Video Diffusion Avatars](https://arxiv.org/abs/2610.23772) (single-image controllable 3D avatars), [ZARA](https://arxiv.org/abs/2611.10562) (zero-shot relightable Gaussian avatars), [DualCast](https://arxiv.org/abs/2611.05825) (product-demo conditioning split), [AVTR-1](https://arxiv.org/abs/2609.22913) (open real-time interactive stack). Shopping-behavior generation has a first reference point: [TwinStore](https://arxiv.org/abs/2610.30909) simulates VLM shoppers whose trips end in receipts.)*

## Track D — Spatial Foundation Models in Retail Worlds

**Goal:** the overarching goal. Use many generated store "worlds" to train spatial foundation models — the group's differentiator vs Amazon's retail-world-model focus.

- Open questions: what pretraining objective (next-view prediction, scene-graph prediction, region-level 3D reasoning à la SpatialRGPT)? What task suite (shelf auditing, planogram compliance, item retrieval, navigation)? How much does synthetic retail pretraining transfer to real store footage?
- Evaluation anchors: SpatialRGBT-Bench-style 3D spatial cognition benchmarks, adapted to retail.
- *(Nov 2026: [Iris-Z](https://arxiv.org/abs/2611.16010) makes the bitter-lesson case for one generalist generative model over specialist geometry models — informs our FM's architecture; [Sophon](https://arxiv.org/abs/2611.14838) warns that benchmark scores can ride priors, so stripped-prior diagnostics belong in our eval; [SpaceMCP](https://arxiv.org/abs/2611.15680) offers a tool-based alternative — commodity VLM + spatial function server; [Physical AI Smart Spaces](https://arxiv.org/abs/2610.02580) provides the real multi-camera retail footage for the transfer test.)*

## Track E — Just-Walk-Out-style Retail Simulation

**Goal:** an end-to-end Amazon Just Walk Out-like environment: multi-camera store, shopper trajectories, synthetic sensor data for checkout-free retail perception research.

- Depends on Tracks A–C. Open questions: camera rig simulation, occlusion-heavy multi-person tracking data generation, and whether the sim supports training receipt-free checkout models.
- *(Nov 2026: [Physical AI Smart Spaces](https://arxiv.org/abs/2610.02580) is the first large-scale real multi-camera benchmark covering retail venues — 280+ h, ~1,800 cameras, 3D annotations — and the natural transfer test for our synthetic rig; [ShelfChange3D](https://arxiv.org/abs/2610.01283) defines the metric-3D change-detection task such a rig should train; [RetailLightNet](https://arxiv.org/abs/2610.35871) sketches the edge-deployment endgame for in-store analytics.)*

## Timeline anchor

Target venue: **ICCV 2027** (main paper submission deadline expected Sunday, March 7, 2027). CVPR 2027 (mid-November 2026) was deliberately skipped to avoid rushed submissions.