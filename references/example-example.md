{
  "file_type": "example",
  "purpose": "Demonstrate how the skill should handle a representative request, with emphasis on handling path and response style rather than pass/fail verification.",
  "recommended_path": "examples/representative-handling.json",
  "example": {
    "name": "representative-handling",
    "input": {
      "user_request": "<representative but non-edge-case request>",
      "available_context": [
        "<optional file>",
        "<optional prior user note>",
        "<optional constraint>"
      ]
    },
    "expected_handling": [
      "Identify the task type before acting.",
      "Use the stated source hierarchy instead of inventing missing facts.",
      "Follow the default workflow in the intended order.",
      "Preserve the expected level of detail and structure in the response."
    ],
    "response_style": {
      "tone": "structured, calm, direct",
      "format": "nested bullets",
      "verbosity": "concise but information-dense"
    },
    "target_output_shape": {
      "sections": [
        "task understanding",
        "key decisions",
        "result"
      ],
      "must_include": [
        "explicit handling path",
        "clear final deliverable"
      ],
      "must_avoid": [
        "unbounded brainstorming",
        "unsupported claims",
        "irrelevant side quests"
      ]
    }
  }
}
