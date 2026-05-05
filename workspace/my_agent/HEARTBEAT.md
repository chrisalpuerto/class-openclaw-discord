# HEARTBEAT

## Primary Trigger

- **Frequency**: Every 15 minutes (900,000 ms).
- **Action**: Check `#announcements` for new posts from the Instructor Agent.
- If a new post is detected, begin the discussion cycle for `#topic-discussion`.
- Light-first approach: read `#announcements` before invoking the LLM to avoid unnecessary model calls.

## Discussion Cycle

1. Detect new Instructor announcement in `#announcements`.
2. Read current thread in `#topic-discussion` to understand what peers have already posted.
3. Generate Chris Alpuerto's opening contribution using the AI Topic Knowledge Base (see TOOLS.md).
4. Post to `#topic-discussion`.
5. Continue checking `#topic-discussion` every heartbeat while the discussion is active.
6. Add follow-up contributions that deepen, challenge, or synthesize ideas already in the thread.
7. Mark the discussion cycle complete when the topic has gone quiet or a new Instructor topic replaces it.

## Guardrails

- Only activate from Instructor Agent posts in `#announcements` — not peer messages or other channels.
- Do not post into `#announcements`.
- Do not consider participation complete after a single reply if peers are still contributing.

## Rate Limit and Model Safety

- **Primary model**: `google/gemini-2.5-flash` via the Google Gemini API.
- Keep heartbeat tasks light to control token usage and avoid unnecessary provider calls.
- Do not schedule heavy background processing during the heartbeat interval.

## OpenClaw Agent Context

This heartbeat loop is managed by the OpenClaw framework. Chris Alpuerto is a configured agent in `workspace/my_agent/`. The heartbeat is the runtime mechanism that makes Chris an active, autonomous participant rather than a one-shot responder. Understanding this loop is itself relevant to class discussions on agentic AI systems.
