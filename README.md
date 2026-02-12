# 🧲 n8n Google Maps Lead Generation Workflow

This repository contains an **n8n automation workflow** designed for **B2B lead generation**. The workflow automatically searches Google Maps for businesses based on user prompts, extracts contact details, stores them in Google Sheets, and optionally enriches the data using AI.

---

## 🚀 Features

* 💬 **Chat-based AI agent** for natural language lead requests
* 🗺️ **Google Maps business search** via Serper.dev API
* 📄 **Automatic storage in Google Sheets**
* 🧠 **AI-powered data enrichment** (email & background info)
* 🔁 Pagination support for bulk lead collection
* 🧹 Data cleaning (phone formatting, empty field handling)

---

## 🧠 Workflow Architecture

### 1️⃣ Chat-Based AI Agent

* Accepts user input such as:

  ```
  Find dental clinics in Ahmedabad
  ```
* Powered by **Google Gemini AI**
* Maintains **conversation memory** for context-aware searches
* Converts natural language queries into structured search tasks

---

### 2️⃣ Google Maps Business Search

* Uses **Serper.dev Google Maps API**
* Configured with geographic focus:

  * 📍 Location: **Bhopal, India**
  * 🌐 Coordinates: `23.233247, 77.416724`
* Supports pagination (currently up to **page 4**)

#### Extracted Business Data:

* Business Name
* Address
* Phone Number ("+" removed)
* Website URL
* Google Rating
* Opening Hours

---

### 3️⃣ Data Processing & Storage

The workflow processes and stores data as follows:

* Formats extracted business data into structured JSON
* Normalizes phone numbers (removes country prefix symbols)
* Sets `Email = "N/A"` when not available
* Saves results to **Google Sheets immediately after each search**
* Does **not consolidate results** (each search appends rows)
* Continues searching until no more results are returned

---

### 4️⃣ Data Enrichment Subworkflow (Separate Workflow)

> ⚠️ This workflow is intentionally kept **separate** from the main lead generation flow.

#### Trigger

* Runs automatically when **new rows are added** to the Google Sheet

#### Steps

* Skips header and empty rows
* Iterates over each business entry
* Uses AI to:

  * Extract or infer **email addresses**
  * Generate **background/company information**
* Updates the same Google Sheet with enriched data

---

## 🎯 Use Case

This automation is ideal for:

* B2B lead generation
* Sales prospecting
* Agency outreach campaigns
* Local business research

It allows teams to quickly build **industry- and location-specific lead lists** without manual Google Maps scraping.

---

## 🛠️ Tech Stack

* **n8n** – Workflow automation
* **Google Gemini AI** – Natural language understanding & enrichment
* **Serper.dev API** – Google Maps search
* **Google Sheets API** – Data storage

---

## 📌 Notes & Best Practices

* Respect Google & data privacy policies when using extracted data
* Use enriched emails responsibly for outreach
* Adjust pagination carefully to avoid API rate limits
* Keep enrichment workflow isolated for better scalability

---

## 📷 Example Prompt

```
Find real estate agencies in Indore
```

---

## 📄 License

This project is intended for educational and internal business use. Ensure compliance with all third‑party API terms before using in production.

---

## 🙌 Author

Built with ❤️ using **n8n automation**
