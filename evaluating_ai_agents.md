# Evaluating AI Agents

Community Notes from our study group, June 20, 2026

Deeplearning.ai -> [Go to course](https://www.deeplearning.ai/courses/evaluating-ai-agents)

Here's a synthesis of what the group landed on:

## Course assessment

Solid mental map for a 2-hour intro, well-organized and easy to follow, but very dense — especially Lab 2 on tracing, which felt rushed and was probably recorded before the notebook was finalized. Jupyter as a medium drew some grumbling. Concepts like "spans" need self-exploration to really stick. Useful as scaffolding for ongoing vibe-coded projects rather than a deep treatment.

### Technical takeaways

- Error handling matters more than the course emphasizes — graceful failure ("if no analysis is returned") prevents cascading breakage downstream.
- Arize Phoenix is open source; the UI for organizing traces and spans used in the course.
- OTel appears to be the de facto tracing standard — the group flagged this as worth interrogating (are there real alternatives?).
- Building the agent is the easy part; observability is where the hard problems live.
- Contained execution environments for code-running agents were flagged as under-covered — possibly addressed later, possibly feedback for future iterations.

## Open questions the group surfaced

- Should graders be application-specific rather than generic?
- Need for more robust multi-judge setups — single LLM-as-judge feels thin.
- Evals for the tools an agent calls, not just the agent's outputs.
- Sycophancy / agreeableness wasn't mentioned — is it considered irrelevant in production, or just out of scope here?
- How do you evaluate generative tasks with a wide space of valid outputs (e.g., test case generation from PRDs) beyond basic LLM-as-judge?

## Idea floated
- Releasing something as an open-source agent / project off the back of the group's exploration.
