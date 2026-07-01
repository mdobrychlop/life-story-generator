# Life Story Generator

A synthetic personal dataset generator powered by Google Gemini. Given a time range, it produces a coherent, day-by-day personal record for a fictional person: daily to-do lists, journal entries, and informal notes, where the story develops consistently across months, complete with goals, setbacks, habits, and life events.

Originally built for the [Google – Gemini Long Context competition](https://www.kaggle.com/competitions/gemini-long-context/overview) on Kaggle.

## What it does

The generator uses a four-step LLM pipeline, where each step feeds structured context into the next:

1. **Profile generation** - creates a fictional person with occupation, family, goals, habits, and personality traits
2. **Full story arc** - plans the character's overall progression across the entire defined timespan (monthly bullet points covering fitness, career, personal development, and two multi-month plot lines)
3. **Monthly breakdowns** - expands each month into a day-by-day outline, grounded in the full arc
4. **Daily records** - generates detailed daily entries in week-sized batches, each chunk receiving context from the previous week

The output is a JSON file containing the full profile followed by a dated record for every day in the timespan.

```json
{
    "GENERAL_PROFILE": {
        "name": "Seraphina Jones",
        "age": 28,
        "details": "* Occupation: Marine Biologist\n* ..."
    },
    "DAILY_RECORDS": {
        "October 1, 2020": "**Tasks for Today:**\n- ...",
        "October 2, 2020": "..."
    }
}
```

## Key concepts

- **Prompt chaining** - each generation step receives the outputs of all previous steps as context, keeping the narrative consistent across a long timespan
- **Context window management** - daily records are generated in weekly chunks to stay within token limits while preserving short-term continuity
- **Structured output parsing** - responses are formatted with XML-style tags and parsed with retry logic, a practical pattern for reliable structured output from LLMs
- **Synthetic data generation** - the resulting dataset is suitable for testing long-context retrieval, RAG pipelines, or personal assistant applications

## Stack

- Python, Jupyter Notebook
- Google Gemini API (`gemini-1.5-flash`)
- Kaggle Secrets (for API key management in the notebook environment)

## Usage

The notebook is hosted on Kaggle and can be run directly there: [life-story-generator on Kaggle](https://www.kaggle.com/code/mateuszdobrychlop/life-story-generator).

To run it locally or elsewhere, replace the `UserSecretsClient` key retrieval with your own API key and install the dependency:

```bash
pip install google-generativeai
```

Then set your key and run the cells in order. The timespan and profile constraints are configurable at the top of each step.

---

*Part of a broader set of LLM-based tools. See my other repositories for more advanced work with RAG pipelines and AI agents.*
