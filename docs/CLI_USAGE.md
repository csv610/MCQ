# MCQ Generator - Usage Guide

Two CLI tools are provided: one for multiple-choice questions and one for binary (True/False, Yes/No) questions.

## Installation

```bash
pip install -e .
```

## Setup

Set your API key (default provider is Perplexity):

```bash
export PERPLEXITY_API_KEY="pplx-..."
```

## MCQ Generation CLI

### Basic Usage

```bash
python scripts/mcq_generate_cli.py \
  --field "Physics" \
  --difficulty hard \
  --count 5 \
  --options 4 \
  --correct-answers 1 \
  --provider perplexity \
  --model sonar \
  --save physics.json
```

### Options

| Flag | Required | Description | Default |
|------|----------|-------------|---------|
| `--field, -f` | Yes | Subject field | - |
| `--subfield, -sf` | No | Sub-category within field | None |
| `--difficulty, -d` | No | easy, medium, hard | medium |
| `--count, -c` | No | Number of questions | 5 |
| `--options, -o` | Yes | Options per question (> 1) | - |
| `--correct-answers` | No | Correct answers per question | 1 |
| `--max-tokens` | No | Max tokens for LLM | 3000 |
| `--provider` | No | openai, claude, perplexity, litellm | perplexity |
| `--model` | No | Model name | sonar |
| `--save` | No | Output JSON file | auto-generated |

### Examples

```bash
# Minimum required
python scripts/mcq_generate_cli.py --field "History" --options 4

# Custom difficulty and count
python scripts/mcq_generate_cli.py -f "Biology" -d easy -c 10 -o 4 --save biology.json

# Multiple correct answers ("Select all that apply")
python scripts/mcq_generate_cli.py -f "Math" -o 5 --correct-answers 2

# "None of the Above" questions
python scripts/mcq_generate_cli.py -f "Chemistry" -o 4 --correct-answers 0
```

## Binary Question Generation CLI

### Basic Usage

```bash
python scripts/binary_question_cli.py \
  --field "Biology" \
  --difficulty easy \
  --count 5 \
  --question-type true_false \
  --save biology_tf.json
```

### Options

| Flag | Required | Description | Default |
|------|----------|-------------|---------|
| `--field, -f` | Yes | Subject field | - |
| `--subfield, -sf` | No | Sub-category within field | None |
| `--difficulty, -d` | No | easy, medium, hard | medium |
| `--count, -c` | No | Number of questions | 5 |
| `--question-type, -qt` | No | true_false, yes_no | true_false |
| `--max-tokens` | No | Max tokens for LLM | 2000 |
| `--provider` | No | openai, claude, perplexity, litellm | perplexity |
| `--model` | No | Model name | sonar |
| `--save` | No | Output JSON file | auto-generated |
| `--display` | No | Show questions after generation | True |

### Examples

```bash
# True/False questions
python scripts/binary_question_cli.py -f "Physics" -qt true_false

# Yes/No questions with custom provider
python scripts/binary_question_cli.py -f "History" -qt yes_no --provider openai --model gpt-4o-mini
```

## JSON Output Format

### MCQ Format

```json
{
  "field": "Physics",
  "subfield": "Mechanics",
  "generated_at": "2024-11-23T10:30:45.123456",
  "question_count": 5,
  "questions": [
    {
      "question": "What is the SI unit of force?",
      "options": ["Newton", "Joule", "Watt", "Pascal"],
      "correct_answer": ["A"]
    }
  ]
}
```

### Binary Question Format

```json
{
  "metadata": {
    "field": "Biology",
    "question_type": "true_false",
    "count": 3,
    "generated_at": "2024-11-23T10:30:45.123456"
  },
  "questions": [
    {
      "question": "The heart has four chambers.",
      "correct_answer": "True",
      "explanation": "The human heart has four chambers: two atria and two ventricles."
    }
  ]
}
```

## Logging

- MCQ CLI logs to `mcq_generate.log`
- Binary question CLI logs to `binary_question_cli.log`

## Troubleshooting

### Validation Errors

```
Invalid input: Field must be a non-empty string
Invalid input: Number of options (--options) must be greater than 1
Invalid input: Max tokens must be at least 100
```

### API Errors

Check your API key is set and valid for the chosen provider.
