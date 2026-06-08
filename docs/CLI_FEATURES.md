# MCQ Generator - Features & Capabilities

## Overview

AI-powered question generation tool with two CLI interfaces for creating multiple-choice and binary (True/False, Yes/No) questions.

## Core Features

### 1. Flexible Model Selection
Choose between OpenAI, Claude, Perplexity, or any LiteLLM-supported provider.

### 2. Customizable Question Generation
- **Field**: Subject area for question generation (required)
- **Subfield**: Optional sub-category within the field
- **Difficulty Level**: easy, medium, or hard
- **Question Count**: 1 to 100+ questions
- **Options per Question** (MCQ): 2+ answer choices
- **Correct Answers** (MCQ): Single, multiple, zero ("None of the Above")

### 3. Question Types
- **Multiple Choice Questions** (MCQ) - customizable option count, single/multiple correct answers
- **True/False Questions**
- **Yes/No Questions**

### 4. Output & Storage
- JSON format with metadata
- Auto-generated or custom filenames
- Timestamped for organization

### 5. Reliability
- Automatic retry with exponential backoff (tenacity)
- Comprehensive error handling
- Detailed logging

### 6. Progress Tracking
- Tqdm progress bars for question parsing
- Visual feedback during generation

## Technical Features

### CLI Tools

| Script | Purpose |
|--------|---------|
| `scripts/mcq_generate_cli.py` | Generate multiple-choice questions |
| `scripts/binary_question_cli.py` | Generate True/False and Yes/No questions |

### Architecture

```
src/mcq_generator/
  __init__.py              - Package exports
  mcq_generator.py         - Core MCQ generation logic
  binary_question_generator.py - Binary question generation
  prompt_builder.py        - Prompt construction
  question_translator.py   - Question translation
  question_prerequisite.py - Prerequisite knowledge
  similar_question_generator.py - Similar question generation
```

## Providers

| Provider | Models | Env Variable |
|----------|--------|-------------|
| Perplexity (default) | sonar, sonar-pro | `PERPLEXITY_API_KEY` |
| OpenAI | gpt-4o-mini, gpt-4o, gpt-4 | `OPENAI_API_KEY` |
| Anthropic | claude-3-5-sonnet, claude-3-5-haiku | `ANTHROPIC_API_KEY` |
| LiteLLM | Any litellm-supported model | Varies |

For detailed usage, see `CLI_USAGE.md`
For quick start, see `QUICK_START.md`
