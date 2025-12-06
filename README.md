# SideQuest 9001 - Question Database

This repository contains example question files for the SideQuest 9001 game system.

## Question File Format

Questions are stored in JSON format with support for **multilingual content**.

### File Naming Convention

Event-specific question files should be named: `{eventname}_questions.json`

Example: `hoth25_questions.json`, `summer2024_questions.json`

### JSON Structure (Multilingual)

```json
{
  "questions": [
    {
      "id": 1,
      "question": {
        "en": "What is the capital of Germany?",
        "de": "Was ist die Hauptstadt von Deutschland?"
      },
      "answer": "Berlin",
      "answerType": "text",
      "choices": ["Munich", "Berlin", "Hamburg", "Frankfurt"]
    }
  ]
}
```

### Legacy Format (Single Language)

The system also supports the legacy single-language format for backwards compatibility:

```json
{
  "questions": [
    {
      "id": 1,
      "question": "What is the capital of Germany?",
      "answer": "Berlin",
      "answerType": "text",
      "choices": ["Munich", "Berlin", "Hamburg", "Frankfurt"]
    }
  ]
}
```

### Field Descriptions

- **id** (number, required): Unique identifier for the question (1-100)
- **question** (string OR object, required): The question text
  - As string: Single language text
  - As object: `{"en": "English text", "de": "German text"}` for multilingual support
- **answer** (string OR object, required): The correct answer
  - As string: Single language answer (e.g., `"Paris"`, `"42"`)
  - As object: `{"en": "Pacific Ocean", "de": "Pazifischer Ozean"}` for multilingual answers
- **answerType** (string, required): Type of answer - `"text"`, `"number"`, or `"task"` (default: `"text"`)
- **choices** (array, optional): Multiple choice options for UI
  - Each choice can be a string or multilingual object
  - Must include the correct answer
- **numberRange** (object, optional): For `answerType: "number"` - defines min/max values: `{"min": 1, "max": 100}`
- **taskDuration** (number, optional): For `answerType: "task"` - duration in seconds (default: 300)

### Question Types

#### Text-based Multiple Choice (Multilingual)
Questions with text options that players select from.

```json
{
  "id": 1,
  "question": {
    "en": "What is the capital of Germany?",
    "de": "Was ist die Hauptstadt von Deutschland?"
  },
  "answer": "Berlin",
  "answerType": "text",
  "choices": ["Munich", "Berlin", "Hamburg", "Frankfurt"]
}
```

#### Fully Multilingual (Question, Answer, and Choices)
For answers that differ between languages:

```json
{
  "id": 8,
  "question": {
    "en": "What is the largest ocean on Earth?",
    "de": "Was ist der größte Ozean der Erde?"
  },
  "answer": {
    "en": "Pacific Ocean",
    "de": "Pazifischer Ozean"
  },
  "answerType": "text",
  "choices": [
    {"en": "Atlantic Ocean", "de": "Atlantischer Ozean"},
    {"en": "Indian Ocean", "de": "Indischer Ozean"},
    {"en": "Pacific Ocean", "de": "Pazifischer Ozean"},
    {"en": "Arctic Ocean", "de": "Arktischer Ozean"}
  ]
}
```

#### Numeric Questions (Multilingual)
Questions with numeric answers. Can have a range for validation.

```json
{
  "id": 2,
  "question": {
    "en": "What is 15 × 8?",
    "de": "Was ist 15 × 8?"
  },
  "answer": "120",
  "answerType": "number",
  "numberRange": {"min": 100, "max": 150}
}
```

#### Free Task "Questions" (Multilingual)
Questions/Tasks with custom duration. Can be skipped directly. (Cannot verify completion)

```json
{
  "id": 3,
  "question": {
    "en": "Clean the Kitchen",
    "de": "Küche aufräumen"
  },
  "answer": "done",
  "answerType": "task",
  "taskDuration": 360
}
```

## Supported Languages

The system supports any language code. Common codes:
- `de` - German (default fallback)
- `en` - English

The user's language preference is stored in their profile and the appropriate translation is shown automatically.

## Best Practices

1. **Clear Questions**: Make questions unambiguous and easy to understand
2. **Accurate Answers**: Ensure answers are factually correct
3. **Balanced Difficulty**: Mix easy, medium, and hard questions
4. **Diverse Categories**: Include variety to keep the game interesting
5. **Research Time**: Consider that players have 5 minutes to research each answer or `taskDuration` time
6. **Answer Format**: Keep answers concise and in a consistent format
7. **Provide Both Languages**: When possible, provide both `en` and `de` translations

## Limits

- Question IDs must be unique within a file
- Answer strings should be kept reasonably short (< 200 characters)
- Options array should contain 2-6 choices (4 is recommended)

## Example Files

See the example question files in this repository:
- `example_questions.json` - Basic example with various question types
- `science_questions.json` - Science-focused questions
- `trivia_questions.json` - General trivia questions
- `all_question_types.json` - Demonstration of all supported question types

## Legacy Files

Old single-language versions are preserved in the `old/` folder for reference.
