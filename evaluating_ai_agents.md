# Evaluating AI Agents

Community Notes from our study group, June 20, 2026

Deeplearning.ai -- [Go to course](https://www.deeplearning.ai/courses/evaluating-ai-agents)

Evaluation in the time of LLMs
1. categorizes evaluation scope between LLM Model and LLM System
2. analogues with traditional software testing
3. some metrics listed; a comprehensive list might be useful for future studies
4. "even small changes can cause performance regressions"

Decomposing agents
1. simpler router = better & more consistent performance, but narrower capabilities - evaluation could helps close the gap
2. splitting up tasks into two (or more) simpler tasks/calls is recommended compared to completing one more complex, difficult task

Lab 1
1. table printed in the small jupyter notebook embedded in the platform could be hard to read as table categories increase (column shifts etc.)
2. good idea to remove prefixes added by the model (SQL, python) and just keep runnable code, e.g. `code = code.replace("```python", "").replace("```", "")`; although seems to fail in the output for the last cell??
3. keep agents in contained environments when giving them ability to run code - need to be able to test this
4. modifying router entries is an interative feedback process to improve model capability
5. notebooks are high-level, easy to understand but limited in hands-on approach; use seems to depends from person to person

Course seems to be well-organized so far.

Lab 2
1. a bit rushed, too information dense, will have to revisit

Adding router and skill evaluations
1. code-based evals especially useful to compare ground truth data with application output
2. eval templates in LLM-as-a-judge example should be human-evaluated first before letting a separate eval LLM use it as a source-of-truth (training/tuning)
3. graders should be application-specific rather than generic
