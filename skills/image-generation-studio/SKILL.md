---
name: image-generation-studio
description: "Professional studio asset renderer and e-commerce image generator. Zero text overlays, studio lighting, floor shadows, and isolated product rendering using Antigravity generate_image."
---

# 📸 Image Generation Studio — Commercial Product & Studio Asset Renderer

This skill provides an authoritative prompting framework for generating commercial e-commerce assets, product showcases, and marketing visuals with Antigravity's `generate_image` tool, ensuring **zero text glitches, studio-grade directional lighting, and hyper-realistic product separation**.

---

## 🚫 1. Zero Text in Generated Graphics

To eliminate garbled or illegible text rendering:
- **No Text in Prompts:** Never prompt image models to render brand names, button labels, price tags, or marketing slogans directly into pixels.
- **HTML/CSS Typography Layer:** All copy, prices, tags, and calls-to-action must be overlaid via semantic HTML and Tailwind CSS over the clean generated image.

---

## 💡 2. 8K Studio Lighting & Neutral Backdrop Baseline

Incorporate these core commercial photography keywords into production prompts:

```text
Professional 8K commercial product photography, isolated on clean neutral minimalist studio backdrop,
soft directional diffusion lighting, subtle contact floor drop-shadow (ambient occlusion),
sharp macro focus, Hasselblad medium format color grading, hyper-realistic, zero text, zero overlays.
```

---

## 📐 3. Aspect Ratio Standards

- **E-Commerce Product Cards:** `1:1` or `3:4`
- **Hero Banners & Feature Cards:** `16:9`
- **Mobile Stories & Vertical Banners:** `9:16`
- **Editorial & Blog Headers:** `3:2` or `4:3`
