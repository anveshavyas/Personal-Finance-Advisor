# 🤖 AI-Powered Personal Debt Finance Advisor

An intelligent Streamlit app that analyzes your debts, generates optimized repayment plans, and delivers personalized financial guidance through a conversational AI interface.

---

## ✨ Features

### 💸 Debt Repayment Engine
- **Three Strategies** — Avalanche (lowest total interest), Snowball (fastest motivation), and Mathematical Optimal (linear programming)
- **Month-by-Month Schedules** — full repayment timelines with principal vs. interest breakdowns per debt
- **Budget Validation** — checks that your budget covers all minimum payments before running plans
- **Multi-Debt Support** — handles any number of debts simultaneously with configurable APR and minimum payments

### 🤖 AI Financial Advisor
- Conversational chat backed by **Groq's Llama 3.3 70B** model via LangChain
- Slash commands for quick structured actions:
  ```
  /plan strategy=avalanche budget=15000
  /whatif extra=3000
  /rag question="explain debt consolidation"
  ```
- **RAG Knowledge Module** — vector store retrieval for financial education queries
- Session-based chat history so context carries across turns

### 🔮 Scenario Modeling
- What-if analysis for extra monthly payments, lump-sum windfalls, and strategy switches
- Interactive Matplotlib charts comparing debt trajectory across scenarios
- Side-by-side interest and timeline comparisons

### 📄 Document Intelligence
- Upload PDFs, CSVs, Excel, or TXT bank statements for automated parsing
- Extracts balances, rates, and transaction summaries without manual entry
- Powered by `core/docsum.py` with multi-format support

### ⭐ Credit Optimization
- Personalized credit utilization recommendations
- Score improvement timelines based on your current debt profile
- Actionable steps ranked by estimated impact

---

### ⚙️ Feature Engineering (Debt Scoring Inputs)

| Feature | Description |
|---|---|
| `apr` | Annual percentage rate normalized to decimal |
| `balance` | Current outstanding balance |
| `min_payment` | Required minimum monthly payment |
| `interest_rate` | Display rate (percent); normalized from APR automatically |
| `limit` | Optional credit card limit (for utilization scoring) |
| `monthly_income` | User's gross monthly income |
| `monthly_expenses` | Fixed monthly expenses |
| `extra_payment` | Available monthly surplus beyond minimums |

---

## 🗂️ Project Structure

```
financebrew/
├── app2.py / app3.py         # Streamlit application entry points
├── static/
│   └── index.html            # Static frontend assets
├── core/
│   ├── schemas.py            # Pydantic v2 models — Debt, UserProfile, RepaymentPlan
│   ├── optimization.py       # Avalanche, snowball & optimal repayment algorithms
│   ├── scenarios.py          # What-if scenario analysis engine
│   ├── recommendations.py    # Personalized advice generator
│   ├── education.py          # Financial literacy content module
│   ├── education_rag.py      # RAG-based knowledge retrieval
│   ├── chat_tools.py         # Slash command processors
│   ├── docsum.py             # Document upload & summarization
│   ├── llm_explainer.py      # LLM explanation wrapper
│   ├── memory.py             # Chat history management
│   ├── plan_utils.py         # Chart & visualization helpers
│   ├── prompts.py            # AI prompt templates
│   └── utils.py              # Shared utilities
└── tests/
    └── test_optimization.py  # Unit tests for repayment algorithms
```

---

## 🚀 Getting Started

### Prerequisites
- Python 3.8+
- A [Groq API key](https://console.groq.com) (free tier available)

### Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/financebrew.git
cd financebrew

# Create and activate a virtual environment
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### Running the App

```bash
streamlit run app3.py
```

Open [http://localhost:8501](http://localhost:8501) in your browser.

---

## 🔌 API / Command Reference

### `/plan` — Generate Repayment Plan
Runs the selected strategy against your current debt profile.

```
/plan strategy=avalanche budget=15000
/plan strategy=snowball budget=12000
/plan strategy=optimal budget=20000
```

**Response:** Full month-by-month schedule with total interest paid and months to debt-free.

---

### `/whatif` — Scenario Analysis
Models the impact of additional payments or windfalls.

```
/whatif extra=3000
/whatif lumpsum=50000
```

**Response:** Updated payoff timeline and interest savings vs. baseline plan.

---

### `/rag` — Educational Query
Retrieves and explains financial concepts from the knowledge base.

```
/rag question="explain debt consolidation benefits"
/rag question="what is credit utilization"
```

**Response:** AI-generated explanation grounded in the vector knowledge store.

---

## 🧰 Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Streamlit |
| AI / LLM | LangChain + Groq API (Llama 3.3 70B) |
| Financial Algorithms | Python — NumPy, Pandas |
| Data Validation | Pydantic v2 |
| Visualization | Matplotlib |
| Knowledge Retrieval | Vector store (RAG) |
| File Parsing | PyPDF2 / openpyxl / csv |

---

## 📦 Key Dependencies

```
streamlit
langchain
groq
pydantic>=2.0
pandas
numpy
matplotlib
pypdf2
openpyxl
python-dotenv
```

---

## 🧪 Testing

```bash
# Full test suite
python -m pytest tests/ -v

# Optimization logic only
python -m pytest tests/test_optimization.py -v
```

---

## ⚙️ Configuration

| Variable | Description | Default |
|---|---|---|
| `GROQ_API_KEY` | Groq API authentication key | **Required** |
| `LLM_MODEL` | Language model to use | `llama-3.3-70b-versatile` |
| `DEBUG_MODE` | Enable verbose debug output | `false` |

Create a `.env` file in the project root:

```env
GROQ_API_KEY=your_groq_api_key_here
LLM_MODEL=llama-3.3-70b-versatile
DEBUG_MODE=false
```

To customize AI responses, edit `core/prompts.py`. To expand the educational knowledge base, add text files to `data/financial_kb/`.

---

## ⚠️ Notes

- **Local calculations** — all debt math runs entirely on your machine; no financial data is sent to external servers
- **Groq API** — only your chat messages are transmitted; Groq's free tier is sufficient for normal usage
- **Session-only storage** — no financial data persists between sessions
- Add these to your `.gitignore`:
  ```
  venv/
  __pycache__/
  *.pyc
  .env
  ```

---

## 📄 License

MIT License — see [LICENSE](LICENSE) for details.

---

> **Disclaimer:** FinanceBrew provides educational financial guidance only and is not a substitute for advice from a qualified financial advisor.
