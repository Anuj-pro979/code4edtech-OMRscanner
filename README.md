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
