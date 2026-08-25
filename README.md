# 🍽️ Review Analyser: Local AI Powered Customer Intelligence

A privacy first, locally hosted sentiment and review analysis application built using Local AI + Ollama + Qwen + Prompt Engineering with Streamlit.

Convert raw, unstructured customer feedback from platforms like Zomato, Swiggy, Google Reviews, Amazon, or App Stores into structured, actionable business reports in seconds without sending a single byte of sensitive customer data to cloud APIs.

## ✨ Key Highlights & Features

* 🔒 **100% Privacy & On-Premise Data Sovereignty**: Operates completely locally via Ollama. No API keys, no external cloud dependencies, zero data leakage, and full compliance with corporate privacy policies.
* 🎯 **Multi-Dimensional Sentiment Analysis**: Calculates overall sentiment (Positive, Neutral, Negative, Mixed), an estimated star rating out of 5, and a clear one-line executive verdict.
* 💡 **Actionable Business Intelligence**: Extracts top positive highlights, critical negative callouts, customer pain points, and strategic business suggestions.
* 🗣️ **Multilingual & Vernacular Support**: Supports output in English, Telugu, and code-switched Tenglish for regional market insights.
* 📊 **Structured JSON Export**: Download generated insights in clean JSON schema format for easy integration into business intelligence platforms, databases, or CRM workflows.
* ⚙️ **Configurable LLM Engine & Parameters**: Dynamically switch between local open-weights models (qwen2.5:3b, llama3.2:1b, llama3.2, mistral) and adjust inference temperature for deterministic JSON output.

## 🔄 System Architecture & Workflow

The application bridges raw unstructured customer text and actionable executive analytics through a 5-stage pipeline:

```
┌─────────────────────────┐
│ Raw Customer Reviews    │  (Zomato, Swiggy, Google, E-Commerce, Support Tickets)
└───────────┬─────────────┘
            │
            ▼
┌─────────────────────────┐
│ Streamlit Frontend UI   │  (Input text area, language selection, temperature tuning)
└───────────┬─────────────┘
            │  Structured System Prompt + Strict JSON Constraints
            ▼
┌─────────────────────────┐
│ Local Ollama REST API   │  (http://localhost:11434/api/chat)
│ (Qwen2.5:3b / Llama 3.2)│
└───────────┬─────────────┘
            │  Raw JSON String Response
            ▼
┌─────────────────────────┐
│ JSON Extractor & Parser │  (Regex fallback parsing & error handling)
└───────────┬─────────────┘
            │
            ▼
┌─────────────────────────┐
│ Executive Dashboard &   │  (Metric boxes, color-coded insight cards,
│ JSON Export Engine      │   and downloadable .json report)
└─────────────────────────┘
```

### Workflow Steps:
1. **Data Ingestion**: Users paste raw, unstructured multi-line customer reviews into the high-contrast Streamlit interface.
2. **Prompt Engineering & Formatting**: The app wraps reviews inside a strict JSON instruction system prompt, specifying required schema fields and target output language.
3. **Local LLM Inference**: Streamlit dispatches an HTTP POST request to the local Ollama daemon hosting lightweight open-weights LLMs like qwen2.5:3b.
4. **Resilient JSON Parsing**: A custom parsing layer extracts and validates the JSON payload from the raw model response with regex fallback for high reliability.
5. **Dashboard Rendering & Export**: Results are rendered into visual KPI cards (Sentiment, Rating, Verdict, Positives, Negatives, Pain Points, Suggestions) with a one-click button to download the structured JSON file.

## 🏢 Target Industries & Value Proposition

