# Human Anatomy 3D & Live X-Ray AR Atlas

A high-performance, clinical-grade 3D Human Anatomy Atlas and Live Augmented Reality X-Ray Spatial Mirror built with Three.js, WebGL, and MediaPipe AI computer vision.

![Human Anatomy 3D and X-Ray Scanner](assets/xray-animated-preview.svg)

---

## 1. System Overview & Dual-Engine Architecture

The application is structured into a unified launcher hub (`index.html`) connecting two specialized clinical visualization engines without mutual code interference:

### Portal Launcher (`index.html`)
- Responsive medical portal with card selection and collapsible technical specifications.
- Instant routing between Craniofacial V1 and Full-Body V2.

### Engine A: Craniofacial, Dentomaxillofacial & Neuroanatomy Studio (`head_v1.html`)
- **49 Anatomical Structures:** Cranial vault (Frontal, Parietal, Temporal, Occipital, Sphenoid, Ethmoid), articulated Mandible with physiological TMJ condylar kinematics, full adult dentition (FDI dental arches), muscles of mastication (Masseter, Temporalis), and 8 cerebral/brainstem divisions.
- **Micro-Tracking Kinematics:** 478-point MediaPipe Face Landmarker with 6-DOF facial transformation matrix and dynamic real-time jaw articulation telemetry ($0.0^\circ$ to $18.0^\circ$).
- **20-Bone Hand Skeletal Kinematics:** Two independent 20-bone hand instances (Carpals, Metacarpals 1–5, Phalanges) tracked 1:1 via MediaPipe Hand Landmarker.
- **Interactive Hand Lens:** Optical X-ray magnifier reticle slaved to 3D index fingertip coordinates with high-DPI framebuffer scaling.
- **Refined Studio Framing:** Default viewing distance calibrated to 65 units for complete pedestal clearance and anatomical label legibility.

### Engine B: Full-Body Systemic AR Atlas (`fullbody.html`)
- **350 Anatomical Structures:** Comprehensive systemic dataset including:
  - **Osteology:** Complete human skeleton (196 individual bones).
  - **Myology:** Axial and appendicular musculature (105 muscle groups).
  - **Splanchnology:** 21 internal organs (Heart, Lungs, Liver, Kidneys, Spleen, Stomach, Intestines).
  - **Integumentary:** Volumetric human skin surface.
  - **Neuroanatomy:** Complete cerebral lobes, cerebellum, and brainstem.
- **15-Segment Kinematic Solver:** Driven by 33 MediaPipe 3D Pose World Landmarks across 15 anatomical segments (Pelvis root, Torso, Head, Upper Arms, Forearms, Hands, Thighs, Shanks, Feet).
- **Dual-Light Blinn-Phong Shader:** Specular highlight modeling for muscle fascial sheaths and cortical bone contours.
- **Hands-Free Air Interaction Engine:** Touchless air-cursor and gestural dissection controls designed for distance camera use.

---

## 2. Hands-Free Air Interaction Engine

Because users stand 2 to 3 meters away from the webcam for full-body tracking, physical mouse and touchscreen input is unavailable. `fullbody.html` includes an integrated hands-free interaction pipeline:

1. **Air Cursor & Dwell Selection:**
   - Detects the index fingertip landmark (`landmark 8`) on the primary tracked hand.
   - Applies an exponential moving average (EMA) filter to eradicate jitter while maintaining responsive tracking.
   - Hovering the air reticle over any UI button, chip, or system toggle for 750 ms triggers a dwell click with a circular progress countdown ring.
2. **Stratified Dissection Gestures:**
   - Tracks thumb-to-index distance normalized against palm length.
   - **Left-Hand Pinch:** Peels back anatomical layers sequentially:
     $$\text{Surface \& Skin} \longrightarrow \text{Musculature \& Viscera} \longrightarrow \text{Visceral Organs} \longrightarrow \text{Skeletal System}$$
   - **Right-Hand Pinch:** Reconstructs and restores layers in reverse order.
   - 550 ms refractory cooldown eliminates accidental double triggers.
3. **On-Screen Telemetry & Air Toggle:**
   - Real-time frosted glass status notifications (`#air-toast`).
   - Air Gesture toggle button (`#airb`) in the bottom dock allowing one-click activation or deactivation.

---

## 3. MediaPipe Calibration Architecture & Bug Resolution

