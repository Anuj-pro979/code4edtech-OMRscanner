# 🚀 Smart OMR Evaluation System

## 📌 Overview
Automated OMR evaluation for **3000+ exam sheets**, designed for **real-time speed** and **bulk scalability**.  
Supports both **mobile photo uploads** and **bulk scanned PDFs** with <0.5% error tolerance.

---

## ⚡ Workflows

### 1️⃣ Real-time Upload (Mobile)
- Student/evaluator uploads photo.
- Processed in **~1 sec per sheet**.
- Only **results schema (JSON/DB)** stored → no heavy images.
- Perfect for **classroom quizzes**.

### 2️⃣ Bulk PDF Upload (Scanned Sets)
- Institute uploads scanned PDF of thousands of sheets.
- PDF auto-split → parallel OMR evaluation.
- **Latency**:  
  - 4-core server → ~12–15 min for 3000 sheets  
  - 8-core server → ~6–8 min  
  - Cluster (Celery/Docker) → <3 min  

---

## 🔑 Latency Comparison

| Mode         | Input Type | Storage              | Latency/sheet | 3000 Sheets |
|--------------|------------|----------------------|---------------|-------------|
| Real-time    | Mobile img | DB schema only       | ~1 sec        | Live        |
| Batch Upload | PDF set    | Results + overlays   | ~1 sec/sheet  | 8–15 min    |

---

## 🏗️ Tech Stack
- **Python + OpenCV** → OMR bubble detection  
- **Flask / FastAPI** → Backend APIs  
- **PostgreSQL / SQLite** → Results DB  
- **Celery + Redis (optional)** → Parallel processing  

---

## ✅ Features
- Real-time evaluation from photos.  
- Bulk PDF exam set processing.  
- Lightweight **schema-only storage**.  
- Optional overlays for audit.  
- Scales from **10 → 3000+ sheets**.  

---

## 🎯 Hackathon Pitch
- **Realtime (mobile):** 1 sec per sheet.  
- **Bulk (3000 sheets):** <15 min on single server, <3 min on cluster.  
- Saves **days of manual work**, gives **instant student feedback**.  

---




flowchart TD
    A[Student takes OMR photo] --> B[Upload photo via web/mobile interface]
    B --> C[Server receives image]
    C --> D[Align image to template]
    D --> E[Extract bubble ROIs based on template]
    E --> F[Check pixel intensity → filled/unfilled]
    F --> G[Map answers to JSON schema]
    G --> H[Compute per-subject & total scores]
    H --> I[Store JSON result in database]
    I --> J[Return result to student/dashboard]
    J --> K[Optional: Overlay image stored for audit]




output 

{
  "student_id": "12345",
  "exam_version": "SetA",
  "answers": {
    "Subject1": [1,3,2,4,0,1,2,3,4,1,0,2,3,1,4,2,0,3,1,2],
    "Subject2": [0,1,3,2,1,4,0,2,3,1,2,0,4,1,3,2,1,0,4,3],
    "Subject3": [1,2,0,3,4,1,2,0,3,4,1,2,0,3,4,1,2,0,3,4],
    "Subject4": [2,3,1,0,4,2,3,1,0,4,2,3,1,0,4,2,3,1,0,4],
    "Subject5": [0,2,3,1,4,0,2,3,1,4,0,2,3,1,4,0,2,3,1,4]
  },
  "scores": {
    "Subject1": 18,
    "Subject2": 16,
    "Subject3": 19,
    "Subject4": 17,
    "Subject5": 20
  },
  "total": 90,
  "timestamp": "2025-09-20T12:34:56"
}



