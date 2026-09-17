# Research Tracks

Long-horizon research directions for the group, ordered from near-term (SKU assets) to the overarching goal (spatial foundation models trained in virtual retail worlds). Each track lists the open questions we want answers to — pick one and open an `IDEA:` issue.

## Track A — SKU Digitization: Texture → 3D → Texture

**Goal:** near-1:1 3D replicas of real SKUs (barcode, nutrition facts, label typography intact) that can populate shelves at scale.

- **Texture acquisition without buying every product.** The first Sari Sandbox group bought originals and scanned them on a lab scanner; scraped photos are only average quality. Open questions: can GarmentZoom-style reference-based super-resolution lift scraped product photos to texture-grade quality? Can close-up references be sourced cheaply (manufacturer sites, packaging PDFs, user photos)?
- **Reference assets in-repo:** [`images/`](images/) holds two wrap-around label scans — [555 Tuna Afritada 155g](images/555_TUNA_AFRITADA_155G.jpg) (8192×3618) and [Zesto Root Beer 500ml](images/ZESTO_ROOT_BEER_500ML_LABEL.jpg) (4000×1579) — as the concrete target format: flat label art that texture→3D must wrap onto can/bottle geometry, with barcode and nutrition facts surviving the round trip.
- **Texture → 3D:** generate a complete, correctly-proportioned 3D SKU from flat packaging art + a few reference photos. Open questions: how to enforce box/can/bottle priors so generated geometry is shelf-ready; how to keep printed text legible (barcodes, nutrition panels) through the generation pipeline.
- **3D → texture (re-texturing):** re-skin an existing 3D SKU with new packaging art — the retail analogue of virtual try-on, and the easier direction (cf. try-off being more learnable than try-on in Voost). Open questions: UV-free texture representations (HKTex) vs UV atlases for boxy packaging; editing consistency across the 6 faces of a carton.
- **Evaluation:** how do we measure "1:1-ness" of a generated SKU? Barcode decodability, OCR of nutrition facts, texture fidelity vs scanner ground truth.

## Track B — Store and Scene Generation

**Goal:** procedural, photorealistic store interiors (shelves, fridges, checkout) that accept arbitrary SKU sets.

- Claimed to be easier than SKU digitization once assets exist — but open questions remain: physically plausible shelf packing (planogram-aware placement), lighting variation across store zones, and layout diversity for training-time world variety.
- Candidate approach: start from the Sari Sandbox store builder, automate planogram generation, and render with the same asset pipeline as Track A.

## Track C — Human Clones in the Store

**Goal:** controllable digital humans that shop, restock, and checkout inside the generated stores.

- Open questions: identity-preserving avatars from a single photo/video; garment handling on articulated bodies (virtual try-on applied to 3D avatars, not flat images); plausible shopping behaviors (trajectories, dwell times, grasp poses) for data generation.
- This is the least-explored track and likely the highest-risk one — treat as a stretch goal behind Tracks A/B.

## Track D — Spatial Foundation Models in Retail Worlds

**Goal:** the overarching goal. Use many generated store "worlds" to train spatial foundation models — the group's differentiator vs Amazon's retail-world-model focus.

- Open questions: what pretraining objective (next-view prediction, scene-graph prediction, region-level 3D reasoning à la SpatialRGPT)? What task suite (shelf auditing, planogram compliance, item retrieval, navigation)? How much does synthetic retail pretraining transfer to real store footage?
- Evaluation anchors: SpatialRGBT-Bench-style 3D spatial cognition benchmarks, adapted to retail.

## Track E — Just-Walk-Out-style Retail Simulation

**Goal:** an end-to-end Amazon Just Walk Out-like environment: multi-camera store, shopper trajectories, synthetic sensor data for checkout-free retail perception research.

- Depends on Tracks A–C. Open questions: camera rig simulation, occlusion-heavy multi-person tracking data generation, and whether the sim supports training receipt-free checkout models.

## Timeline anchor

Target venue: **ICCV 2027** (main paper submission deadline expected Sunday, March 7, 2027). CVPR 2027 (mid-November 2026) was deliberately skipped to avoid rushed submissions.