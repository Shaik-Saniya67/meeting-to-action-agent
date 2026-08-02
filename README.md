# 🗒️ AI Meeting-to-Action Agent

**Submission for:** AI Builders Challenge with IBM Bob — Wildcard Track (Intelligent Systems for the Future of Work)
**Built by:** Shaik Saniya

## Problem Statement
Teams lose time and accountability after every meeting: decisions go undocumented, action items get forgotten, double-assigned, or left with no owner and no deadline, and someone has to manually write follow-ups and calendar invites. Existing "AI meeting summarizer" tools stop at a text summary — they don't clarify ambiguity, flag risk, or take action.

## Solution Description
An AI agent that takes a raw meeting transcript **or audio recording** and produces a full action system, not just a summary:

- **Audio upload** — upload an .mp3/.wav/.m4a meeting recording; Gemini's native multimodal audio understanding transcribes it directly, no separate speech-to-text service needed
- **Structured minutes** — summary, topics, decisions, open questions
- **AI Clarification Agent** — flags exactly which fields are ambiguous ("Who owns this task?", "What is the expected deadline?") instead of silently guessing
- **Priority Detection with reasoning** — every action item gets a High/Medium/Low priority *and* a one-sentence explanation of why
- **Conflict Detection + AI Resolution Suggestions** — flags duplicate task ownership and contradicting decisions, then proposes a concrete, evidence-grounded resolution
- **Risk Detector** — flags risky situations proactively (unfinalized owner on a near-term deadline, unresolved blocking decisions)
- **Meeting Effectiveness Score** — a 0–100 score with a visual breakdown of what helped or hurt it (decisions taken, deadlines defined, conflicts, open questions)
- **AI Recommendations** — meeting-level next steps (sequencing, follow-ups, ownership gaps)
- **Workload Distribution** — task counts per person, with an overload warning and rebalancing suggestion
- **Execution Plan & Due Soon views** — action items automatically grouped into Today / Tomorrow / by-date buckets
- **Meeting Insights & Analytics Dashboard** — totals, completion rate, productivity, conflicts, and risks across every meeting
- **AI Chat with meeting history** — ask "who owns the dashboard?" or "what's still pending?" and get answers grounded in every saved meeting
- **Personalized follow-up emails** — one tailored email per person
- **Multi-format export** — PDF minutes, DOCX report, CSV action item list, and ICS calendar events (deadlines like "Thursday" are resolved to real calendar dates)
- **Action status tracker** — Pending / In Progress / Done, tracked across meetings
- **Shared demo key with quota guard** — judges can try the app without needing their own API key, protected by a daily generation limit

This closes the full agentic loop: **Listen → Understand → Detect → Reason → Recommend → Act → Export.**

## AI Approach & Architecture
- **Model:** Google Gemini (`gemini-flash-latest`), used with structured JSON output mode for reliable, schema-consistent extraction, and its native multimodal capability for direct audio transcription.
- **Single-pass structured extraction** captures minutes, action items (with priority reasoning and clarification flags), conflicts (with AI-generated resolution recommendations), risks, and meeting-level recommendations together — grounding every recommendation in evidence from the same transcript.
- **Deterministic post-processing in Python** resolves relative deadlines ("Thursday," "tomorrow") into absolute calendar dates using the meeting date, computes the Meeting Effectiveness Score, and groups action items into Execution Plan / Due Soon views — so scoring and date math don't depend on the LLM.
- **Storage:** SQLite, with action items tracked independently of their source meeting so dashboards reflect live status across all meetings.
- **Frontend:** Streamlit with a custom glassmorphism design system (CSS injected via `st.markdown`) — no extra frontend framework required.

## Selected Challenge Theme
Wildcard — Intelligent Systems for the Future of Work

## How IBM Bob Was Used
IBM Bob was used throughout development to assist with architecture planning, scaffolding the multi-page Streamlit UI, debugging the SQLite schema migrations, and refining the structured-output prompts for the clarification agent, priority reasoning, conflict resolution, and risk detection features.

## Tech Stack
- Python, Streamlit
- Google Gemini API (`google-generativeai`) — `gemini-flash-latest`
- SQLite
- fpdf2 (PDF export), python-docx (DOCX export), stdlib csv/datetime (CSV + ICS export)

## Local Setup
```bash
pip install -r requirements.txt
streamlit run app.py
```
Enter a free Gemini API key from [aistudio.google.com/apikey](https://aistudio.google.com/apikey) in the sidebar, or set one as a host secret (see deployment section) so visitors don't need their own.

## Demo Flow (for video)
1. Load the sample transcript (or upload a short audio clip), set the meeting date
2. Click "Generate Minutes"
3. Walk through: Meeting Effectiveness Score → Insights → action item cards with clarification flags → **conflict detected with AI recommendation** → **risk detected** → AI Recommendations
4. Show Workload Distribution and the overload warning
5. Download the PDF, DOCX, CSV, and calendar (.ics) exports
6. Open "AI Chat" and ask a question about the meeting history
7. Open "Analytics" to show cross-meeting stats

## Known Limitations
- Streamlit Community Cloud's filesystem is ephemeral — `meetings.db` and the host quota counter reset on redeploy or app restart. For a persistent hackathon-grade demo this is fine; for production use, swap SQLite for a hosted DB.
- Cross-meeting conflict detection (catching a contradiction against a *previous* meeting, not just within the current transcript) is a planned next step.

## Future Improvements
- Cross-meeting memory for conflict/contradiction detection
- Automatic meeting category classification (Project / Client / HR / Sprint Planning / etc.)
- Slack/email integration to auto-send follow-ups instead of just drafting them
