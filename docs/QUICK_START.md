# MCQ Generator - Quick Start

## Installation

```bash
pip install -e .
```

Set your API key (default provider is Perplexity):

```bash
export PERPLEXITY_API_KEY="your_key_here"
```

## Basic Usage

### Generate MCQs

```bash
python scripts/mcq_generate_cli.py \
  --field "Python" \
  --difficulty medium \
  --count 5 \
  --options 4 \
  --save python.json
```

### Generate True/False Questions

```bash
python scripts/binary_question_cli.py \
  --field "Biology" \
  --difficulty easy \
  --count 5 \
  --question-type true_false
```

## Help

```bash
python scripts/mcq_generate_cli.py --help
python scripts/binary_question_cli.py --help
```

## Common CLI Options

| Flag | Description | Default |
|------|-------------|---------|
| `--field, -f` | Subject field (required) | - |
| `--difficulty, -d` | easy, medium, hard | medium |
| `--count, -c` | Number of questions | 5 |
| `--provider` | openai, claude, perplexity, litellm | perplexity |
| `--model` | Model name | sonar |
| `--save` | Output JSON file | auto-generated |

For detailed documentation, see the other docs in this directory.
