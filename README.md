# Human Anatomy 3D & X-Ray AR Atlas

A high-performance, browser-based 3D Human Anatomy Atlas and Live Radiographic X-Ray Augmented Reality explorer designed for medical, dental, and neuroanatomy education.

---

## 🌟 Clinical & Educational Capabilities

### 1. Dentomaxillofacial & Cranial Osteology
- **Mandible & Maxilla:** Complete visualization of mandibular condyles, coronoid processes, alveolar margins, mental foramina, and the inferior alveolar neurovascular canal.
- **Maxillary & Mandibular Dentition:** Modeled adult dentition including central/lateral incisors, canines, premolars, and molars with root canal anchors and occlusion analysis (Angle's Class I, II, III).
- **Cranial Vault & Base:** Frontal, Parietal, Temporal (mandibular fossa / TMJ glenoid cavity), Occipital (foramen magnum, condyles), Sphenoid (pterygoid plates, sella turcica), and Ethmoid bones.

### 2. Muscles of Mastication & Facial Expression
- **Masticatory Apparatus:** Masseter (superficial and deep heads) and Temporalis with vector orientations, generating crushing bite forces (>700 N) and retractive grinding dynamics.
- **Facial Architecture:** Buccinator ("trumpeter's muscle"), Orbicularis Oris, Orbicularis Oculi, Zygomaticus, and Frontalis with distinct motor/sensory cranial nerve mappings (CN V3 vs CN VII).

### 3. Neuroanatomy & Brainstem Centers
- **Cerebral Cortex:** Frontal lobe (primary motor cortex M1, Broca's area), Parietal lobe (somatosensory homunculus S1), Temporal lobe (primary auditory A1, Wernicke's area, hippocampus), and Occipital lobe (calcarine visual cortex V1).
- **Subcortical & Brainstem:** Internal capsule / cerebral white matter projection tracts, Cerebellum, Pons (pontine respiratory group, cranial nerve nuclei V-VIII), and Medulla Oblongata (cardiovascular & autonomic respiratory reflex centers).

### 4. Hand Osteology & Kinematic Tracking
- Complete 27-bone hand skeletal framework: Carpus (8 carpal bones), Metacarpals 1–5, and Proximal, Middle, and Distal Phalanges mapped 1:1 with real-time MediaPipe hand landmark tracking.

---

## 🔬 Core Technical Features

- **Dual Shader Rendering:**
  - **Radiographic X-Ray:** Custom GLSL fragment shader simulating depth-independent volumetric Fresnel glow with exposure control. Automatically switches to a deep radiographic dark slate theme (`#060b13`) for optimal contrast.
  - **Solid Diagnostic PBR:** Calibrated studio lighting with physically-based shading on a clean clinical studio backdrop.
- **Planar Section Slicing:**
  - Real-time GPU clipping plane (`uPlane`, `uClip`) allowing seamless cross-sectional slicing through the mandible, teeth roots, maxillary sinus, and cerebral hemispheres in both 3D Studio and Live AR modes.
- **Live AR Radiograph & TMJ Telemetry:**
  - Zero-zoom optical fit using WebRTC camera stream with automatic mirroring calibration (front-facing camera mirrors, environment camera does not).
  - Dynamic TMJ condylar articulation telemetry chip calculating real-time mandibular displacement degrees (`TMJ: 0.0°`).
- **Interactive Clinical Search & Detail Engine:**
  - Autocomplete search with categorical tagging (`Dentomaxillofacial`, `Neuroanatomy`, `Mastication / Facial`, `Digital Osteology`).
  - Frosted clinical detail card featuring Latin anatomical terminology, structural landmarks, innervation, blood supply, and high-yield notes.
  - One-click **Focus 3D** (re-centers camera orbit) and **Isolate / Solo** (dims non-selected structures).
- **Universal Device Optimization:**
  - Responsive layout verified across ultra-compact mobile viewports (360px–375px) and 4K desktop workstations.
  - Zero-latency GPU-accelerated rendering using Three.js and WebGL.

---

## 🚀 Quick Start

Open `index.html` directly in any modern WebGL-compatible browser:

```bash
# Using Python local server (recommended for camera permissions):
python -m http.server 8080

# Or open directly in Chrome, Edge, Safari, or Firefox:
# Navigate to http://localhost:8080/index.html
```

### Keyboard Shortcuts
- `/` : Focus search input
- `Esc` : Close detail card / clear search
- `Space` : Reset camera view

---

## 🛠️ Technology Stack
- **Rendering:** Three.js (r160), WebGL, Custom GLSL Shaders
- **Computer Vision:** MediaPipe Face & Hand Landmarker Tasks
- **Styling:** Vanilla CSS3 with Spatial Frosted Glassmorphism
- **Data:** BodyParts3D FMA compliant anatomical dataset

---

## 📄 License
MIT License. Open-source for medical students, dental surgeons, and anatomical researchers worldwide.
