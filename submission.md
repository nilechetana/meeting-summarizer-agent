# CSTE Assignment Submission
## AI Meeting Summarizer + Action Item Agent

---

## 1. Problem Statement

### What problem were you trying to solve?

After every team meeting, someone has to manually go through the entire conversation, figure out what was decided, who is responsible for what, and then write and send a summary email to everyone. This process is:

- **Time-consuming** — it can take 20–30 minutes after every meeting
- **Inconsistent** — different people summarize differently, things get missed
- **Delayed** — summaries often arrive hours after the meeting, causing confusion
- **Error-prone** — action items get lost, deadlines are forgotten, no one follows up

In fast-moving teams, this is a real productivity killer. Important decisions get buried in chat history, and accountability suffers because nobody has a clear record of who owns what.

### Why did you choose this problem?

This problem is universal — every team, in every company, in every industry has meetings. The pain is real and immediate. I chose it because:

1. It has a clear, measurable impact (time saved, accountability improved)
2. It is a perfect use case for an AI agent — it requires reading, understanding, reasoning, and taking action
3. The output (a formatted email) is easy to demo and visually impressive
4. It showcases the full agentic loop: **Input → Understand → Decide → Act**

---

## 2. Approach & Thought Process

### How did you break down the problem?

I broke the problem into a 4-step autonomous pipeline:

**Step 1 — Input:** Load the raw meeting transcript from a text file. In a real-world scenario, this could come from Zoom, Google Meet, or Microsoft Teams transcription APIs.

**Step 2 — Understand (AI Brain):** Send the transcript to Google Gemini AI with a carefully engineered prompt that instructs it to extract structured data — decisions, action items, owners, deadlines, priorities, and blockers — and return it as clean JSON.

**Step 3 — Format:** Take the structured JSON and transform it into a professional, color-coded HTML email with tables for action items, priority indicators, and a clear summary section.

**Step 4 — Act:** Autonomously send the email via Gmail SMTP without any human intervention.

The key insight was treating each step as a **distinct agent responsibility** — the AI doesn't just summarize, it reasons about priority, assigns ownership, and identifies risk. That's what makes it agentic rather than just a simple summarizer.

### What made your approach unique or different?

Most meeting summarizers just produce a text summary. My agent goes further:

- **Assigns priority levels** (High / Medium / Low) to each action item based on context
- **Identifies blockers** — things that could stop the project from moving forward
- **Structures output as actionable data** (JSON), not just prose
- **Takes autonomous action** — sends the email without waiting for human approval
- **Color-coded email** — High priority items appear in red, making it scannable at a glance

The prompt engineering was critical. Instead of asking Gemini to "summarize the meeting," I gave it a strict JSON schema to fill in, which made the output reliable and parseable every time.

---

## 3. Tech Stack

| Layer | Tool | Why |
|-------|------|-----|
| Language | Python 3.11 | Most powerful for AI/agent workflows |
| AI Model | Google Gemini 1.5 Flash | Free tier, fast, excellent at structured extraction |
| Email | Gmail SMTP (smtplib) | Free, no external service needed |
| Data Format | JSON | Structured, reliable, easy to parse |
| Input | Plain text (.txt) | Simple, universally compatible |

### Agentic / Automation Tools Involved

- **Google Gemini API** — the reasoning brain of the agent
- **Prompt Engineering** — structured JSON schema prompting for reliable output
- **Autonomous Email Dispatch** — agent takes action without human input
- **Pipeline Architecture** — each step feeds into the next automatically

### Why Free Tools?

I deliberately chose tools with free tiers to prove that powerful agentic workflows don't require expensive infrastructure. The entire stack costs $0 to run.

---

## 4. Build Explanation

### How does your solution work?

The agent is triggered by running a single command:

```bash
python agent.py
```

From that point, it operates fully autonomously:

1. **Loads** `transcript.txt` — the raw meeting conversation
2. **Calls Gemini AI** with an engineered prompt that extracts:
   - Meeting metadata (title, date, attendees)
   - Key decisions made during the meeting
   - Action items with owner, deadline, and priority
   - Blockers or risks identified
   - A 2-3 sentence executive summary
3. **Parses the JSON** response from Gemini
4. **Builds an HTML email** with:
   - A summary section
   - A decisions list
   - A color-coded action items table (red = High, orange = Medium, green = Low)
   - A blockers section highlighted in red
5. **Sends the email** via Gmail SMTP automatically

### Key Features

- **Zero human intervention** after triggering — fully autonomous end-to-end
- **Structured extraction** — not just a paragraph summary, but organized, actionable data
- **Priority intelligence** — the AI infers priority from context (e.g., "critical bug" = High)
- **Professional HTML output** — the email looks like it was written by a human assistant
- **Extensible** — easy to swap transcript source (Zoom API, Google Meet, etc.) or output channel (Slack, Notion, etc.)

### Project Structure

```
meeting-summarizer-agent/
├── agent.py              ← Main agentic pipeline (4-step autonomous workflow)
├── transcript.txt        ← Meeting transcript input
├── requirements.txt      ← Single dependency (google-generativeai)
├── src/
│   └── email_sender.py   ← Gmail SMTP module
└── README.md             ← Setup instructions
```

---

## 5. Why This Matters

### What makes this project meaningful?

**Immediate real-world value:** Every team has this problem. This agent could save 20–30 minutes per meeting, per team. For a company with 50 teams having 3 meetings per week, that's 150+ hours saved weekly.

**It demonstrates true agentic behavior:** The agent doesn't just answer a question — it reads, reasons, decides, and acts. It completes a full workflow that previously required a human. That's the essence of what makes AI agents powerful and different from simple chatbots.

**It's a foundation, not a ceiling:** This project can be extended to:
- Pull transcripts directly from Zoom or Google Meet APIs
- Post summaries to Slack channels
- Create Jira/Trello tickets for each action item automatically
- Track action item completion over time
- Send reminder emails as deadlines approach

**It showcases prompt engineering as a skill:** The reliability of the agent depends entirely on how well the prompt is designed. Getting Gemini to return consistent, parseable JSON every time required careful schema design and instruction — a skill that is increasingly valuable in AI development.

### Personal Reflection

What I'm most proud of is the simplicity of the final solution. The entire agent is under 100 lines of Python. Yet it performs a task that would take a human 20–30 minutes, in under 10 seconds. That ratio — minimal code, maximum impact — is what good engineering looks like.

This project also changed how I think about automation. The question is no longer "can a computer do this?" but "what is the right way to structure the problem so an AI agent can handle it reliably?" That shift in thinking is what agentic development is really about.

---

## 6. Loom Video Outline (5–10 minutes)

**Suggested structure for your recording:**

1. **(0:00 – 1:00)** — Introduce yourself and the problem. Show a real example of a messy meeting chat and explain the pain point.

2. **(1:00 – 2:30)** — Walk through the project structure. Open each file and explain what it does in 1-2 sentences.

3. **(2:30 – 4:00)** — Show the transcript.txt file. Explain that in production this would come from Zoom/Meet APIs.

4. **(4:00 – 6:00)** — Run the agent live: `python agent.py`. Show the terminal output step by step.

5. **(6:00 – 8:00)** — Open the email inbox and show the received summary email. Highlight the action items table, priority colors, and blockers section.

6. **(8:00 – 9:30)** — Explain your thought process: why you chose this problem, why Gemini, why JSON schema prompting.

7. **(9:30 – 10:00)** — Talk about what you'd build next (Zoom API integration, Slack output, Jira ticket creation).

---

*Submitted by: [Your Name]*
*Date: July 2025*
