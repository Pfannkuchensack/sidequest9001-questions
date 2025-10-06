# SideQuest 9001 - Question Database

This repository contains example question files for the SideQuest 9001 game system.

## Question File Format

Questions are stored in JSON format with the following structure:

### File Naming Convention

Event-specific question files should be named: `{eventname}_questions.json`

Example: `hoth25_questions.json`, `summer2024_questions.json`

### JSON Structure

```json
{
  "questions": [
    {
      "id": 1,
      "question": "Your question text here?",
      "answer": "correct answer",
      "answerType": "text",
      "choices": ["option1", "option2", "option3", "option4"]
    }
  ]
}
```

### Field Descriptions

- **id** (number, required): Unique identifier for the question (1-100)
- **question** (string, required): The question text
- **answer** (string, required): The correct answer
- **answerType** (string, required): Type of answer - `"text"` or `"number"` (default: `"text"`)
- **choices** (array, optional/required): Multiple choice options for UI. If provided, must include the correct answer
- **numberRange** (object, optional/required): For `answerType: "number"` - defines min/max values: `{"min": 1, "max": 100}`

### Question Types

#### Text-based Multiple Choice
Questions with text options that players select from.

```json
{
  "id": 1,
  "question": "What is the capital of Germany?",
  "answer": "Berlin",
  "answerType": "text",
  "choices": ["Munich", "Berlin", "Hamburg", "Frankfurt"]
}
```

#### Numeric Questions
Questions with numeric answers. Can have a range for validation.

```json
{
  "id": 2,
  "question": "What is 15 × 8?",
  "answer": "120",
  "answerType": "number",
  "numberRange": {"min": 100, "max": 150}
}
```

#### Free Task "Questions"
Questions/Task with custom needed duration. Can be skiped directly. (Cannot check whether it has been completed)

```json
{
      "id": 3,
      "question": "Clean the Kitchen",
      "answer": "done",
      "answerType": "task",
      "taskDuration": 360
    },
```

## Best Practices

1. **Clear Questions**: Make questions unambiguous and easy to understand
2. **Accurate Answers**: Ensure answers are factually correct
3. **Balanced Difficulty**: Mix easy, medium, and hard questions
4. **Diverse Categories**: Include variety to keep the game interesting
5. **Research Time**: Consider that players have 5 minutes to research each answer or `taskDuration` time
6. **Answer Format**: Keep answers concise and in a consistent format

## Limits

- Question IDs must be unique within a file
- Answer strings should be kept reasonably short (< 200 characters)
- Options array should contain 2-6 choices (4 is recommended)

## Example Files

See the example question files in this repository:
- `example_questions.json` - Basic example with various question types
- `science_questions.json` - Science-focused questions
- `trivia_questions.json` - General trivia questions
