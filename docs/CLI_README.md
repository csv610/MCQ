# MCQ Generator - Documentation Index

Welcome to the MCQ Generator documentation. This folder contains everything you need to generate high-quality multiple-choice and binary questions using AI.

## Documentation Files

### Getting Started
- **[SETUP.md](SETUP.md)** - Complete setup and installation guide
- **[QUICK_START.md](QUICK_START.md)** - Fast reference guide

### Detailed Usage
- **[CLI_USAGE.md](CLI_USAGE.md)** - Complete command documentation with examples
- **[CLI_FEATURES.md](CLI_FEATURES.md)** - Feature highlights and architecture overview

### Technical Reference
- **[CODE_QUALITY.md](CODE_QUALITY.md)** - Code quality analysis
- **[TESTING.md](TESTING.md)** - Test suite documentation
- **[TEST_RESULTS.md](TEST_RESULTS.md)** - Test results report
- **[CHANGES.md](CHANGES.md)** - Implementation changes
- **[PROJECT_SUMMARY.md](PROJECT_SUMMARY.md)** - Project overview

## Quick Start

```bash
# Install
pip install -e .

# Set API key
export PERPLEXITY_API_KEY="pplx-..."

# Generate MCQs
python scripts/mcq_generate_cli.py --field "Python" --options 4

# Generate True/False questions
python scripts/binary_question_cli.py --field "Biology" --question-type true_false
```

## Features

- **AI-Powered Generation** - Multiple LLM providers via LiteLLM
- **Question Types** - MCQs, True/False, Yes/No
- **Customizable** - Difficulty, count, options, correct answers
- **Reliable** - Automatic retry with exponential backoff
- **Portable** - JSON output with metadata

## Requirements

- Python 3.10+
- litellm, tenacity, tqdm

## Reading Order

1. **First time?** → Start with [SETUP.md](SETUP.md)
2. **In a hurry?** → Check [QUICK_START.md](QUICK_START.md)
3. **Need details?** → Read [CLI_USAGE.md](CLI_USAGE.md)
4. **Want features list?** → See [CLI_FEATURES.md](CLI_FEATURES.md)
