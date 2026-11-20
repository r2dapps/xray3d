# Human Anatomy 3D and X-Ray AR Atlas

A high-performance, browser-based 3D Human Anatomy Atlas and Live Radiographic X-Ray Augmented Reality explorer designed for medical, dental, and neuroanatomy education.

![Human Anatomy 3D and X-Ray Scanner](assets/xray-animated-preview.svg)

---

## Clinical and Educational Architecture

### 1. Dentomaxillofacial and Cranial Osteology
- **Mandible and Maxilla:** Detailed spatial visualization of mandibular condyles, coronoid processes, alveolar margins, mental foramina, and the inferior alveolar neurovascular canal.
- **Maxillary and Mandibular Dentition:** Modeled adult dentition including central/lateral incisors, canines, premolars, and molars with root canal anchors and occlusion analysis (Angle Class I, II, III).
- **Dedicated Dental Occlusion View:** Instant one-click occlusal alignment preset ("D") centering directly onto the mandibular and maxillary dental arches and alveolar plane.
- **Cranial Vault and Base:** Frontal, Parietal, Temporal (mandibular fossa and TMJ glenoid cavity), Occipital (foramen magnum, condyles), Sphenoid (pterygoid plates, sella turcica), and Ethmoid bones.

### 2. Muscles of Mastication and Facial Expression
- **Masticatory Apparatus:** Masseter (superficial and deep heads) and Temporalis with vector orientations, generating crushing bite forces (>700 N) and retractive grinding dynamics.
- **Facial Architecture:** Buccinator, Orbicularis Oris, Orbicularis Oculi, Zygomaticus, and Frontalis with distinct motor/sensory cranial nerve mappings (CN V3 vs CN VII).

### 3. Neuroanatomy and Brainstem Centers
- **Cerebral Cortex:** Frontal lobe (primary motor cortex M1, Broca's area), Parietal lobe (somatosensory homunculus S1), Temporal lobe (primary auditory A1, Wernicke's area, hippocampus), and Occipital lobe (calcarine visual cortex V1).
- **Subcortical and Brainstem:** Internal capsule and cerebral white matter projection tracts, Cerebellum, Pons (pontine respiratory group, cranial nerve nuclei V-VIII), and Medulla Oblongata (cardiovascular and autonomic respiratory reflex centers).

### 4. Hand Osteology and Kinematic Tracking
- Complete 27-bone hand skeletal framework: Carpus (8 carpal bones), Metacarpals 1 through 5, and Proximal, Middle, and Distal Phalanges mapped 1:1 with real-time MediaPipe hand landmark tracking.

---

## Core Technical Features

- **Dual Shader Rendering Pipeline:**
  - **Radiographic X-Ray:** Custom GLSL fragment shader simulating depth-independent volumetric Fresnel glow with exposure control. Automatically switches to a deep radiographic dark slate theme (`#060b13`) for optimal contrast and authentic radiographic appearance.
  - **Solid Diagnostic PBR:** Calibrated studio lighting with physically-based shading on a clean clinical studio backdrop.
- **Planar Section Slicing:**
  - Real-time GPU clipping plane (`uPlane`, `uClip`) allowing seamless cross-sectional slicing through the mandible, tooth roots, maxillary sinus, and cerebral hemispheres in both 3D Studio and Live AR modes.
- **Live AR Radiograph and TMJ Telemetry:**
  - Optical zero-zoom fitting using WebRTC camera stream with automatic mirroring calibration (front-facing camera mirrors, environment camera does not).
  - Dynamic TMJ condylar articulation telemetry calculating real-time mandibular displacement degrees (`TMJ: 0.0 deg`).
- **Interactive Clinical Search and Minimizable Detail Card:**
  - Autocomplete search with categorical tagging (Dentomaxillofacial, Neuroanatomy, Mastication, Digital Osteology).
  - Frosted clinical detail card featuring Latin anatomical terminology, structural landmarks, innervation, blood supply, and high-yield notes.
  - **Mobile Minimizable Architecture:** Detail card and systems panels can be collapsed into compact, non-intrusive status pills with a single tap, preserving an unobstructed 3D view for mobile device interaction.
  - One-click **Focus 3D** (re-centers camera orbit) and **Isolate / Solo** (dims non-selected structures).
- **Universal Viewport Optimization:**
  - Calibrated for both desktop workstations and compact mobile viewports (down to 360px width) with adaptive camera field-of-view scaling.
  - Zero-latency GPU-accelerated rendering using Three.js and WebGL.

---

## Quick Start

Open `index.html` directly in any modern WebGL-compatible browser:

```bash
# Using Python local server (recommended for camera and WebRTC permissions):
python -m http.server 8080

# Or open directly in Chrome, Edge, Safari, or Firefox:
# Navigate to http://localhost:8080/index.html
```

### Keyboard Shortcuts
- `/` : Focus search input
- `Esc` : Close detail card or clear search
- `Space` : Reset camera view

---

## Technology Stack
- **Rendering:** Three.js (r160), WebGL, Custom GLSL Shaders
- **Computer Vision:** MediaPipe Face and Hand Landmarker Tasks
- **Styling:** Vanilla CSS3 with Spatial Frosted Glassmorphism
- **Data:** BodyParts3D FMA compliant anatomical dataset

---

## License
MIT License. Open-source for medical students, dental surgeons, and anatomical researchers worldwide.
