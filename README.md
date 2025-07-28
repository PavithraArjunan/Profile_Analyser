## Lead Analysis & Automation Platform

A modular pipeline to extract, process, and analyze LinkedIn lead data using NLP and machine learning techniques.

---

## Project Structure

```bash
├── data/
│   ├── data.html                   # Raw LinkedIn HTML profiles
│
├── scripts/Profile_analyser.ipynb
│   ├── extract_profiles.       # Parses LinkedIn HTML to structured data
│   ├── lead_scoring            # ML-based lead scoring
│   ├── cluster_clients         # KMeans clustering for segmentation
│   ├── sentiment_analysis.      # Email sentiment classification
│
├── models/
│   ├── lead_scoring_model.pkl     # Trained model (optional)
│
└── README.md
```

---

## Features

### 1. **Lead Scoring (ML + Business Rules)**

* **Goal:** Prioritize leads based on engagement and role match.
* **Features used:**

  * `skill_count`, `experience_count`, email response rate, LinkedIn activity, etc.
* **Models:** Logistic Regression, Random Forest.
* **Outputs:** `Lead Type` prediction (e.g., Hot, Warm, Cold).
* **Script:** `lead_scoring.py`

---

### 2. **Data Pipeline for LinkedIn Sync**

* **Goal:** Automate the cleaning and updating of LinkedIn profile data daily.
* **Steps:**

  * Parse HTML files using BeautifulSoup.
  * Normalize data (skills, experiences).
  * Check for duplicates.
  * Sync new data to CRM.
* **Script:** `extract_profiles.py`

---

### 3. **Smart Client Segmentation (Clustering)**

* **Goal:** Group clients by behavior or metadata for targeted campaigns.
* **Techniques:**

  * KMeans clustering
  * PCA for visualization
* **Features used:**

  * `skill_count`, `experience_count`, possibly industry/job title
* **Script:** `cluster_clients.py`

---

### 4. **Sentiment Analyzer for Email Replies**

* **Goal:** Classify responses into:

  * Positive (interested)
  * Negative (not interested)
  * Neutral (follow-up needed)
* **Tools:** TextBlob / BERT (optional fine-tuning).
* **Outputs:** Sentiment label added to CRM.
* **Script:** `sentiment_analysis.py`

---

## Requirements

```bash
pip install pandas scikit-learn matplotlib spacy textblob beautifulsoup4
python -m textblob.download_corpora
python -m spacy download en_core_web_sm
```

---

## Example Workflow

```python
# Load structured LinkedIn data
df = pd.read_csv("linkedin_processed_profiles.csv")

# Run lead scoring
from lead_scoring import score_leads
df = score_leads(df)

# Segment clients
from cluster_clients import cluster
df = cluster(df)

# Analyze email replies
from sentiment_analysis import analyze_sentiments
df = analyze_sentiments(df)

# Save updated DataFrame
df.to_csv("processed_leads.csv", index=False)
```

---

## Output

| Name | Job Title | Lead Type | Cluster | Sentiment | Generated Email |
| ---- | --------- | --------- | ------- | --------- | --------------- |
| John | Data Eng. | Hot       | 1       | Positive  | "Hi John, ..."  |
