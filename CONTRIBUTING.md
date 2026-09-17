# Contributing to Awesome Retail Vision

A curated list of research ideas, papers, datasets and tools for **retail vision and embodied retail AI** — with a focus on building virtual retail worlds (photorealistic SKUs, shelves, stores) and training spatial foundation models in them.

## How to contribute

1. **Open an issue first** for new papers, datasets, tools or project ideas, using one of the templates below. This keeps the list curated instead of a link dump.
2. **One PR per topic area.** Keep edits minimal and consistent with the existing formatting.
3. **Verify links.** Every entry must have a working link (arXiv, GitHub, project page, or DOI). The repo runs a weekly link check; broken entries get flagged.
4. **Add one line on why it matters for retail.** A paper is only listed if the connection to retail vision / virtual retail worlds is stated.

## Entry format

```markdown
- [Name](https://link) — one-line description. *Why retail:* <reason>. `tag1` `tag2`
```

- Use the paper's official title (check the arXiv page or project page).
- arXiv links preferred over blog summaries; GitHub links preferred over forks.
- Tags come from the fixed vocabulary below.

## Tag vocabulary

| Tag | Meaning |
|---|---|
| `sku-3d` | SKU/product-level 3D assets and textures |
| `texture` | Texture generation, super-resolution, PBR materials |
| `3dgs` | 3D Gaussian splatting and related representations |
| `scene-gen` | Store/scene/environment generation |
| `world-model` | Generative world models, interactive environments |
| `spatial-fm` | Spatial foundation models, 3D-aware VLMs |
| `embodied` | Embodied agents, benchmarks, sim2real |
| `human-avatar` | Humanoids, digital humans, avatars in retail |
| `dataset` | Datasets and asset libraries |
| `tooling` | Software, pipelines, capture tools |

## What belongs here

- Papers on 3D asset generation, texture synthesis, virtual try-on/off, scene/world generation, spatial reasoning, embodied retail agents and benchmarks.
- Datasets of products, garments, retail scenes, or 3D assets usable for retail simulation.
- Tools and pipelines for scanning, reconstructing, or generating retail content.
- Open research questions and project ideas (see `README.md` → Research Tracks).

## What does not belong

- Generic e-commerce/recommender papers with no vision or 3D component.
- Dead projects without a public artifact.
- Preprints with no code, no project page, and no results (state clearly if unreviewed).

## Project ideas

If you are proposing a **research direction** rather than a paper, open an issue titled `IDEA: <short name>` describing: the goal, the closest existing work, the expected contribution, and a rough feasibility note. Accepted ideas are added to the Research Tracks section of the README with credit.

## Attribution

Ideas seeded by the Ubiquitous Retail Group (UCL) × UP Diliman Ubiquitous Computing Lab collaboration on Sari Sandbox. Supervised by Dr. Rowel Atienza.