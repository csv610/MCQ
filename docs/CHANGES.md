# MCQ Generator - Recent Changes

## Overview

Refactored codebase: improved architecture, fixed import issues, consolidated modules, and updated documentation.

## Structural Changes

### Package Restructuring
- Migrated source into `src/mcq_generator/` package layout with `pyproject.toml`
- Converted flat intra-package imports to relative imports
- Populated `__init__.py` with re-exports of all public classes

### Deleted Modules
- `question_generator.py` - dead duplicate of classes in `mcq_generator.py`
- `true_false_question_generator.py` - subsumed by `BinaryQuestionGenerator`

### Renamed Files
- `question_prerequsite.py` → `question_prerequisite.py` (typo fix)

### Import Fixes
- `scripts/mcq_generate_cli.py`: fixed to import from `mcq_generator` package
- `scripts/binary_question_cli.py`: fixed to import from `mcq_generator` package
- `scripts/mcq_cli.py`: fixed imports and `BinaryQuestionConfig` reference
- `apps/streamlit_apps/main.py`: replaced `model.get_response()` with `litellm.completion()`, added missing import

### Logging Consolidation
- Library modules no longer set up file/console handlers at import time
- Applications call `setup_logger()` explicitly

## Current Source Files

```
src/mcq_generator/
  __init__.py
  mcq_generator.py              - Core MCQ generation, QuestionConfig, setup_logger
  binary_question_generator.py  - Binary question generation
  prompt_builder.py             - Prompt construction
  question_translator.py        - Question translation
  question_prerequisite.py      - Prerequisite knowledge
  similar_question_generator.py - Similar question generation

scripts/
  mcq_generate_cli.py           - MCQ CLI entry point
  binary_question_cli.py        - Binary question CLI entry point
  mcq_cli.py                    - Legacy CLI

tests/
  test_mcq_generator.py         - 28 tests (PromptBuilder, QuestionGenerator, MCQGenerator)
  test_binary_question_cli.py   - 33 tests (binary CLI)
```

## Test Status

- **Total tests**: 61
- **All passing**: Yes
- **Execution time**: ~0.4s

## Key Improvements

- **Package is installable**: `pip install -e .` works; importable from anywhere
- **No sys.path hacks**: Clean relative imports throughout
- **Consistent API**: All public classes available from `mcq_generator` package
- **Clean logging**: Library code doesn't configure handlers at import time
