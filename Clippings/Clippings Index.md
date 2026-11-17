---
type: moc
title: "Web Clippings Hub"
created: 2026-10-22
tags:
  - moc
  - clippings
---

# 📑 Web Clippings Hub

> [!info] Graph Nexus · Web Clippings
> **Central Knowledge Bridge** connecting web articles, documentation clips, and browser captures into the second brain graph.
> **Navigation:** [[00 Home/Home|🏠 Home Dashboard]] · [[05 Knowledge/Maps of Content/Knowledge MOC|🧠 Knowledge MOC]] · [[06 Resources/References/graphview_plus|📦 graphview_plus]]

---

## 🧭 Curated Clipping Clusters

### ⚡ React Native & Mobile Performance
- [[Optimizing React Native Performance A Developer's Guide]] — Production optimization techniques, memoization boundaries, and custom hook overhead.
- [[Performance Overview · React Native]] — JS thread vs UI main thread frame rates, 60 FPS target, and bridge batching.
- [[06 Resources/Articles/react-native-toast-message|react-native-toast-message]] — Lightweight imperative toast message component for mobile apps.
- *Connected Project:* [[04 Projects & Goals/Projects/DroidLens|DroidLens]] · [[05 Knowledge/Study/Flutter & Dart|Mobile Engineering]]

### 🌊 Oceanography, Wind & Weather
- [[06 Resources/Articles/Weather|Weather (Storm Glass API)]] — Programmatic global weather coordinate data endpoint.
- [[06 Resources/Articles/onshore offshore, cross, explain these. related to surfing|Onshore vs Offshore Wind in Surfing]] — Wind mechanics, surf conditions, wave steepness, and swell impact.
- *Connected Project:* [[04 Projects & Goals/Projects/Surfari Mobile Client|Surfari Mobile Client]]

### 🎨 UI/UX, Design & Accessibility
- [[06 Resources/Articles/Web Accessibility Color Contrast Checker - Meet WCAG Conformance|Web Accessibility Color Contrast Checker]] — WCAG A, AA, and AAA conformance scanning and ratio validation.

---

## 📊 All Web Clippings (Dynamic Index)

```dataview
TABLE source AS "Source URL", author AS "Author", created AS "Clipped Date"
FROM #clippings OR "Clippings" OR "06 Resources/Articles"
WHERE file.name != "Clippings"
SORT created DESC
```

---

## ⚙️ Obsidian Web Clipper Setup Guide

To ensure all new browser captures automatically connect to this hub and support prefix digits:

1. **Folder / Location with Prefix Digits**:
   - In the Web Clipper extension options, set **Note location (Folder)** to:
     `Clippings` (or `06 Resources/Clippings`).
   - Prefix digits and nested folders are 100% supported!
2. **Note Name with Prefix Digits**:
   - You can add date/time prefixes to filenames: `{{date:YYYY-MM-DD}} - {{title}}`.
3. **Automatic Graph Connectivity**:
   - In your Web Clipper template, include `> 🔗 **Clipping Hub:** [[Clippings]]` at the top of the body, or `hub: "[[Clippings]]"` in properties.
