# 📩 SMS & Email Spam Classifier Using NLP & Machine Learning

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg?logo=python&logoColor=white)](https://www.python.org/)
[![Streamlit](https://img.shields.io/badge/Streamlit-App-FF4B4B.svg?logo=streamlit&logoColor=white)](https://streamlit.io/)
[![Scikit-Learn](https://img.shields.io/badge/scikit--learn-F7931E.svg?logo=scikit-learn&logoColor=white)](https://scikit-learn.org/)
[![NLTK](https://img.shields.io/badge/NLTK-NLP-306998.svg)](https://www.nltk.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-brightgreen.svg)](#)

A high-precision Natural Language Processing (NLP) system designed to detect and filter unsolicited spam, promotional fraud, and phishing messages across SMS and Email communication channels.

Powered by **TF-IDF Vectorization**, **Multinomial Naïve Bayes** (achieving **100% Precision / Zero False Positives**), and deployed via an interactive **Streamlit** web app.

---

## 📌 Project Overview

Digital communication channels are constantly targeted by spam, social engineering lures, and phishing scams. Traditional keyword-filtering rules fail as attack patterns constantly evolve.

This project delivers a machine learning solution that converts unstructured textual messages into numerical feature vectors and classifies incoming communications into:
- **Ham (Class 0)**: Legitimate, authentic messages.
- **Spam (Class 1)**: Unsolicited spam, advertisements, or malicious fraud attempts.

---

## ✨ Features

- **Full NLP Pipeline**: Includes case folding, tokenization, alphanumeric filtering, stop-word elimination, and Porter stemming.
- **Zero False Positives (100% Precision)**: Selected Multinomial Naïve Bayes model ensures legitimate emails are never misclassified as spam.
- **Vector Space Modeling**: TF-IDF (Term Frequency-Inverse Document Frequency) transforms raw text into weighted numeric vectors.
- **Real-Time Interactive UI**: Streamlit web dashboard allowing instant message classification.
- **Production Artifacts**: Pre-trained model (`model.pkl`) and vectorizer (`vectorizer.pkl`) for rapid deployment with zero lag.

---

## 🏗️ Project Architecture

```plaintext
Spam-Prediction/
│
├── Data Set/
│   └── Dataset.csv                             # Raw SMS/Email dataset (5,572 messages)
│
├── ipynb/
│   ├── SMS_Email_Spam_Detection.ipynb          # Exploratory analysis & baseline model development
│   └── SMS_Email_Spam_Detection_Updated.ipynb  # Extended notebook with comparative model evaluation
│
├── pkl file/
│   ├── model.pkl                               # Serialized MultinomialNB classifier
│   └── vectorizer.pkl                          # Serialized TF-IDF vectorizer
│
├── python file/
│   ├── frontend.py                             # Streamlit web application
│   └── sms_email_spam_detection.py             # NLP pipeline, EDA & model training script
│
├── requirements.txt                            # Project dependencies
└── README.md                                   # Complete documentation
```

---

## 🔄 NLP Data Processing Pipeline

```
Raw Text Message ──▶ Lowercasing ──▶ Tokenization (NLTK)
                           │
                           ▼
                  Remove Special Characters & Punctuation
                           │
                           ▼
                  Remove English Stopwords
                           │
                           ▼
                  Stemming (PorterStemmer)
                           │
                           ▼
                  TF-IDF Vectorization
                           │
                           ▼
            Multinomial Naïve Bayes Classifier ──▶ [Spam / Ham]
```

---

## 📊 Dataset Description

Trained on the benchmark **SMS Spam Collection Dataset** (`Data Set/Dataset.csv`):

- **Total Messages**: 5,572 messages
- **Class Breakdown**:
  - `Ham (Legitimate)`: 4,825 messages (86.6%)
  - `Spam`: 747 messages (13.4%)
- **Engineered Text Features**:
  - Character count (`num_characters`)
  - Word count (`num_words`)
  - Sentence count (`num_sentences`)
  - Word Cloud visualization of frequent spam keywords (e.g., *free, win, claim, cash, urgent, call now*)

---

## 📈 Model Performance & Comparison

Multiple text classifiers were trained and tested using an 80/20 train-test split:

| Model | Accuracy | Precision | Key Characteristic |
|:---|:---:|:---:|:---|
| 🏆 **Multinomial Naïve Bayes (MNB)** | **96.12%** | **1.0000 (100%)** | **Best for Production: 0 False Positives** |
| **Voting Classifier** | 94.48% | 1.0000 (100%) | Strong ensemble with 0 false positives |
| **Bernoulli Naïve Bayes** | 97.19% | 97.12% | High accuracy, few false positives |
| **Logistic Regression** | 95.06% | 96.34% | Robust linear classifier baseline |
| **Decision Tree** | 93.51% | 81.91% | Prone to overfitting on specific words |
| **AdaBoost Classifier** | 93.02% | 85.71% | Sensitive to noisy textual tokens |
| **Gaussian Naïve Bayes** | 86.92% | 48.25% | Poor assumption for sparse TF-IDF vectors |

> 💡 **Why Precision Matters Most**: In spam filtering, **Precision is the most critical metric**. A False Negative (spam reaching the inbox) is a minor annoyance, but a False Positive (an important legitimate email sent to the spam folder) can cause critical business or personal disruption. **Multinomial Naïve Bayes achieved 1.0000 Precision**, guaranteeing that no legitimate message was mislabeled as spam.

---

## 🚀 Quick Start Guide

### 1. Clone the Repository
```bash
git clone https://github.com/your-username/Spam-Prediction.git
cd Spam-Prediction
```

### 2. Set Up a Virtual Environment (Recommended)
```bash
# Windows
python -m venv venv
venv\Scripts\activate

# macOS / Linux
python3 -m venv venv
source venv/bin/activate
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

### 4. Download Required NLTK Corpora (First run only)
The application uses NLTK's tokenizers and stopwords. Run in Python:
```python
import nltk
nltk.download('punkt')
nltk.download('stopwords')
```

### 5. Run the Streamlit Web Application
Ensure `model.pkl` and `vectorizer.pkl` from `pkl file/` are accessible in your execution directory, then launch:
```bash
streamlit run "python file/frontend.py"
```

The web dashboard will open in your browser at `http://localhost:8501`.

---

## 💻 How to Use the Web App

1. Enter or paste any SMS or email message in the input box.
   - Example 1 (Spam): `"Congratulations! You have won a $1,000 Walmart Gift Card. Click here to claim your prize."`
   - Example 2 (Ham): `"Hey, are we still meeting for lunch tomorrow at 1 PM?"`
2. Click **Predict**.
3. The system returns:
   - 🔴 **Spam**: High risk / fraudulent message detected.
   - 🟢 **Not Spam**: Safe, legitimate message.

---

## 🛠️ Technologies Used

- **Programming Language**: Python 3.8+
- **Natural Language Processing**: NLTK (Natural Language Toolkit)
- **Machine Learning**: Scikit-Learn (MultinomialNB, TF-IDF Vectorizer)
- **Data Manipulation**: Pandas, NumPy
- **Visualization**: Matplotlib, Seaborn, WordCloud
- **Web App Framework**: Streamlit
- **Model Serialization**: Pickle

---

## 🤝 Contributing

Contributions are welcomed! Feel free to report issues, suggest new features, or submit pull requests.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/NewFeature`)
3. Commit your Changes (`git commit -m 'Add NewFeature'`)
4. Push to the Branch (`git push origin feature/NewFeature`)
5. Open a Pull Request

---

## 📄 License

This project is open-source and licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
