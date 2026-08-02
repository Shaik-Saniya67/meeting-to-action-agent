<div align="center">

# 🗒️ AI Meeting-to-Action Agent

### Turn any meeting into decisions, owners, deadlines, and done — automatically.

*Submission for the AI Builders Challenge with IBM Bob*
**Wildcard Track — Intelligent Systems for the Future of Work**

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white)
![Gemini](https://img.shields.io/badge/Gemini_API-8E75FF?style=for-the-badge&logo=googlegemini&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-07405E?style=for-the-badge&logo=sqlite&logoColor=white)
![License](https://img.shields.io/badge/Built_with-IBM_Bob-1F70C1?style=for-the-badge&logo=ibm&logoColor=white)

</div>

---

## 💡 The Problem

Every team loses something after a meeting — a decision nobody wrote down, a task nobody officially owns, two people quietly doing the same work, a deadline mentioned once and never logged anywhere.

Most "AI meeting summarizer" tools stop at a shorter transcript. They don't ask what's missing. They don't catch contradictions. They don't tell you what to do next.

**This one does.**

---

## ✨ What It Actually Does

<table>
<tr><td width="40">🎤</td><td><b>Listens</b></td><td>Upload .mp3 / .wav / .m4a — transcribed directly via Gemini's native audio understanding. No separate speech-to-text needed.</td></tr>
<tr><td>📋</td><td><b>Understands</b></td><td>Structured minutes: summary, topics, decisions made, open questions.</td></tr>
<tr><td>⚠️</td><td><b>Asks when unclear</b></td><td>The <b>AI Clarification Agent</b> flags exactly what's missing — "Who owns this?", "What's the deadline?" — instead of silently guessing.</td></tr>
<tr><td>🔍</td><td><b>Detects</b></td><td>Priority scoring with reasoning, duplicate-ownership conflicts, contradicting decisions, and proactive risk flags.</td></tr>
<tr><td>🤖</td><td><b>Reasons</b></td><td>Every conflict gets an <b>AI-recommended resolution</b>, grounded in transcript evidence — not just "here's a problem."</td></tr>
<tr><td>⭐</td><td><b>Scores</b></td><td>A 0–100 <b>Meeting Effectiveness Score</b> with a visual breakdown of what helped and what hurt.</td></tr>
<tr><td>📅</td><td><b>Plans</b></td><td>Action items auto-sorted into an <b>Execution Plan</b> (Today / Tomorrow / by date) and a <b>Due Soon</b> view.</td></tr>
<tr><td>👥</td><td><b>Balances</b></td><td><b>Workload Distribution</b> flags overloaded teammates and suggests who to hand work to.</td></tr>
<tr><td>📤</td><td><b>Exports</b></td><td>One click → PDF, DOCX, CSV, and real calendar events (.ics) — "Thursday" becomes an actual date.</td></tr>
<tr><td>🧠</td><td><b>Remembers</b></td><td><b>AI Chat</b> answers questions like "who owns the dashboard?" grounded in your full meeting history.</td></tr>
</table>

> **The full loop:** Listen → Understand → Detect → Reason → Recommend → Act → Export
> Not a shorter transcript — an actual outcome.

---

## 🏗️ How It's Built

| Layer | Choice | Why |
|---|---|---|
| 🧠 **AI Model** | Google Gemini (`gemini-flash-latest`) | Single structured-JSON pass returns minutes, priorities, conflicts, risks, and recommendations together — grounded in one read of the transcript |
| 🎙️ **Audio** | Gemini native multimodal | No separate Whisper/STT pipeline required |
| 🧮 **Scoring & Dates** | Pure Python | Effectiveness score and deadline resolution are deterministic — stable, explainable, not left to the LLM |
| 🗄️ **Storage** | SQLite | Action items tracked independently, so dashboards reflect live status across *every* meeting |
| 🎨 **Frontend** | Streamlit + custom CSS | Glassmorphism design system — built to look like a real product, not a prototype |
| 🔑 **Demo Access** | Host-side shared key + daily quota guard | Judges can try it instantly, no API key required |

---

## 🛠️ Tech Stack

```
Python · Streamlit · Google Gemini API (gemini-flash-latest)
SQLite · fpdf2 · python-docx
```

## 🏆 Challenge Theme
**Wildcard — Intelligent Systems for the Future of Work**

## 🤝 How IBM Bob Was Used
IBM Bob supported the build throughout — architecture planning, scaffolding the multi-page Streamlit interface, debugging the SQLite schema as it evolved, and refining the structured-output prompts behind the clarification agent, priority reasoning, conflict resolution, and risk detection.

---

## 🚀 Running It Locally

```bash
pip install -r requirements.txt
streamlit run app.py
```

Enter a free Gemini API key from [aistudio.google.com/apikey](https://aistudio.google.com/apikey) in the sidebar — or set one as a host secret so visitors don't need their own.

---

## 🎬 Demo Walkthrough

| Step | Action |
|---|---|
| 1️⃣ | Load the sample transcript, or upload a short audio clip |
| 2️⃣ | Click **Generate Minutes** |
| 3️⃣ | Walk through the Effectiveness Score → action items → a clarification flag → a conflict with its AI recommendation → a detected risk |
| 4️⃣ | Show **Workload Distribution** and the overload warning |
| 5️⃣ | Download a PDF, a DOCX, and a calendar file |
| 6️⃣ | Open **AI Chat** and ask a real question about the meeting |
| 7️⃣ | Open **Analytics** to show it working across multiple meetings |

---

## 🔮 What's Next

- 🔗 **Cross-meeting memory** — catch a contradiction even when it spans two different meetings
- 🏷️ **Auto meeting categorization** — Project / Client / HR / Sprint Planning
- 📨 One-click email delivery — send the drafted follow-up and personalized emails straight to all meeting participants using SMTP or an email service API, instead of just copying them out
- 📨 **Direct Slack/email integration** — send follow-ups automatically instead of just drafting them

---

## 📌 A Note on Storage

> Streamlit Community Cloud's filesystem is temporary — the meeting database and daily quota counter reset on app restart or redeploy. Perfectly fine for a hackathon demo; for production, swap SQLite for a hosted database.

---

<div align="center">

**Built with 🗒️ + 🤖 for the AI Builders Challenge with IBM Bob**

</div>
