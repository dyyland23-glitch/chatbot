Here is a precise, granular engineering guide on how to build and execute an automated evaluation harness for production LLMs, free of generic filler:

```markdown
# 🔍 Granular Engineering Guide: Automated LLM Evaluation & Testing Harness

Deploying a model like **Llama** to production requires a rigorous, code-driven testing pipeline. Relying on manual chat checks ("vibes-based testing") fails to catch edge-case regressions. 

This guide details the exact architecture, code patterns, and open-source tooling used by machine learning engineers to automate LLM testing.

---

## 🛠️ Step 1: Setting Up the Test Harness Architecture

To evaluate models programmatically, engineers build Python test suites using modern evaluation frameworks like **DeepEval** or **Promptfoo**. 

### 1. Project Directory Structure
```text
llm_eval_harness/
│
├── data/
│   └── test_cases.json          # The 500+ edge-case inquiries & ground truths
├── evaluators/
│   └── metrics.py               # Custom scoring logic (Faithfulness, Correctness)
├── run_evals.py                 # Main execution script
└── requirements.txt             # pytest, deepeval, openai / httpx

```

### 2. Structuring the Test Dataset (`test_cases.json`)

Each test case must define the user input, the expected context (retrieved via RAG), and the ground-truth answer:

```json
[
  {
    "input": "Can I return a clearance item purchased during the flash sale?",
    "retrieved_context": ["Section 4.2: Clearance items marked as final sale cannot be returned or exchanged."],
    "expected_output": "I apologize, but items purchased during the flash sale as clearance are final sale and cannot be returned or exchanged."
  }
]

```

---

## ⚙️ Step 2: Writing the Evaluation Script (`run_evals.py`)

Using **DeepEval** integrated with **Pytest**, you can automate assertions against your model's outputs.

```python
import pytest
from deepeval import assert_test
from deepeval.test_case import LLMTestCase
from deepeval.metrics import HallucinationMetric, AnswerRelevancyMetric

# 1. Load your test suite from JSON
test_cases_data = [
    {
        "input": "Can I return a clearance item purchased during the flash sale?",
        "actual_output": "Flash sale clearance items are final sale and non-returnable.",
        "retrieved_context": ["Section 4.2: Clearance items marked as final sale cannot be returned or exchanged."]
    }
]

@pytest.mark.parametrize("case", test_cases_data)
def test_customer_support_llm(case):
    # 2. Define quantitative evaluation metrics with strict thresholds
    hallucination_metric = HallucinationMetric(threshold=0.1)  # Max allowed hallucination score
    relevancy_metric = AnswerRelevancyMetric(threshold=0.85)    # Min required relevancy score

    # 3. Construct the test case object
    test_case = LLMTestCase(
        input=case["input"],
        actual_output=case["actual_output"],
        retrieval_context=case["retrieved_context"]
    )

    # 4. Execute assertions (fails CI/CD pipeline if thresholds are breached)
    assert_test(test_case, [hallucination_metric, relevancy_metric])

```

---

## 🔬 Step 3: Core Evaluation Metrics Explained

When running your test harness across the 500+ inquiries, your script measures three vital signals:

1. **Faithfulness (Groundedness Check)**:
* **How it works**: Uses a judge model (e.g., GPT-4 or a local Llama-3-70B-Instruct) to parse your `actual_output` and cross-reference every claim against the `retrieval_context`.
* **Formula**: $\text{Faithfulness} = \frac{\text{Claims supported by context}}{\text{Total claims made in output}}$
* **Passing Threshold**: $\ge 0.95$ (Zero tolerance for unbacked claims).


2. **Semantic Similarity (Correctness)**:
* **How it works**: Uses embedding models (like Hugging Face Transformers `text-embedding-ada-002` or open-source BGE embeddings) to calculate the cosine similarity vector distance between your model's output and the `expected_output`.


3. **Toxicity & Safety Guardrails**:
* **How it works**: Passes responses through specialized classification heads (such as Llama-Guard or NeMo Guardrails) to ensure adversarial prompts (e.g., forcing policy bypasses) are safely rejected.



---

## 🚀 Step 4: Gating Production via CI/CD (**[GitHub Actions](https://github.com/dyyland23-glitch/chatbot/tree/main/.github)**)

To enforce automated quality gates before any deployment, configure a workflow file (e.g., `.github/workflows/eval.yml`) inside your **[chatbot](https://github.com/dyyland23-glitch/chatbot)** repository:

```yaml
name: LLM Evaluation Pipeline

on:
  push:
    branches: [ main ]

jobs:
  evaluate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.10'
          
      - name: Install Dependencies
        run: pip install -r requirements.txt pytest deepeval
        
      - name: Run Test Harness
        env:
          OPENAI_API_KEY: ${{ secrets.OPENAI_API_KEY }}
        run: pytest run_evals.py

```

If a single test case out of the 500+ suite drops below your metric threshold, **[GitHub Actions](https://github.com/dyyland23-glitch/chatbot/tree/main/.github)** automatically blocks the build, preventing faulty weights or broken prompts from reaching production.

```

```
