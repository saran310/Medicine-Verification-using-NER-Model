# 🏥 Medicine Verification System (India)

This project automates the verification of medicines against official **Indian government reference lists** such as the **National List of Essential Medicines (NLEM 2022)** and the **CDSCO Approved Drugs** database.  
It helps identify whether medicines in a given dataset are officially recognized and approved for use in India.

---

## 📌 Features
- ✅ Verifies medicines against **NLEM 2022** and **CDSCO approvals**  
- 🔎 Performs **exact** and **fuzzy string matching**  
- 📊 Generates a verification report with statuses:  
  - ✅ Found  
  - ❌ Not Found  
  - ⚠ Close Match  
- ⚡ Automated pipeline (no manual verification required)  
- 📝 Provides summary statistics for quick insights  

---

## 📂 Data Sources
- **User Dataset**: Any CSV/Excel file with medicines (e.g., `medicine_name`, `salt_composition`).  
- **Reference Lists**:  
  - [NLEM 2022 (India)](https://www.cdsco.gov.in/opencms/opencms/en/consumer/Essential-Medicines/)  
  - CDSCO Approved Drugs Index  

---

## ⚙️ Methodology

1. **Preprocessing**
   - Normalize medicine names (lowercase, remove dosage units).
   - Extract salt compositions.

2. **Matching**
   - **Exact match**: If salt matches directly.  
   - **Fuzzy match**: Uses Levenshtein distance (via `rapidfuzz`) to handle spelling/format variations.  

   Matching thresholds:  
   - Score ≥ 90 → ✅ Found  
   - 70 ≤ Score < 90 → ⚠ Close Match  
   - Score < 70 → ❌ Not Found  

3. **Reporting**
   - Outputs a detailed report with match results and scores.  
   - Provides summary statistics.  


---

## 📊 Example Output

| query_medicine     | match             | score | status   |
|--------------------|------------------|-------|----------|
| Paracetamol 500mg  | paracetamol      | 100   | ✅ Found |
| Crocin DS          | paracetamol      | 92    | ⚠ Close Match |
| UnknownDrugX       | –                | –     | ❌ Not Found |

**Summary:**
- ✅ Found: 247,628  
- ❌ Not Found: 5,616  
- ⚠ Close Match: 729  

---

## 🛠 Tech Stack
- **Python** (main language)  
- **pandas** → data manipulation  
- **rapidfuzz** → fuzzy string matching  
- **tabula-py / camelot** → PDF parsing (NLEM)  
- **requests + BeautifulSoup** → optional scraping (CDSCO)  

---

## 🚀 Future Work
- Add support for **NLEM 2024** (when released).  
- Integrate **State EMLs**.  
- Use **ML/NLP models** (e.g., BioBERT, embeddings) for semantic matching (e.g., *acetaminophen* ≈ *paracetamol*).  
- Build a **web dashboard** for non-technical users.  
- Add **NER** for extracting medicines from free-text prescriptions.  

---

## 📜 License
This project is intended for **educational and research purposes only**.  
It is **not a substitute for clinical judgment** or medical advice.  

---


