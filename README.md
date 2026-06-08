# MCQ Generation using LLM

Generating Multi-Choice Questions (MCQ) that evaluates diverse knowledge of the test takers is often
very challenging and time-consuming task. Large Language Models (LLMs) hold a promising method that can
be useful while meeting the objectives of the MCQ.

## Using the Power of AI in Question Generation

Our MCQ Generator leverages AI models including **OpenAI's GPT**, **Claude**, and **Perplexity** via the **LiteLLM** library to generate thoughtful, relevant, and challenging questions. These models allow the tool to create questions that are not only grammatically accurate but also contextually relevant, tailored to various subjects and difficulty levels.

### Key Features

#### 1. Flexible Model Selection
Choose between OpenAI, Claude, Perplexity, or any LiteLLM-supported provider.

#### 2. Customizable Question Generation
Tailor your quiz to perfection with these CLI options:
- **Field**: Subject area for question generation (required).
- **Subfield**: Optional sub-category within the field.
- **Difficulty Level**: Select from easy, medium, or hard (default: medium).
- **Number of Questions**: Choose how many questions to generate (default: 5).
- **Options per Question**: Define the number of answer choices (required, must be > 1).
- **Correct Answers**: Set number of correct answers per question (default: 1).
  - Use `0` for "None of the Above" questions
  - Use value equal to options count for "All of the Above" questions
- **Maximum Token Limit**: Adjust the token limit for LLM response (default: 3000).

#### 3. Question Types
- **Multiple Choice Questions** (MCQ) with customizable option count
- **True/False Questions**
- **Yes/No Questions**

#### 4. Comprehensive Question Analysis
For every generated question, users can:
- **Check the Correct Answer**: Instantly verify the solution.
- **Request a Detailed Explanation**: Gain insights into why the answer is correct or incorrect.
- **Access Prerequisite Knowledge**: Understand any foundational concepts needed for the question.
- **Translate the Question**: Convert the question to different languages.

## CLI Usage

The MCQ Generator provides two command-line interfaces:

### MCQ Generation
```bash
python scripts/mcq_generate_cli.py \
  --field "Physics" \
  --subfield "Mechanics" \
  --difficulty hard \
  --count 5 \
  --options 4 \
  --correct-answers 1 \
  --provider perplexity \
  --model sonar \
  --save questions.json
```

### Binary Question Generation
```bash
python scripts/binary_question_cli.py \
  --field "Biology" \
  --difficulty easy \
  --count 5 \
  --question-type true_false \
  --provider openai \
  --model gpt-4o-mini
```

### Arguments:
- `--field`, `-f` (required): Subject field for questions
- `--subfield`, `-sf` (optional): Sub-category within the field
- `--difficulty`, `-d` (default: medium): Easy, medium, or hard
- `--count`, `-c` (default: 5): Number of questions to generate
- `--options`, `-o` (MCQ only, required): Number of options per question (> 1)
- `--correct-answers` (MCQ only, default: 1): Number of correct answers per question
- `--question-type`, `-qt` (binary only, default: true_false): true_false or yes_no
- `--max-tokens` (default: 3000): Maximum tokens for LLM response
- `--provider` (default: perplexity): LLM provider (openai, claude, perplexity, litellm)
- `--model` (default: sonar): Model name specific to the provider
- `--save`: Output JSON file (auto-generated filename if not specified)

## Technical Detail

The **MCQ Generator** is built using Python with the **LiteLLM** library, providing a unified interface for multiple LLM providers. The system includes:

- **mcq_generate_cli.py** / **binary_question_cli.py**: Command-line interfaces with argument parsing and validation
- **MCQGenerator**: Core engine managing question generation and display
- **BinaryQuestionGenerator**: Generates True/False and Yes/No questions
- **QuestionGenerator**: Handles LLM API calls via LiteLLM and response parsing
- **PromptBuilder**: Creates optimized prompts with competitive exam quality rules

The system ensures content meets factual accuracy and adheres to educational best practices through comprehensive prompt engineering.

## Real-World Applications

This tool has a broad range of applications across various fields:
- **Education**: Teachers can quickly generate quizzes for assessments or homework.
- **E-Learning Platforms**: Content creators can generate quizzes that complement their online courses.
- **Corporate Training**: HR departments can create skill evaluation tests for employees.
- **Test Prep Companies**: Generate practice questions for standardized tests like SAT, GRE, etc.
- **Gamified Learning Apps**: Integrate endless MCQs into educational games for dynamic learning experiences.

## Testing

The MCQ Generator includes comprehensive unit tests covering all major components:

```bash
python -m unittest discover tests -v
```

### Test Coverage:
- **PromptBuilder**: 11 tests covering all prompt generation methods
- **QuestionGenerator**: 11 tests covering parsing and answer extraction
- **MCQGenerator**: 6 tests covering validation and display
- **Binary Question CLI**: 33 tests covering argument parsing, validation, file operations, and display
- **Total**: 61 tests

### Key Test Scenarios:
- Dynamic option generation (2-6 options)
- Multiple answer formats (comma-separated, "and", special cases)
- "All of the Above" and "None of the Above" handling
- Input validation and error handling
- CLI argument parsing and validation
- JSON file save/load operations
- Edge cases and boundary conditions
