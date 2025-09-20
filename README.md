# 📄 Smart OMR Evaluation System

## 🚀 Overview
This project is an AI-powered **Optical Mark Recognition (OMR)** evaluation system designed for speed, scalability, and real-world deployment.  
It supports **two workflows**:  
1. **Real-time individual upload** (low-latency, mobile-first)  
2. **Bulk scanned PDF processing** (scalable for thousands of sheets)  

Our design ensures **fast results, minimal storage overhead, and batch scalability** — perfect for both classroom quizzes and large-scale exams.

---

## ⚡ Workflow Modes

### 1️⃣ Mode 1 — **Individual Upload (Real-time)**
- **Flow**:
  - Evaluator/student takes a photo of the OMR sheet.
  - Image is uploaded → processed instantly.
  - Only the **result schema (JSON/DB entry)** is stored.
  - Optional: Store overlay image for audit.

- **Latency**:
  - ~0.6–1.0 sec per sheet (including image upload + processing).
  - Feels real-time for students/teachers.

- **Advantages**:
  - Extremely fast, <2 sec per result.
  - No heavy image/PDF storage → only structured results.
  - Perfect for **live classroom tests**.

---

### 2️⃣ Mode 2 — **Batch Processing (Scanned PDF Set)**
- **Flow**:
  - Institute uploads a **scanned PDF** (e.g., 3000 pages).
  - System splits PDF → parallel processing of each sheet.
  - Results stored in DB along with optional overlays.

- **Latency**:
  - ~1 sec per sheet (baseline).
  - On 4-core server → ~12–15 min for 3000 sheets.
  - On 8-core server → ~6–8 min for 3000 sheets.
  - With cluster (Celery + Docker workers) → <3 min possible.

- **Advantages**:
  - Handles **large-scale exams** efficiently.
  - Flexible scaling via server parallelization.
  - Results for 3000 sheets in minutes instead of days.

---

## 🔑 Latency Comparison

| Mode | Input Type | Storage | Latency per Sheet | 3000 Sheets Total |
|------|------------|---------|-------------------|------------------|
| **Mode 1** | Mobile photo | DB schema only (optional overlay) | ~1 sec | N/A (done live) |
| **Mode 2** | Scanned PDF set | Results + optional overlays | ~1 sec/sheet (parallelized) | 8–15 min (on server) |

---

## 🏗️ Tech Stack
- **Python / OpenCV** → Image preprocessing & OMR bubble detection  
- **Tesseract (optional)** → Roll number / ID extraction  
- **Flask/FastAPI** → REST API for uploads and results  
- **PostgreSQL / SQLite** → Result storage (JSON schema)  
- **Celery + Redis (optional)** → Distributed batch processing  

---

## ✅ Features
- Real-time result generation from **individual uploads**.  
- Bulk processing of **scanned exam PDFs**.  
- **Schema-only storage** → lightweight and fast.  
- Scalable architecture for **3000+ sheets**.  
- Optional **overlay image generation** for audit.  

---

## 🎯 Hackathon Pitch
> “We designed our solution with **two workflows**:  
> - For **individual uploads** (via mobile), latency is ~1 second per sheet. We skip image storage and directly store results in DB, making it real-time.  
> - For **bulk uploads** (scanned PDFs with thousands of sheets), we deploy our API on a multi-core server and process 3000 sheets in under 15 minutes. This way, we cover both use-cases: real-time feedback for students and bulk evaluation for institutes.”  

---

## 📂 Repo Structure (planned)
├── app/ # Backend code
│ ├── api/ # Flask/FastAPI routes
│ ├── omr/ # OMR detection + processing
│ └── utils/ # Helpers (PDF split, overlay)
├── tests/ # Sample test cases
├── docs/ # Documentation
├── requirements.txt # Python dependencies
├── README.md # Project overview (this file)

yaml
Copy code

---

## 📌 Next Steps
- [ ] Implement Mode 1 (real-time photo upload → JSON schema)  
- [ ] Implement Mode 2 (batch PDF split + multiprocessing)  
- [ ] Add DB schema for result storage  
- [ ] Deploy API on cloud server  
- [ ] Optimize for <3 min latency for 3000 sheets  

---

## 👥 Team
- **AI/ML Engineer** → OMR detection pipeline  
- **Backend Developer** → API + database  
- **Deployment Engineer** → Scaling & server setup  

---

## 🏆 Why This Matters
- Cuts evaluation time from **days → minutes**.  
- Works for both **small quizzes** and **large exams**.  
- **Fast, scalable, and storage-efficient**.  

---
