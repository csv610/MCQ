# MCQ Generator - Unit Testing Documentation

## Test Suite Overview

Comprehensive unit tests covering all major components: **61 test cases**, all passing.

## Test Organization

Tests are organized into two files:

### 1. tests/test_mcq_generator.py (28 tests)

#### TestPromptBuilder (11 tests)
Tests for prompt generation covering all question types and answer formats.

- `test_mcq_generation_prompt_single_answer`
- `test_mcq_generation_prompt_multiple_answers`
- `test_mcq_generation_prompt_zero_answers`
- `test_mcq_generation_prompt_all_answers`
- `test_mcq_generation_prompt_dynamic_options`
- `test_true_false_prompt`
- `test_yes_no_prompt`
- `test_explain_answer_prompt_with_options`
- `test_prerequisites_prompt`
- `test_similar_question_prompt`
- `test_text_translation_prompt`

#### TestQuestionGenerator (11 tests)
Tests for question parsing and answer extraction.

- `test_question_generator_initialization`
- `test_parse_question_basic`
- `test_parse_question_five_options`
- `test_parse_question_multiple_answers`
- `test_parse_question_empty_response`
- `test_parse_correct_answers_single`
- `test_parse_correct_answers_multiple_comma`
- `test_parse_correct_answers_multiple_and`
- `test_parse_correct_answers_case_insensitive`
- `test_parse_correct_answers_all_of_above`
- `test_parse_correct_answers_none_of_above`

#### TestMCQGenerationEngine (6 tests)
Tests for the MCQGenerator class.

- `test_validate_params_valid`
- `test_validate_params_valid_zero_correct_answers`
- `test_validate_params_invalid_options`
- `test_validate_params_invalid_negative_correct_answers`
- `test_display_questions_empty`
- `test_display_questions_with_data`

### 2. tests/test_binary_question_cli.py (33 tests)

#### TestValidateCliArgs (12 tests)
- Field validation (empty, None, whitespace)
- Subfield validation
- Count validation (negative, zero)
- Max tokens validation
- Question type validation
- Valid arguments pass

#### TestFormatModelId (4 tests)
- Provider/model formatting
- Existing slash format preserved
- Claude, Perplexity formatting

#### TestSetupModel (2 tests)
- Returns formatted model ID
- Prints confirmation message

#### TestSaveQuestions (6 tests)
- JSON structure correctness
- Custom and auto-generated filenames
- Multiple questions, metadata

#### TestGenerateOutputFilename (4 tests)
- Valid filename generation
- Timestamp inclusion
- Space replacement

#### TestDisplayQuestions (5 tests)
- All question components displayed
- True/False and Yes/No display
- Empty list handling
- Question count display

## Running Tests

### Run All Tests
```bash
python3 -m unittest discover tests -v
```

### Run Specific Test File
```bash
python3 -m unittest tests.test_mcq_generator -v
python3 -m unittest tests.test_binary_question_cli -v
```

### Run Specific Test Class
```bash
python3 -m unittest tests.test_mcq_generator.TestPromptBuilder -v
```

### Run Specific Test
```bash
python3 -m unittest tests.test_mcq_generator.TestQuestionGenerator.test_parse_question_basic -v
```

## Test Data

All tests use:
- **Sample questions** with realistic formats
- **Temporary directories** for file I/O tests
- **Mock objects** for LLM interaction (no API calls)
- **Various edge cases** (empty lists, invalid input, boundary conditions)

## Mock Usage

Tests use `unittest.mock` to:
- Mock LLM calls to avoid external API dependencies
- Mock file operations where needed
- Verify method calls and parameters
- Test error conditions safely

## Performance

- All 61 tests complete in **~0.4 seconds**
- Tests use temporary directories for file operations
- No actual API calls (all mocked)
- Tests are independent and can run in any order

## Test Quality Metrics

| Metric | Value |
|--------|-------|
| Total Tests | 61 |
| Passing | 61 ✅ |
| Failing | 0 |
| Success Rate | 100% |
| Execution Time | ~0.4s |

## Dependencies

Tests require only built-in modules:
- `unittest`, `tempfile`, `json`, `pathlib`, `unittest.mock`

Plus the `mcq_generator` package (installed via `pip install -e .`).
