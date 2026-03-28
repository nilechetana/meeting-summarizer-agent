# 🤖 AI Meeting Summarizer Agent

An autonomous AI agent that reads meeting transcripts, extracts decisions and action items, and automatically sends a formatted summary email — with zero manual effort.

---

## 🚀 Setup Instructions

### 1. Install Dependencies
```bash
pip install -r requirements.txt
```

### 2. Get Your Free Gemini API Key
- Go to: https://aistudio.google.com/app/apikey
- Click "Create API Key"
- Copy the key

### 3. Set Up Gmail App Password
- Go to your Google Account → Security → 2-Step Verification → App Passwords
- Generate a password for "Mail"
- Copy the 16-character password

### 4. Set Environment Variables
```bash
# Windows
set GEMINI_API_KEY=your_gemini_api_key
set SENDER_EMAIL=your_gmail@gmail.com
set SENDER_PASSWORD=your_16char_app_password
set RECIPIENT_EMAIL=recipient@gmail.com

# Mac/Linux
export GEMINI_API_KEY=your_gemini_api_key
export SENDER_EMAIL=your_gmail@gmail.com
export SENDER_PASSWORD=your_16char_app_password
export RECIPIENT_EMAIL=recipient@gmail.com
```

### 5. Run the Agent
```bash
python agent.py
```

---

## 📁 Project Structure
```
meeting-summarizer-agent/
├── agent.py              # Main agentic pipeline
├── transcript.txt        # Meeting transcript input
├── requirements.txt      # Dependencies
├── src/
│   └── email_sender.py   # Gmail email module
└── README.md
```

---

## 🔄 How It Works

```
transcript.txt
      ↓
Step 1: Load transcript
      ↓
Step 2: Gemini AI analyzes & extracts structured data
        (decisions, action items, owners, deadlines, blockers)
      ↓
Step 3: Format beautiful HTML email
      ↓
Step 4: Send via Gmail SMTP automatically
```

---

## ✨ What the Agent Extracts
- Meeting title, date, attendees
- Key decisions made
- Action items with owner, deadline, and priority (High/Medium/Low)
- Blockers and risks
- 2-3 sentence overall summary
