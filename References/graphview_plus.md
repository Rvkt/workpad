---
type: reference
created: 2026-10-22
source_url: "https://pub.dev/packages/graphview_plus"
package: "graphview_plus"
version: "0.1.3"
domain: "flutter"
tags:
  - reference
  - flutter
  - graph
  - visualization
  - force-directed
---

# 🕸️ graphview_plus — Interactive Force-Directed Graph for Flutter

> [!resource] Package Blueprint & Metadata
> **Package:** `graphview_plus` `^0.1.3` · **Publisher:** `bangertstudio.kz` (Verified)
> **Platforms:** Android · iOS · macOS · Windows · Linux · Web · **License:** MIT
> **Pub Repository:** [pub.dev/packages/graphview_plus](https://pub.dev/packages/graphview_plus) · **GitHub:** [AlexHCJP/graphview_plus](https://github.com/AlexHCJP/graphview_plus)
> **Summary:** Interactive force-directed network graph widget for Flutter with d3-style cooling physics that settles without jitter, collision prevention (non-overlapping nodes), pan/zoom, node dragging, and an Obsidian-like reveal animation.

---

## 🎯 Key Architectural Features

1. **Settles, Then Sleeps (Zero Idle CPU)**:
   - Physics forces are multiplied by an `alpha` temperature parameter that decays to zero over ~300 frames.
   - Once settled, simulation halts rendering completely — no continuous jitter, battery drain, or CPU burn.
2. **Strict Non-Overlapping Collision Geometry**:
   - Integrated collision pass prevents circle overlap.
   - Hub nodes dynamically increase link/spoke length based on degree so leaf clusters fit cleanly.
3. **Smooth Canvas Interactivity**:
   - Native pan and pinch/wheel zoom support.
   - Interactive node drag (connected graph components react dynamically).
   - Hover highlighting and tap callbacks.
4. **Obsidian-Style Reveal Animation**:
   - Nodes pop into view one by one adjacent to visible neighbor nodes when the graph first renders or receives additions.
5. **Headless Core (`GraphSimulation<T>`)**:
   - Physics core is written in pure Dart with no Flutter widget dependencies, allowing offline unit testing and alternative renderers.
6. **Zero External Dependencies**:
   - Depends solely on Flutter framework primitives.

---

## 🛠️ Installation & Dependency Setup

Add to your Flutter project's `pubspec.yaml`:

```yaml
dependencies:
  flutter:
    sdk: flutter
  graphview_plus: ^0.1.3
```

Install via terminal:
```bash
flutter pub get
```

---

## 📖 Core Usage & Code Patterns

### 1. Initialize Controller with Generic Data Type
The type parameter carries your domain model or identifier:

```dart
import 'package:flutter/material.dart';
import 'package:graphview_plus/graphview_plus.dart';

final controller = GraphController<Task>();
```

### 2. Populate Nodes & Relationships
```dart
controller.setGraph(
  nodes: [
    for (final task in tasks)
      GraphNode<Task>(
        id: task.id,           // Stable unique identifier across layout updates
        label: task.title,     // Display label / circle text
        color: task.color,     // Custom node background tint
        data: task,            // Attached domain model
      ),
  ],
  links: [
    for (final rel in relations)
      GraphLink(rel.parentId, rel.childId),
  ],
);
```

### 3. Display GraphView Widget
```dart
GraphView<Task>(
  controller: controller,
  showLabels: true,
  initialScale: 1.0,
  minScale: 0.2,
  maxScale: 3.5,
  highlightColor: Theme.of(context).colorScheme.primary,
  edgeColor: Theme.of(context).colorScheme.outlineVariant,
  onNodeTap: (GraphNode<Task> node) {
    if (node.data != null) {
      openTaskDetails(node.data!);
    }
  },
)
```

### 4. Layout Tuning Parameters
```dart
controller
  ..repulsion = 1.2        // Range: 0.1 – 20.0 (Push force between nodes, default: 0.8)
  ..linkDistance = 180.0   // Rest length of link springs in canvas px (default: 150)
  ..linkStrength = 0.15    // Range: 0.0 – 0.3 (Spring stiffness)
  ..centerForce = 0.0003   // Range: 0.0 – 0.005 (Gravity pull toward origin)
  ..physicsEnabled = true; // Toggle false to freeze node positions
```

### 5. Mutating Graph without Disrupting Existing Layout
```dart
// Known nodes maintain their positions; newly added nodes animate in smoothly
controller.addNode(GraphNode(id: 'new_task', label: 'Telemetry Pipeline'));
controller.addLink(GraphLink('root_task', 'new_task'));

// Dynamic recoloring without reheating layout
controller.nodeById('new_task')?.color = Colors.teal;
controller.refresh();
```

---

## ⚙️ How the Physics Engine Operates (d3-force Mechanics)

- **Velocity Retention:** Velocities retain $60\%$ of their value each step (`velocityDecay: 0.4`).
- **Repulsion Falloff:** Many-body Coulomb repulsion scales as $1/d$ with a cutoff horizon of $2.5 \times \text{linkDistance}$ to prevent distant node clusters from distorting local hub leaves.
- **Centering Transformation:** The center of mass is aligned to the canvas origin via translation, preventing artificial graph squashing.
- **Pinned Dragging:** Dragging a node fixes its coordinates and reheats the simulation until gesture release.

---

## 🔗 Cross-Domain Connected Notes

- **Target Project:** [[Surfari Mobile Client|Surfari Mobile Client]] *(Candidate for interactive wave network & telemetry dependency visualizer)*
- **Engineering Learning:** [[Study MOC|Study MOC]] *(Dart/Flutter canvas graphics & state architecture)*
- **Knowledge Representation:** [[Knowledge MOC|Knowledge MOC]]
