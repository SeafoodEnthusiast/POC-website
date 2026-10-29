# GlaucoScan POC — AI Glaucoma Screening Web App (1:1 iOS Simulator)

A 1:1 web port of the **GlaucoScan iOS SwiftUI Proof-of-Concept** for glaucoma screening research. Runs **100% in the browser on Vercel** without requiring any external backend server, powered by **ONNX Runtime Web** (`models/GlaucomaSegmentation.onnx`, converted directly from `GlaucomaSegmentation.mlpackage`).

## Key Features

- **1:1 SwiftUI Mobile Simulator**:
  - **Desktop / Laptop / iPad**: Displays an interactive iPhone 16 Pro frame alongside a Clinical Demo Presenter Panel.
  - **Smartphone (iOS Safari / Android Chrome)**: Automatically adapts to a 100% fullscreen native mobile experience.
- **Complete Clinical Screening Flow**:
  1. **Onboarding**: Camera & Photos permission screens with interactive **NTAG213 NFC Frame** detection simulation.
  2. **Eye Scan (`Left Eye / OS` & `Right Eye / OD`)**: Live WebRTC camera preview with alignment target, 1x–4x zoom slider, photo library upload, and 1-click **Sample OS (`RET018OS.jpg`) / Sample OD (`RET018OD.jpg`)** clinical test buttons.
  3. **Photo Review**: Interactive pan, 1x–5x zoom, and square crop guide before running AI segmentation.
  4. **Report Overview**: Side-by-side Left & Right Eye structure scan cards with AI optic disc & cup contours, Vertical CDR (`vCDR`) calculation, risk classification (`Normal`, `Glaucoma Suspect`, `High Risk Glaucoma`), clinical finding summary, and recommended next steps.
  5. **Eye Details**: Segmented eye switcher (`Left eye` | `Right eye`), interactive visualization modes (`AI Contour`, `Filled Mask`, `Original`, `Schematic`), and pixel morphometrics.
  6. **High-Resolution JPG Report Export (`overview.jpg`)**: Generates the side-by-side annotated retinal overview with CDR values and AI disclaimer banner for immediate download.

## Project Structure

```text
POC-website/
├── index.html                        # 1:1 iOS Simulator + Clinical Presenter UI
├── styles.css                        # iOS SwiftUI Design System & Responsive Layout
├── app.js                            # ONNX Runtime Web Inference & SwiftUI View Logic
├── models/
│   └── GlaucomaSegmentation.onnx     # Converted ResNet34-UNet CoreML Model (512x512, 46.6 MB)
├── samples/
│   ├── RET018OS.jpg                  # Sample Left Eye (OS) Fundus Image (vCDR: 0.56 - Glaucoma Suspect)
│   ├── RET018OD.jpg                  # Sample Right Eye (OD) Fundus Image (vCDR: 0.45 - Normal)
│   └── reference_masks.json          # Pre-verified CoreML segmentation masks for instant demo
├── vercel.json                       # Vercel static hosting & caching configuration
└── package.json                      # Project metadata & local dev server script
```

## Running Locally

Run a local HTTP server from the project root:

```bash
python3 -m http.server 3000
```

Then open **http://localhost:3000** in your browser.

## Deploying to Vercel

1. Push this repository to GitHub (or use the Vercel CLI `npx vercel`).
2. Import the repository at [vercel.com/new](https://vercel.com/new).
3. Leave the **Framework Preset** as **Other** (root directory `./`) and click **Deploy**.