### The Calibration Bug in Reference V2
In the initial full-body tracking prototype, user calibration (`calSample()`) frequently caused limbs to twist unnaturally or invert depth by $180^\circ$. Root causes resolved in `fullbody.html`:
1. **Dynamic $Z$-Sign Desync:** Live correlation flipped $z\text{Sign}$ dynamically, causing live frames to apply inverted depth against recorded calibration offsets. Resolved by strictly locking coordinate conventions once calibration completes.
2. **Local vs. World Rotation Space:** Corrected rotation matrix composition from local bone space (`Qt[k].multiply`) to camera/world coordinate pre-multiplication (`Qt[k].premultiply`).
3. **Shortest-Path Quaternion Slerp:** Corrected quaternion sign flipping (`dot < 0`) during bone orientation interpolation.
4. **Sample Threshold:** Increased calibration stabilization threshold to ensure noise-free landmark averaging before locking offsets.

---

## 4. Medical Educational Color Specification

Standardized medical color specification modeled after classical anatomical atlases (Netter, Sobotta):

| Anatomical System | Clinical Color | Hex Code | RGB (Normalized) | Visual Quality |
|---|---|---|---|---|
| **Osteology (Bones)** | Calcified Natural Ivory | `#E8E2CE` | `[0.91, 0.88, 0.81]` | Warm cortical bone with subtle osteoid patina |
| **Dentition (Teeth)** | Enamel Pearl White | `#F5F5F0` | `[0.96, 0.96, 0.94]` | Natural semi-translucent dental enamel |
| **Myology (Musculature)** | Striated Myofibril Red | `#9E3A33` | `[0.62, 0.23, 0.20]` | Anatomical striated muscle with fiber sheen |
| **Viscera: Heart** | Myocardial Crimson | `#8B1E22` | `[0.55, 0.12, 0.13]` | Dense vascularized muscular organ |
| **Viscera: Lungs** | Aerated Pleural Rose | `#C48B92` | `[0.77, 0.55, 0.57]` | Light, vascular spongy tissue |
| **Viscera: Liver** | Hepatic Russet | `#783024` | `[0.47, 0.19, 0.14]` | Deep vascular parenchyma |
| **Viscera: Kidneys** | Renal Bean Brown | `#6E2D26` | `[0.43, 0.18, 0.15]` | Dense cortical tissue |
| **Viscera: Digestive** | Visceral Buff / Ochre | `#C4A47C` | `[0.77, 0.64, 0.49]` | Peritoneal membrane and smooth muscle |
| **Integumentary (Skin)** | Translucent Dermal Buff | `#E2B89B` | `[0.89, 0.72, 0.61]` | Subsurface dermal layer |
| **Neuro: Frontal Lobe** | Executive Mauve | `#8E5B78` | `[0.56, 0.36, 0.47]` | Muted educational distinction |
| **Neuro: Parietal Lobe** | Somatosensory Slate Blue | `#5A6B8A` | `[0.35, 0.42, 0.54]` | Muted educational distinction |
| **Neuro: Temporal Lobe** | Auditory Teal | `#457B7B` | `[0.27, 0.48, 0.48]` | Muted educational distinction |
| **Neuro: Occipital Lobe** | Visual Warm Amber | `#8A6B48` | `[0.54, 0.42, 0.28]` | Muted educational distinction |
| **Neuro: Cerebellum** | Coordination Indigo | `#4B6B8A` | `[0.29, 0.42, 0.54]` | Muted educational distinction |
| **Neuro: Brainstem** | Autonomic Ochre | `#855F45` | `[0.52, 0.37, 0.27]` | Muted educational distinction |

---

## 5. PWA Caching Strategy

The Progressive Web App service worker (`sw.js`) and manifest (`manifest.json`) implement a hybrid caching architecture:

- **Application Shell & Code (Network-First):** HTML, CSS, and app scripts are fetched from the network first with immediate cache fallback. Connected users always receive the newest code without stale cache struggles.
- **Heavy MediaPipe Models & WebAssembly (Cache-First):** Model weights (`.task`) and WebAssembly runtime files (`.wasm`) from Google Cloud Storage and jsDelivr are permanently cached in `anatomy-models-v1`. Once downloaded, model startup is instantaneous and works fully offline.

---

## 6. Quick Start & Local Run

Serve the repository directory over HTTP (required for camera and WebRTC access):

```bash
# Python 3 local server:
python -m http.server 8080

# Access via browser:
# http://localhost:8080/index.html
```

---

## 7. License
MIT License. Open-source educational resource for medical students, dental surgeons, anatomical researchers, and digital health developers worldwide.
