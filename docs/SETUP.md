# MCQ Generator - Setup Guide

## Prerequisites

- Python 3.10 or higher
- pip (Python package manager)
- An API key from one of: Perplexity, OpenAI, Anthropic, or another LiteLLM provider

## Step 1: Verify Python Installation

```bash
python3 --version
```

Should show Python 3.10 or higher.

## Step 2: Install the Package

From the project root directory:

```bash
pip install -e .
```

This installs the `mcq_generator` package and its dependencies (`litellm`, `tenacity`, `tqdm`).

## Step 3: Configure API Keys

The default provider is Perplexity. Set the corresponding environment variable:

**For Perplexity (default):**
```bash
export PERPLEXITY_API_KEY="pplx-..."
```

**For OpenAI:**
```bash
export OPENAI_API_KEY="sk-..."
```

**For Claude/Anthropic:**
```bash
export ANTHROPIC_API_KEY="sk-ant-..."
```

You can also add these to your shell profile (`~/.zshrc`, `~/.bashrc`, etc.).

## Step 4: Verify Installation

```bash
python scripts/mcq_generate_cli.py --help
python scripts/binary_question_cli.py --help
```

## Step 5: Generate Your First Questions

```bash
python scripts/mcq_generate_cli.py \
  --field "Python Programming" \
  --difficulty medium \
  --count 3 \
  --options 4 \
  --save first_questions.json
```

## Troubleshooting

### "No module named 'tenacity'"

Make sure you installed the package:
```bash
pip install -e .
```

### "Error: field is required"

All CLIs require `--field` (or `-f`) with a non-empty subject.

### API Key Issues

Check that the environment variable for your chosen provider is set:
```bash
echo $PERPLEXITY_API_KEY
echo $OPENAI_API_KEY
```

## Next Steps

- Read `QUICK_START.md` for common usage patterns
- Check `CLI_USAGE.md` for detailed command documentation
- Review `CLI_FEATURES.md` for all available features
