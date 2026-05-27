# AI-Powered Personal Debt Finance Advisor

> An intelligent Streamlit app that analyzes your debts, generates optimized repayment plans, and delivers personalized financial guidance through a conversational AI interface.

---

## Overview

FinanceBrew combines LLM-powered chat (Llama 3.3 70B via Groq) with deterministic financial algorithms to help users understand and eliminate debt faster. Users enter their debts and income, then get interactive repayment plans, what-if scenario modeling, document analysis, and AI-driven credit improvement advice — all in one app.

---

## Features

### Debt Repayment Engine
- **Avalanche** — targets highest-APR debt first; minimizes total interest paid
- **Snowball** — targets lowest-balance debt first; maximizes early motivation
- **Mathematical Optimal** — linear programming to find the absolute fastest payoff path
- Month-by-month payment schedules with principal vs. interest breakdowns

### AI Financial Advisor
- Conversational chat backed by Groq's Llama 3.3 70B model
- Slash commands for quick actions:
  ```
  /plan strategy=avalanche budget=15000
  /whatif extra=3000
  /rag question="explain debt consolidation"
  ```
- RAG-powered educational module retrieves relevant financial knowledge
- Persistent chat history within a session

### Scenario Modeling
- What-if analysis for lump-sum windfalls, extra monthly payments, and strategy switches
- Interactive charts comparing debt trajectories side-by-side

### Document Intelligence
- Upload PDFs, CSVs, Excel, or TXT bank statements for automated analysis
- Extracts balances, rates, and transaction summaries without manual entry

### Credit Optimization
- Personalized credit utilization recommendations
- Score improvement timelines based on current debt profile

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Streamlit |
| AI / LLM | LangChain + Groq API (Llama 3.3 70B) |
| Financial Algorithms | Python (NumPy, Pandas) |
| Data Validation | Pydantic v2 |
| Visualization | Matplotlib |
| Knowledge Retrieval | Vector store (RAG) |
| File Parsing | PyPDF2 / openpyxl / csv |

---

## Project Structure

```
financebrew/
├── app2.py / app3.py         # Streamlit application entry points
├── static/
│   └── index.html            # Static frontend assets
├── core/
│   ├── schemas.py            # Pydantic data models (Debt, UserProfile, RepaymentPlan)
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

## Getting Started

### Prerequisites
- Python 3.8+
- A [Groq API key](https://console.groq.com) (free tier available)

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/yourusername/financebrew.git
cd financebrew

# 2. Install dependencies
pip install -r requirements.txt

# 3. Configure environment
cp .env.example .env
# Edit .env and add your Groq API key
```

### Environment Variables

```env
GROQ_API_KEY=your_groq_api_key_here
LLM_MODEL=llama-3.3-70b-versatile
DEBUG_MODE=false
```

### Run the App

```bash
streamlit run app3.py
```

Open [http://localhost:8501](http://localhost:8501) in your browser.

---

## Usage

1. **Set up your profile** — enter monthly income, expenses, and available debt budget
2. **Add your debts** — use the interactive editor or import a CSV (name, balance, APR, minimum payment)
3. **Generate a plan** — choose avalanche, snowball, or optimal and view your full payoff schedule
4. **Chat with the advisor** — ask questions in plain English or use slash commands
5. **Upload documents** — drop in a bank statement or credit card PDF for automated parsing
6. **Run scenarios** — see what happens if you put an extra ₹5,000/month toward debt

---

## Running Tests

```bash
# Full test suite
python -m pytest tests/ -v

# Optimization logic only
python -m pytest tests/test_optimization.py -v
```

---

## Configuration

| Variable | Description | Default |
|---|---|---|
| `GROQ_API_KEY` | Groq API authentication key | **Required** |
| `LLM_MODEL` | Language model to use | `llama-3.3-70b-versatile` |
| `DEBUG_MODE` | Enable verbose debug output | `false` |

To customize AI behavior, edit `core/prompts.py`. To add educational content, place text files in `data/financial_kb/`.

---

## Privacy & Security

- All financial calculations run **locally** — no balance or income data is sent to external servers
- Only the chat messages you type are sent to the Groq API
- No permanent storage of personal financial data; everything is session-based
- API keys are loaded from environment variables, never hardcoded

---

## License

MIT License — see [LICENSE](LICENSE) for details.

---

> **Disclaimer:** FinanceBrew provides educational financial guidance only and is not a substitute for advice from a qualified financial advisor.