| Industry | Primary Use Cases | Why Use This Application? |
| --- | --- | --- |
| 🍕 **Food & Beverage / Cloud Kitchens** | Analyzing Zomato, Swiggy, and Google reviews for food quality, delivery delays, packaging leaks, and staff behavior. | Provides instant operational feedback per kitchen outlet, pinpointing exact items needing quality control. |
| 🛒 **E-Commerce & Retail** | Triage of product reviews, return reasons, defect logs, and packaging feedback across Amazon/Flipkart listings. | Uncovers recurring product flaws or vendor issues quickly without paying SaaS fees per review analyzed. |
| 🏨 **Hospitality & Travel** | Aggregating guest feedback from TripAdvisor, Airbnb, and Booking.com regarding room cleanliness, service speed, and amenities. | Enables hotel managers to boost guest satisfaction scores (NPS/CSAT) by acting on key guest pain points. |
| 🏥 **Healthcare & Patient Care** | Processing patient survey feedback, clinic waiting times, staff care reviews, and pharmacy services. | **HIPAA & Privacy Compliance**: Patient feedback remains strictly on-premise without risking third-party cloud data breaches. |
| 💳 **Financial Services & Banking** | Analyzing mobile banking app store reviews, loan application friction, and branch service feedback. | Complies with strict financial data protection laws (GDPR, PCI-DSS) by guaranteeing zero cloud data transmission. |
| 💻 **Software & SaaS Products** | Mining Play Store, App Store, G2, and Capterra reviews following major feature releases or patch updates. | Detects newly introduced software bugs, pricing dissatisfaction, and competitor comparisons in real time. |

## 🚨 Critical Industry Gaps Filled by This Application

### 1. Data Privacy & Zero Cloud Leakage (Data Sovereignty)
* **The Industry Gap**: Enterprise customer reviews often contain PII (Personally Identifiable Information), specific order IDs, names, phone numbers, or confidential operational notes. Standard AI solutions rely on third-party cloud APIs (OpenAI, Anthropic, Google Cloud), exposing organizations to data breach risks and vendor lock-in.
* **The Solution**: 100% local processing via Ollama ensures data never leaves the host machine, fully satisfying enterprise security, GDPR, and strict privacy audits.

### 2. High Operational Costs of Commercial SaaS Analytics
* **The Industry Gap**: Commercial sentiment platforms (Qualtrics, Sprinklr, Medallia) and cloud LLM APIs charge heavy per-token or monthly seat subscription costs, making continuous large-scale feedback analysis expensive for SMBs and mid-market firms.
* **The Solution**: Zero recurring API costs. Runs entirely on existing hardware (laptops, local workstations, or private GPU servers) using efficient open-weights models.

### 3. Context-Aware SLMs vs. Primitive Keyword-Based Sentiment Tools
* **The Industry Gap**: Legacy sentiment analyzers (VADER, TextBlob, keyword matching) rely on static dictionaries. They fail completely on sarcasm, mixed sentiment ("The food was delicious but delivery took 2 hours and was freezing cold"), and cannot provide strategic advice.
* **The Solution**: Generative Small Language Models (Qwen2.5 / Llama 3.2) deeply comprehend context, separate mixed feelings into discrete pros/cons, and generate actionable business recommendations.

### 4. Vernacular & Code-Switched Language Intelligence
* **The Industry Gap**: In modern global and regional markets, customer reviews are frequently written in code-switched languages (for example Tenglish, Hinglish, etc.), which standard NLP tools reject or mistranslate.
* **The Solution**: Powered by multilingual open-weights models, the analyzer natively understands regional dialects and code-switched inputs, returning output in English, Telugu, or Tenglish.

### 5. Bridging Unstructured Text to Machine-Readable BI Pipelines
* **The Industry Gap**: Review text is unstructured, forcing staff to manually read, tag, and categorize reviews into spreadsheets before operational decisions can be made.
* **The Solution**: Automatically transforms unstructured text blocks into a standardized JSON schema containing ratings, sentiment metrics, pain point arrays, and keyword tags ready for automated database ingestion or BI reporting.

## 🚀 Quickstart & Setup Guide

### Prerequisites
1. **Python 3.9+** installed on your system.
2. **Ollama** installed from [ollama.com](https://ollama.com).

### Step 1: Start Ollama & Pull the Model
Open your terminal or PowerShell and run:
```bash
# Start Ollama service (if not running automatically)
ollama serve

# Pull the lightweight, high-performance Qwen2.5:3b model
ollama pull qwen2.5:3b
```

You can also pull other supported models:
```bash
ollama pull llama3.2:1b
ollama pull llama3.2
ollama pull mistral
```

### Step 2: Clone Repository & Set Up Environment
```bash
# Clone repository
git clone https://github.com/akhiranandan-04/Review-Analyser-Ollama.git
cd Review-Analyser-Ollama

# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

### Step 3: Run the Streamlit Application
```bash
streamlit run app.py
```
Access the application in your web browser at `http://localhost:8501`.

## 📄 License 
Distributed under the open-source license. Contributions and feature suggestions are welcome!
