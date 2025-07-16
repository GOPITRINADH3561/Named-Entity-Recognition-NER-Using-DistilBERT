# Named Entity Recognition (NER) Using DistilBERT

🧠 Project Summary:
This project focuses on training a transformer-based model (DistilBERT) to perform Named Entity Recognition on 11,090 English tweets. The model identifies and classifies entities like PERSON, ORG, LOC, etc., using IOB tagging and character-span annotations.

📁 Files Included:
- coded_sol.ipynb — Full implementation in Jupyter
- report.pdf — 4-page project summary and results
- Data.json — 11,090 tweets with entity spans
- problem.pdf — Assignment instructions

⚙️ Steps Overview:

1. Preprocessing:
   - No text cleaning needed (already done).
   - Plotted tag distributions.
   - Analyzed how many tweets contain 1+, 2+, etc., tags.

2. Character-Spans to IOB Tags:
   - Used DistilBERT tokenizer.
   - Mapped spans to IOB tags:
     - B- for beginning
     - I- for inside
     - O for outside
   - Special tokens ([CLS], [SEP]) tagged with O.

3. Finetuning DistilBERT:
   - Transformer layers frozen.
   - Custom classification head trained for 30 epochs.
   - Used cross-entropy loss, Adam optimizer, 5e-4 learning rate.
   - Achieved macro F1 score ≈ 0.634 on validation set.
   - Best performing tags: O, B-GPE, B-DATE, I-PERSON.

4. Word-level Tagging and Evaluation:
   - Converted subword tokens to word-level tags.
   - Two reconciliation methods:
     a) Majority Voting — Best results
     b) First Token — Slightly lower accuracy
   - Word-level F1 score with Majority Voting: 1.00 for all tags.

📊 Hyperparameters Used:
- learning_rate: 5e-4
- batch_size: 16
- dropout: 0.3
- epochs: 30
- max_seq_length: 128
- loss: CrossEntropy
- optimizer: AdamW

📝 Insights & Challenges:
- Subword token handling was tricky during tagging and evaluation.
- Model did well on common tags (O, PERSON, GPE) but struggled with rare ones like I-NORP or B-LOC.
- Word-level evaluation using Majority Voting provided better real-world accuracy.

🧪 Total Trained Parameters:
- 11,535 (classifier head only)

🗑️ Tags considered for removal:
- I-NORP, B-LOC, I-LOC due to consistently poor performance and low data support.

👤 Author:
Gopi Trinadh Maddikunta
