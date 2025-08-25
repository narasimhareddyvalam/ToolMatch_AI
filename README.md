# ⚡ ToolMatch AI

**ToolMatch AI** is a fine-tuned **T5-small** model that translates vague business automation requests into **structured low-code workflows**.  
It suggests the right combination of tools (like Airtable, Zapier, Slack, Gmail, Typeform) with clear **Trigger → Action** logic — making automation accessible to startups, ops managers, and non-technical teams:contentReference[oaicite:0]{index=0}.

---

## ✨ Project Summary
- **Model:** Hugging Face `t5-small`, fine-tuned with 250 curated examples  
- **Goal:** Convert plain English tasks (e.g., “Remind customers about overdue invoices”) into structured automation recipes  
- **Training:** Hugging Face Transformers, Seq2SeqTrainer, Google Colab (GPU)  
- **UI:** Gradio web interface for interactive testing  
- **Output Example:**  
Use Airtable + Zapier + Gmail.
Trigger: When invoice is overdue in Airtable → Action: Send email via Gmail.

---

## 📂 Dataset Preparation
- **Format:** 250 samples in `.jsonl` format (`{"input": "...", "output": "..."}`)  
- **Steps Taken:**
- Deduplication of prompts  
- Normalization of phrasing  
- Verified `Trigger → Action` structure  
- Added 100 diverse examples across invoicing, CRM, onboarding, HR:contentReference[oaicite:1]{index=1}  

📊 **Tool frequency:**  
- Zapier (26.7%)  
- Airtable (20%)  
- Gmail/Slack/Typeform/Mailchimp (~6.7% each)

---

## 🧠 Model Selection
- **Why T5-small?**
- Text-to-text framing aligns perfectly with workflow generation  
- Lightweight & efficient for free Colab GPUs  
- Encoder-decoder structure ensures controlled outputs:contentReference[oaicite:2]{index=2}  

- **Alternatives considered:**  
- GPT-2 (discarded: decoder-only, less structured)  
- BART (discarded: larger & slower for Colab)  
- FLAN-T5 (tested, limited benefit for Trigger → Action formatting)

---

## ⚙️ Fine-Tuning Setup
- **Framework:** Hugging Face `Seq2SeqTrainer`  
- **Configuration:**  
- Learning Rate: **5e-4** (best after sweep)  
- Batch Size: 8  
- Epochs: 5  
- **Result:** Final training loss ≈ **0.0644** with stable convergence:contentReference[oaicite:3]{index=3}  

---

## 📊 Model Evaluation
- Compared learning rates (2e-4, 3e-4, 5e-4)  
- **Best result:** LR = 5e-4 → lowest loss (0.0644)  
- ✅ Effective generalization to structured business tasks:contentReference[oaicite:4]{index=4}

---

## 🔎 Error Analysis
Tested on tricky prompts:  
- *“Build a dashboard without writing code”* → Partial relevance, missed core idea  
- *“Predict which customers are unhappy”* → Misinterpreted predictive nature  
- *“Help team feel more connected”* → Misaligned, treated as customer service task  

📉 **Insight:** ToolMatch struggles with **abstract or emotional prompts**, highlighting the need for broader training:contentReference[oaicite:5]{index=5}.

---

## 🖥️ Inference Pipeline
Two modes of interaction:  
1. **Console function** (`generate_tool_suggestion()`) for direct testing  
2. **Gradio Web App**  
 - Textbox input for tasks  
 - Predict button → structured tool recipe  
 - Dark theme, responsive layout, emojis for clarity:contentReference[oaicite:6]{index=6}  

---

## 📦 Repository Structure
toolmatch-ai/
├─ ToolMatchAI.pdf # Full project report
├─ demo.mp4 # Demo video (optional, add via Git LFS if >100MB)
├─ dataset/ # Training dataset (.jsonl)
├─ notebook/ # Colab/Notebooks for fine-tuning & inference
├─ model/ # Saved fine-tuned model + tokenizer
├─ app/ # Gradio web app files
├─ README.md # You are here

---

## 🚧 Limitations
- ❌ Struggles with vague/multi-intent prompts  
- ❌ Limited generalization (only 250 samples)  
- ❌ No safety filters for risky automations  
- ❌ Not yet deployed as a hosted public app:contentReference[oaicite:7]{index=7}  

---

## 🙌 Acknowledgments
- [Hugging Face Transformers](https://huggingface.co/docs/transformers)  
- [Gradio](https://www.gradio.app/guides)  
- [Google Colab](https://colab.research.google.com/) for free GPU fine-tuning  
