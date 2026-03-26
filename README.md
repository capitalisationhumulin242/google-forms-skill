# Google Forms Generator Skill

An [Antigravity](https://blog.google/technology/google-deepmind/gemini-model-policy-updates-jan-2025/) / Claude Skill that creates Google Forms from **any content** - Word documents, text files, or just a topic description.

No fixed input format required. Just tell the AI Agent what you need, and it handles everything.

## How It Works

```
You: "Create a customer satisfaction survey"
Agent: Analyzes → Generates questions → Calls Google Forms API → Returns form link
```

### Supported Question Types

| Type | Description |
|------|------------|
| Short text | Single-line answer |
| Paragraph | Multi-line answer |
| Radio | Single choice |
| Checkbox | Multiple choice |
| Dropdown | Dropdown select |
| Scale | Linear scale (1-5, 1-10, etc.) |
| Date | Date picker |
| Time | Time picker |
| Section | Page break with title |

## Setup

### 1. Google Cloud Credentials

1. Create a project at [Google Cloud Console](https://console.cloud.google.com/)
2. Enable [Google Forms API](https://console.cloud.google.com/apis/library/forms.googleapis.com)
3. Go to **APIs & Services > Credentials > Create Credentials > OAuth client ID**
4. Select **Desktop app**, download JSON
5. Save as `credentials.json` in this repo's root directory

### 2. Install Dependencies

```bash
cd scripts
npm install
```

### 3. Install the Skill

Copy the `google-forms/` folder into your Antigravity/Claude skills directory:

```
.agents/skill/google-forms/
```

## Usage

Just talk to your AI Agent naturally:

- "Create a registration form for my marketing workshop"
- "Turn this document into a Google Form survey"
- "Build a feedback questionnaire for our team"
- "Make a quiz about Vietnamese history"

The Agent reads the SKILL.md, understands your request, generates appropriate questions, and creates the Google Form automatically.

## Example Output

```
=== Google Form Created ===
Title: Workshop Registration
Questions: 7
Total items: 9

Form URL: https://docs.google.com/forms/d/e/.../viewform
Edit URL: https://docs.google.com/forms/d/.../edit
```

## Tech Stack

- **Google Forms API v1** - form creation and management
- **OAuth 2.0** - authentication with token caching
- **Node.js** - runtime for the API script

## Author

**Minh Do** - [Zalo Community](https://zalo.me/g/igkywu632)

Built with [Google Antigravity](https://blog.google/technology/google-deepmind/gemini-model-policy-updates-jan-2025/)

## License

MIT
