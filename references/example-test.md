{
  "file_type": "test",
  "purpose": "Define a single high-risk or boundary scenario with explicit pass/fail criteria, focusing on whether the skill behaves correctly under that condition.",
  "recommended_path": "tests/ambiguous-boundary-case.json",
  "test_case": {
    "name": "ambiguous-boundary-case",
    "risk": "The skill may proceed too far before required clarification, or may skip an important decision boundary.",
    "setup": {
      "user_request": "<underspecified or boundary-case request>",
      "available_context": [],
      "known_gaps": [
        "missing trigger definition",
        "missing output contract",
        "missing required input details"
      ]
    },
    "expected_behavior": [
      "Recognize that the request is underspecified.",
      "Stop before entering a later workflow stage.",
      "Ask a small set of high-information clarification questions.",
      "Avoid pretending that missing inputs are already known."
    ],
    "pass_criteria": [
      "The response explicitly identifies at least one missing prerequisite.",
      "The response asks concrete clarification questions rather than giving a generic request for more detail.",
      "The response does not produce a full downstream artifact prematurely."
    ],
    "fail_criteria": [
      "The skill invents assumptions to keep moving.",
      "The skill jumps directly into architecture, drafting, or execution without clarification.",
      "The skill responds with only vague warnings and no actionable follow-up questions."
    ]
  }
}
