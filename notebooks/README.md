#  Project Title: CV Section Classification and Structural Information Extraction

## 1. Introduction and Problem Definition

This project focuses on the **Domain-Specific Topic Classification** problem aimed at **automatically segmenting text lines from a Curriculum Vitae (CV)** into logical sections.

###  Objective
To classify each line of unstructured CV text into three primary categories:

- **content:** Main text such as experience, skills, or education details.  
- **header:** Section titles (e.g., “PROFESSIONAL SUMMARY”, “EDUCATION”).  
- **meta:** Personal or contact information (e.g., name, email, phone).

---

## 2. Dataset and Preprocessing

**Dataset Name:** Resume Section Classification Dataset  
**Source:** [Hugging Face](https://huggingface.co)  
**Number of Data Points:** ~40,000 rows  

### 🔧 Preprocessing Steps
- Raw single-column data (e.g., `meta\tothers\tJitesh Vishwakarma`) was **split into three columns:**
  - `main_label`
  - `sub_label`
  - `clean_text`
- Identified **significant class imbalance**:  
  - `content: 27,341`  
  - `meta: 7,311`  
  - `header: 5,349`
- This imbalance motivated using **Macro F1-Score** instead of Accuracy for evaluation.
- Cleaned dataset (`clean_cv_data.csv`) was stored and synced via **GitHub** and **Google Drive** for collaborative work.

---

## 3. Experimental Methods and Comparison

The project compared a total of **six models**, spanning both **Classical Machine Learning (ML)** and **Deep Learning (DL)** approaches.

| Method | Representation | Accuracy | Macro F1 | Key Strength | Key Weakness |
|:--|:--|:--:|:--:|:--|:--|
| **Naïve Bayes** | TF-IDF | 0.86 | 0.80 | Simple, fast baseline | Fails on minority classes |
| **Logistic Regression** | TF-IDF | 0.879 | 0.807 | Solid classical baseline | Still weak on short segments (meta) |
| **Linear SVM** | TF-IDF | 0.874 | — | Strong linear separation | Limited contextual understanding |
| **CNN** | Word Embeddings | 0.88 | 0.83 | Captures spatial text patterns | Slight overfitting |
| **BiLSTM** | Word Embeddings | 0.865 | 0.815 | Sequence context learning | Sensitive to imbalance |
| **DeBERTa** | Contextual Embeddings | **0.94+** | **0.88–0.89** | Best semantic understanding | Computationally expensive |

---

## 4. Results and Conclusions

###  Best Performance
The **DeBERTa model** achieved the **highest performance** with a **Macro F1-Score of 0.879–0.89**.  
This demonstrates the necessity of utilizing **contextual models** to capture the **semantic nuances** within CV text.

---

###  Baseline Insights
- **Naive Bayes** established the initial baseline (**Macro F1: 0.80**).  
- It revealed a strong bias toward the **dominant content class** (*Recall: 0.96*).  
- The model struggled on **minority classes**, specifically *meta* (*Recall: 0.63*) and *header* (*Recall: 0.70*).

---

###  Error Analysis
The most challenging categories across all models were **short, context-poor segments**,  
particularly within the **meta** and **header** classes.  
This indicates that limited contextual information significantly reduces model accuracy for those segments.

---

###  Future Work
Future research should focus on:
- **Data augmentation** to increase minority class examples.  
- **Contextual embeddings** or **attention-based models** to improve recall for *meta* and *header*.  
- Experimenting with **domain adaptation** or **transfer learning** to enhance robustness across diverse CV formats.


