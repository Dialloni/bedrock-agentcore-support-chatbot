# Note on Project Implementation

This submission implements the chatbot using **Amazon Bedrock AgentCore's managed
harness** rather than **Bedrock Flows**, per the course's own updated project
instructions (see "Project Instructions" and "Testing and Evaluation" pages).

Amazon Bedrock Agents Classic was closed to new customers on July 30, 2026. Since
Bedrock Flows' "Agent node" depends on Agents Classic, the course replaced this
project's architecture with the AgentCore managed harness + AgentCore Gateway
stack. The rubric text on the submission page still references the older
Bedrock Flows terminology (flow diagram, Condition node, flow-tests.json), which
does not apply to the current version of this project.

Equivalent evidence for this architecture:
- Routing logic (classification + path selection): implemented entirely inside
  `system_prompt.txt`, since the harness has no separate condition/classifier
  node — this matches the course's own Project Instructions, which state:
  "there are no condition nodes or classifiers, just instructions."
- Test suite: `harness-tests.json` (the current filename per the Testing and
  Evaluation guide, renamed from flow-tests-template.json).
- All other requirements (Gateway-invoked Lambda tool, DynamoDB persistence,
  FAQ-grounded answers, human hand-off, automated eval with Bedrock
  Evaluations/LLM-as-a-judge) are implemented and verified as shown in the
  attached screenshots and output files.

## Evaluation Results (Bedrock Evaluations, LLM-as-a-judge, Nova Pro evaluator)
- Faithfulness: 1.00 — no responses fabricated information outside the FAQ/tool results
- Correctness: 0.75
- Helpfulness: 0.665
- Refusal: 0.25 (appropriately low - model only redirected on genuinely
  out-of-scope requests)

Full per-example breakdown available in output_eval_dataset.jsonl and the
attached evaluation screenshots.
