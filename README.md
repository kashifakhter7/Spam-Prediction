The exponential growth of digital communication has made text-based messaging systems 
vulnerable to unsolicited spam content, leading to financial losses, nuisance, and cybersecurity 
threats. Traditional filtering mechanisms are inadequate because spam content evolves 
continuously and employs varied linguistic patterns, obfuscation strategies, and social 
engineering techniques. This project proposes a machine learning-based text classification 
system for detecting spam in emails and SMS messages using statistical learning methods and 
feature engineering. A benchmark dataset is pre-processed through text normalization and 
numerical feature transformation using TF-IDF vectorization. Multiple machine learning 
models including Gaussian Naïve Bayes, Multinomial Naïve Bayes, Bernoulli Naïve Bayes, 
Logistic Regression, Decision Tree Classifier, AdaBoost Classifier, and an Ensemble Voting 
Classifier are trained and evaluated. Metrics such as accuracy and precision are used to 
determine model reliability. Results indicate that Multinomial Naïve Bayes and the Voting 
Ensemble achieve the strongest precision performance, making them ideal for real-time spam 
classification. The trained model is deployed through a Streamlit interface to enable practical 
user interaction. The proposed pipeline demonstrates a computationally efficient and highly 
accurate spam detection mechanism, suitable for communication platforms, enterprise email 
systems, and mobile messaging applications. 

System Overview  
The proposed system follows a pipeline-based architecture, where each stage performs a 
specific function in the transformation of raw text into actionable predictions. The architecture 
ensures that the system is: 
Modular – Each module (preprocessing, feature extraction, model training, evaluation) works 
independently. 
Scalable – New datasets or algorithms can be integrated without redesigning the entire system. 
Efficient – TF-IDF vectorization and optimized machine learning algorithms ensure fast 
execution. 
Deployable – The final model is integrated with a Streamlit-based interface for easy use. 
The overall objective is to convert unstructured text messages into structured numerical 
features, classify them using the best-performing ML model, and deliver instant spam/ham 
prediction results. 
System Architecture Components 
The architecture is divided into several key components, each responsible for a specific task in 
the workflow. 
Input Layer 
This layer accepts raw SMS or email text messages from: 
• Dataset files (CSV/Text) 
• User input through deployment interface 
• External systems (optional future integration) 
Data Preprocessing Module 

 
This module cleans and prepares raw text through: 
• Lowercasing 
• Removing URLs, emojis, numbers, punctuation 
• Stop-word elimination 
• Tokenization 
• Optional stemming/lemmatization 
The output is a purified and standardized text corpus ready for vectorization. 
Feature Engineering Module (TF-IDF) 
The TF-IDF vectorizer transforms text into numerical vectors. 
Key functions: 
• Extract meaningful words 
• Assign importance weights 
• Convert text into sparse matrix form 
• Prepare data for classifier training 
This module greatly influences model accuracy and computational efficiency. 
Model Training Module 
Multiple machine learning algorithms are trained using the processed TF-IDF features. 
Implemented models: 
• Gaussian Naïve Bayes 
• Multinomial Naïve Bayes 
• Bernoulli Naïve Bayes 
• Logistic Regression 
• Decision Tree Classifier 
• AdaBoost Classifier 
• Voting Ensemble Classifier 

 
Each model learns patterns distinguishing spam from ham. 
Model Evaluation Module 
Evaluation uses metrics such as: 
• Accuracy 
• Precision 
This step identifies the best-performing model based on precision, essential in reducing false 
spam detection. 
Model Selection & Serialization 
The best-performing model (Multinomial NB) and TF-IDF vectorizer are serialized using 
Pickle. 
This allows: 
• Fast loading 
• Avoiding retraining 
• Lightweight deployment 
Deployment Layer (Streamlit) 
The final component exposes the model to users through a simple and interactive UI. 
Users can: 
• Enter SMS or email text 
• Trigger classification 
• View prediction instantly 
Streamlit provides a responsive and cross-platform deployment option. 
