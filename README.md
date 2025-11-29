# Healthcare LLM Guardrail Framework

The Healthcare LLM Guardrail Framework is a validation and safety layer designed to ensure reliable, structured, and compliant outputs from large language models used in healthcare automation workflows. The framework focuses on schema enforcement, hallucination detection, and domain-specific rule validation to prevent unsafe or incorrect LLM responses from entering downstream clinical, RCM, and payer-facing systems.

---

## Purpose

Healthcare LLM applications frequently interact with sensitive data, medical coding standards, and operational workflows that require strict accuracy. Unvalidated LLM output can introduce:

- Incorrect CPT/ICD/Modifier codes  
- Fabricated or unsupported clinical statements  
- Invalid payer rules  
- Non-compliant or unstructured response formats  
- Downstream processing failures  
- Risk to financial, operational, or clinical integrity  

This framework provides a robust intermediary layer between LLMs and production systems, ensuring all generated content is validated, normalized, and safe before use.

---

## Core Capabilities

### 1. Schema Validation  
Enforces strict output formats using Pydantic and JSON Schema.  
Prevents malformed or incomplete structures from reaching business logic.

### 2. Medical Code and Terminology Validation  
Validates CPT, ICD, and modifier codes.  
Checks for domain alignment (e.g., CPT–ICD compatibility).  
Ensures the LLM does not fabricate or misuse medical terminology.

### 3. Hallucination Detection  
Identifies unsupported medical claims, fabricated payer rules, inconsistent reasoning, and domain-inaccurate terminology.  
Uses rule-based, pattern-based, and embedding-based checks.

### 4. Structured Output Enforcement  
Transforms natural-language LLM responses into stable, machine-readable objects:  
JSON, key-value mappings, label sets, and validated structured outputs.

### 5. Safety Enforcement Layer  
Applies healthcare-specific constraints such as:  
- Documentation requirements  
- Coding domain boundaries  
- Claim processing constraints  
- Payer-specific limitations  
- Prohibited reasoning patterns  

### 6. Correction Pipeline (Optional)  
Implements a feedback loop where invalid responses are returned to the LLM for self-revision based on specific violations.  
Ensures the final output meets all safety and compliance expectations.

---

## Architecture

```
healthcare-llm-guardrail-framework/
│
├── guardrails/
│   ├── schema/
│   │     ├── json_schema_loader.py
│   │     └── pydantic_schema.py
│   ├── filters/
│   │     ├── hallucination_filter.py
│   │     ├── clinical_term_filter.py
│   │     └── code_safety_filter.py
│   ├── enforcement/
│   │     ├── output_enforcer.py
│   │     ├── structure_guard.py
│   │     └── correction_pipeline.py
│   └── utils/
│         └── validator_utils.py
│
├── examples/
│       ├── schema_validation_demo.ipynb
│       └── guardrail_pipeline_demo.ipynb
│
├── tests/
│       ├── test_schema.py
│       ├── test_filters.py
│       └── test_enforcement.py
│
├── requirements.txt
└── README.md
```

---

## Example Workflow

1. LLM generates an output containing CPT, ICD, or claim-related information.  
2. The Guardrail Framework receives the response.  
3. Schema validator ensures the structure is correct.  
4. Code validators verify each medical code against authoritative sets.  
5. Hallucination filters evaluate unsupported or fabricated content.  
6. Safety rules enforce domain-specific constraints.  
7. The final output is either:  
   - Approved and passed downstream, or  
   - Returned to the LLM for correction with violations specified.

This design mirrors real-world LLM deployment patterns in healthcare automation pipelines.

---

## Technology Stack

- Python 3.10+  
- Pydantic v2  
- JSON Schema  
- Regex-based validation  
- Optional integration with embedding models  
- pytest for testing  

---

## Roadmap

- CPT/ICD compatibility matrix integration  
- Embedding-driven hallucination scoring  
- Modifier-level rule constraints  
- Batch processing support for multi-agent systems  
- FastAPI wrapper for Guardrail-as-a-Service deployment  
- Domain rule expansion for RCM, clinical documentation, and payer-specific workflows  

---

## License

MIT License © 2025 Lisa Patel

