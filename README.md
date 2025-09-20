# AI Internship Recommender System

This project is a **Python-based AI recommender system** that matches student candidates to internship opportunities based on **skills, qualifications, location, and preferences**. It outputs **top internship recommendations** with a **percentage fit** and **eligibility**.

---

## CSV Files

- **candidates.csv** → Contains student profiles with columns:
  - `ID`, `Name`, `State`, `City`, `Skills`, `Qualifications`, `Year_of_Study`, `GPA`, `Rural_or_Urban`, `First_Time_Applicant`
- **internships.csv** → Contains internship listings with columns:
  - `ID`, `Company`, `Role`, `Required_Skills`, `Qualification_Required`, `Location_State`, `Location_City`, `Sector`, `Duration_Months`, `Stipend_Range`, `Capacity`

> These CSVs are the inputs to the notebook. Users can modify or extend them with real data.

---

## Matching & Scoring System

The model works in **two stages**:

1. **Skill similarity**  
   - Uses **TF-IDF** vectorization and **cosine similarity** between candidate skills and internship required skills.

2. **Preference boosts** (applied on top of skill similarity):

- +2.0 if Qualification matches  
- +0.5 if City matches  
- +0.3 if State matches  
- +0.2 if candidate is Rural  
- +0.2 if First-Time Applicant == Yes  
- +1.0 per skill match  
- -2.0 if Qualification mismatch  

- Total raw score is **normalized to a percentage fit (0–100%)**.  
- **Eligibility** is determined using a configurable **threshold** (default 50%).

> You can tweak threshold, boost values, or top-K recommendations directly in the notebook.

---

## Usage

1. **Place CSV files** (`candidates.csv` & `internships.csv`) in the same folder as the notebook.  
2. **Open and run the notebook** `AI_Internship_Recommender.ipynb`.  
3. **Steps in notebook**:
   1. Load and explore data  
   2. Preprocess skills  
   3. Vectorize skills & compute similarity  
   4. Apply boosted matching logic  
   5. Generate top recommendations with eligibility  
   6. Save results (`final_matches.csv`)  
   7. Test live candidate example  

4. **View results**  
   - `final_matches.csv` is generated automatically after running the notebook.  
   - It contains:
     - Candidate Name & ID  
     - Internship ID, Company, Role  
     - Score (percentage fit)  
     - Eligibility (Yes/No)  
     - Reason for match (skills + boosts)

---

## Live Candidate Test

In the 7th cell of the notebook, you can provide a **single candidate profile** as a dictionary. The notebook will return **top internship recommendations** with:

- Percentage fit score  
- Eligibility  
- Reason (skills + boosts)

Example dictionary:

```python
live_candidate = {
    'Name':'Live Candidate',
    'State':'Guwahati',
    'City':'Dispur',
    'Skills':'Content Writing, Copywriting',
    'Qualifications':'BBA',
    'Year_of_Study':'3rd',
    'GPA':'7',
    'Rural_or_Urban':'Urban',
    'First_Time_Applicant':'Yes'
}
