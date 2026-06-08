# Design System Specification: Travel Journal App ("Scrapbook Minimal")

This document serves as the absolute source of truth for the visual style, layout principles, and component behavior of the Travel Journal application. All generated code must strictly adhere to these aesthetic guidelines.

## 1. Aesthetic Narrative
The interface blends **premium, minimalist digital layouts** with **tactile, physical scrapbook elements (skeuomorphism)**. It should feel clean and spacious, yet playful, warm, and highly personalized. Think luxury editorial meets a personal polaroid diary.

---

## 2. Color Palette & Surface Hierarchy

The app relies on soft, low-contrast backgrounds to let white physical elements and vibrant photos "pop."

| Layer | Type | Tailwind / Hex Code | Visual Intent |
| :--- | :--- | :--- | :--- |
| **Canvas Background** | Base | `bg-[#F0F1F3]` | Soft, muted neutral light gray. Feels like a premium matte paper surface. |
| **Containers / Cards** | Surface | `bg-white` | Pure crisp white. Represents physical cards or paper folders dropped onto the canvas. |
| **Primary Typography** | Text | `text-gray-900` | High legibility, dark charcoal (not pure black). |
| **Secondary Typography** | Text | `text-gray-400` / `text-gray-500` | Muted metadata, place counts, and dates. |
| **Accent Sticker (Blue)** | Detail | `bg-[#A2D2DF]` | Used for taped elements, sticky notes, or highlight backdrops. |
| **Accent Sticker (Yellow)**| Detail | `bg-[#FCD34D]` | Used for sun/travel decorative labels. |

---

## 3. Elevation, Borders & Geometry

To achieve the soft, touchable "neumorphic-adjacent" feel, follow these strict geometric rules:

* **Extreme Rounding:** Main dashboard containers and folders must use `rounded-3xl` (24px) or `rounded-[2rem]` (32px). Sharp corners are strictly prohibited.
* **Ambient Shadows:** Shadows must be incredibly soft, diffuse, and low-opacity to mimic real paper on a table. 
  * *Tailwind implementation:* `shadow-[0_8px_30px_rgb(0,0,0,0.04)]` or a layered `shadow-sm`. Never use harsh, dark shadows.
* **Rotation Quirks:** Scrapbook elements (polaroids, sticky notes, badges) should feature micro-rotations between `-2deg` and `2deg` (`rotate-1`, `rotate-[-2]`) to look hand-placed.

---

## 4. Typography

* **Headers & Interface UI:** Bold, highly structured, clean sans-serif (e.g., system font stack or Inter). `font-bold tracking-tight text-gray-900`.
* **Editorial & Notes:** A handwritten, organic script font (e.g., Google Fonts 'Caveat' or 'Architects Daughter') for sticky note commentary, sticker labels, and captions.

---

## 5. Core Component Specifications

### A. The Travel Folder Card (Dashboard Grid)
* **Structure:** A vertical `bg-white` card with `rounded-[2rem]` and `p-5`.
* **Top Asset Stack:** An absolute-positioned, layered stack of 2-3 images tilted at contrasting angles, mimicking photos peeking out of a physical folder file.
* **Details Layout:** A horizontal row at the bottom containing a flat country emoji/flag asset on the left, and an absolute-positioned "postage stamp" or "clipped label" graphic on the right.
* **Collaborator Avatars:** Clean circular images overlapping each other (`-space-x-2`).

### B. The Polaroid Component (Inner View)
* **Structure:** A crisp white frame (`bg-white p-3 pb-12 shadow-md`) housing an aspect-ratio accurate photo.
* **Skeuomorphic Attachments:** Must feature a decorative overlay asset, such as a semi-transparent "clear tape" strip at the top center, or a "paperclip" holding a pastel-colored sticky note to the border.

### C. The Jagged "Ripped Paper" Collage
* **Structure:** Photo grids or headers that don't have straight lines. Uses custom SVG `clip-path` masks to create a jagged, torn-edge scrapbook effect.
* **Sticker Accents:** Overlaid cartoonish, bold-outline vector stickers (cameras, airplanes, sunglasses) and high-expression emojis dropped casually over image corners.

### D. Floating Interaction Docks
* **Structure:** Pill-shaped navigation bars (`rounded-full`) floating explicitly above the canvas with a strong ambient shadow.
* **States:** Active items use a solid black capsule background (`bg-gray-900 text-white rounded-full px-4 py-2`) contrasting against the bare icons of inactive states.

## 6. Color Palette: Dark Mode Overrides

When dark mode is active (`.dark` class applied), the system shifts to a "Midnight Journal" theme, mimicking dark metallic foil and black cardstock.

| Layer | Light Mode | Dark Mode (Hex) | Visual Intent |
| :--- | :--- | :--- | :--- |
| **Canvas Background** | `bg-[#F0F1F3]` | `bg-[#121315]` | Deep, matte charcoal canvas. |
| **Containers / Cards**| `bg-white` | `bg-[#1A1B1E]` | Rich slate-black cardstock with a fine border. |
| **Primary Text** | `text-gray-900` | `text-[#E4E6EB]` | Off-white high legibility text. |
| **Secondary Text** | `text-gray-500` | `text-[#A0A5B1]` | Muted silver-gray metadata. |
| **Folder Accents** | Soft shadows | `border border-white/[0.05]` | Subtle inner glints instead of heavy shadows. |

---

## 7. Motion & Screen Transitions

To make the app feel like a premium native mobile application, layout animations must feel physical and elastic. Use `framer-motion` with spring physics instead of rigid linear timings.

* **Page Transitions:** When switching between the Dashboard and a Trip View, the entire page should softly slide up from the bottom and fade in simultaneously.
  * *Spring Setting:* `type: "spring", stiffness: 100, damping: 20`
* **Shared Layout (Folder Expansion):** When a user taps a travel folder card, the card should morph smoothly into the main header of the detailed page view using a shared layout ID.
* **Micro-interactions:** * **Buttons/Docks:** Micro-scale down on tap (`whileTap={{ scale: 0.95 }}`) and scale up slightly on hover.
  * **Polaroids:** Tapping a photo inside a journal should gently scale it up and straighten its rotation (`rotate: 0`) to bring it to focus, mimicking picking a photo up off a desk.
