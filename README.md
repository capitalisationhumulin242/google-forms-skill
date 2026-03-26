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

## Setup (Step-by-Step)

### Prerequisites

- **Node.js** (v18+) - [Download here](https://nodejs.org/)
- **Google Account** - Any Gmail account works

### Step 1: Install Dependencies

```bash
cd scripts
npm install
```

### Step 2: Create Google Cloud Project

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Click **Select a project** (top bar) → **New Project**
3. Name your project (e.g., `my-forms-generator`) → **Create**
4. Make sure your new project is selected in the top bar

### Step 3: Enable Google Forms API

1. Go to [APIs & Services > Library](https://console.cloud.google.com/apis/library)
2. Search for **Google Forms API**
3. Click it → **Enable**

### Step 4: Configure OAuth Consent Screen

> This step is required before you can create credentials.

1. Go to [APIs & Services > OAuth consent screen](https://console.cloud.google.com/apis/credentials/consent)
2. Select **External** → **Create**
3. Fill in:
   - **App name**: anything (e.g., `Forms Generator`)
   - **User support email**: your email
   - **Developer contact email**: your email
4. Click **Save and Continue** through Scopes and Test Users
5. On the **Test Users** page, click **Add Users** → add your Gmail address → **Save**

### Step 5: Create OAuth Credentials

1. Go to [APIs & Services > Credentials](https://console.cloud.google.com/apis/credentials)
2. Click **+ Create Credentials** → **OAuth client ID**
3. Application type: **Desktop app**
4. Name: anything (e.g., `Forms Generator`)
5. Click **Create**
6. Click **Download JSON** (or the download icon)
7. Save the file as `credentials.json` in this skill's **root directory** (same level as SKILL.md)

Your folder should look like:
```
google-forms/
├── credentials.json    ← you just added this
├── SKILL.md
├── scripts/
│   ├── create-form.js
│   └── package.json
```

### Step 6: First Run (Authorization)

The first time you run the skill, it will ask you to authorize:

1. A URL will appear in the terminal - open it in your browser
2. Select your Google account
3. You'll see **"This app isn't verified"** - this is normal for personal projects:
   - Click **Advanced**
   - Click **Go to [app name] (unsafe)**
4. Click **Continue** to grant permissions
5. Your browser will redirect to `localhost` and show an error page - **this is expected!**
6. Look at the **URL bar** of your browser. It will look like:
   ```
   http://localhost/?code=4/0AfJohX...abc123&scope=...
   ```
7. Copy everything between `code=` and `&scope` (that's your authorization code)
8. Paste it into the terminal and press Enter

Done! A `token.json` file will be saved automatically. You won't need to authorize again.

### Step 7: Install the Skill

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

## Troubleshooting

| Problem | Solution |
|---------|---------|
| `credentials.json not found` | Make sure the file is in the skill's root directory (not inside `scripts/`) |
| `401 Unauthorized` or `invalid_grant` | Delete `token.json` from the root directory and run again to re-authorize |
| `403 Forbidden` | Google Forms API is not enabled. [Enable it here](https://console.cloud.google.com/apis/library/forms.googleapis.com) |
| `ENOENT: node_modules` | Run `npm install` inside the `scripts/` directory |
| "This app isn't verified" | Normal for personal projects. Click **Advanced** → **Go to [app name] (unsafe)** |
| Browser shows "localhost refused to connect" | Expected! Copy the `code=` value from the URL bar and paste into terminal |
| `Error: No refresh token` | Delete `token.json` and re-authorize. Make sure you granted offline access |

## Tech Stack

- **Google Forms API v1** - form creation and management
- **OAuth 2.0** - authentication with token caching
- **Node.js** - runtime for the API script

## Author

**Minh Do** - [Facebook](https://facebook.com/dotanminh) | [Zalo Community](https://zalo.me/g/igkywu632)

Built with [Google Antigravity](https://blog.google/technology/google-deepmind/gemini-model-policy-updates-jan-2025/)

## License

MIT
