Darshan Cement AI:-

AI-assisted hole & crack measurement, cement estimation, and repair reporting — from a single site photo.
Darshan Cement AI helps engineers, contractors, and site workers measure empty holes, potholes, or damaged patches using just a smartphone, then instantly calculates how much cement, sand, and aggregate is needed to fill them — with a downloadable PDF report.
This build is a single self-contained HTML file (index.html). No install, no server, no build step — open it in any modern browser (desktop or mobile) and it works.

# Features
Core workflow
Capture or upload a photo (mobile camera or file upload/drag-drop)
Manual entry mode — no photo? Type in length/width/diameter/area directly and skip straight to the cement calculation
AI-style hole detection — client-side computer-vision pipeline (grayscale → adaptive threshold → connected-component flood fill → contour tracing → polygon simplification) automatically outlines the hole; a manual point-and-click tracer is available as a fallback
Reference-object calibration — tap two points on a known-size object (A4 sheet, coin, steel scale, or custom length) to convert pixels into real-world centimeters
Depth entry → automatic volume calculation
Concrete mix selection — M10 through M30, using standard dry-volume (1.54×) correction
Material & cost estimate — cement (bags/kg), sand (cu.ft/kg), aggregate (cu.ft/kg), and total cost with editable material prices
Repair report dashboard — annotated image, measurement cards, material bar chart, priority badge (Low/Medium/High), estimated repair time, and AI-style recommendations

#Extras

📄PDF export — multi-page, page-aware report generation (via jsPDF)

💾 History — reports are saved locally (per-user persistent storage) with thumbnails, searchable and filterable by priority

📍 GPS tagging — attach coordinates to a report

🔊 Voice read-back — reads the report summary aloud (Web Speech API)

🌗 Dark / light theme toggle

🌐 EN / HI language toggle for key labels

📱 Fully responsive — works on phone, tablet, and desktop

🚀 Getting started

Download index.html
Open it directly in any modern browser (Chrome, Safari, Edge, Firefox) — double-click, or drag it into a browser window
On mobile, use Use Camera to photograph the hole, or Upload Image for an existing photo
No photo available? Tap "No photo available? Enter measurements manually" on the first step instead

That's it — everything runs client-side in the browser. No backend, database, or API key required for the current build.

* Tip: a synthetic test photo (irregular dark "hole" + an A4 reference sheet) can be generated on request if you want something to try the detection pipeline on immediately.

# Using the measurement workflow
Step	What happens
1. Capture => Take/upload a photo, or switch to manual entry
2. Detect =>  AI auto-traces the hole boundary; adjust sensitivity or trace manually
3. Calibrate => Click two points on a reference object of known length
4. Depth => Enter hole depth (optional — defaults to 3 cm)
5. Cement => Pick a mix grade (M10–M30) and material prices
6. Report=> view/export the full measurement + material + cost report

The step indicator at the top is clickable to jump back and forth (manual-entry mode skips steps 2–3 since there's no photo to trace or calibrate).

# Tech notes
Frontend only — plain HTML/CSS/JavaScript, no framework, no build tooling
"AI" detection is a genuine, from-scratch image-processing pipeline (thresholding + flood fill + contour tracing) rather than a real trained model — browsers can't run YOLOv8/YOLOv11/SAM/Mask R-CNN directly. It's a practical stand-in tuned for hole/pothole-style photos (dark region against a lighter surface)
PDF export uses jsPDF, loaded from a CDN
History storage uses a simple key-value persistence API (per-browser/per-account), not a real database
All calculations (area, volume, dry-volume cement/sand/aggregate quantities) use standard construction-estimation formulas
Wiring this to a real backend

The spec this was built from called for YOLOv11 + SAM + OpenCV on a Python (Flask/FastAPI) backend, MongoDB/Firebase storage, and Firebase Auth. To move in that direction:

Replace detectHoleMask() in the JS with an API call to a backend running a real segmentation model
Replace the local persistence calls with real database + auth-backed endpoints
Everything else (UI, math, PDF, report layout) can stay as-is
🎨 Customizing the branding
App name: search/replace Darshan Cement AI throughout index.html
Favicon (browser tab icon): edit the <link rel="icon" ...> tag in <head>
Nav logo mark: edit the .brand-mark CSS class — swap the striped gradient for background:url('your-logo.png') center/cover; to use an image instead
Colors: all theme colors are CSS variables at the top of the <style> block (--hazard, --tape, --steel-blue, etc.)

Disclaimer!!!

Measurements, material quantities, and cost estimates are guidance only. Always verify critical or structural repairs with a qualified engineer or contractor before ordering materials or beginning work.

