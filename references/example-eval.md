{
  "file_type": "eval_set",
  "purpose": "Provide a repeatable, comparable set of prompts for regression checking across versions of the skill.",
  "recommended_path": "evals/stage-routing.json",
  "eval_set": {
    "name": "stage-routing",
    "target": "<skill-or-bundle-name>",
    "items": [
      {
        "id": "brief-001",
        "prompt": "<request that should trigger clarification or briefing behavior>",
        "expected_traits": [
          "recognizes_missing_information",
          "asks_for_clarification",
          "does_not_jump_to_late_stage"
        ]
      },
      {
        "id": "architect-001",
        "prompt": "<request that should trigger architecture or module-selection behavior>",
        "expected_traits": [
          "classifies_problem_structure",
          "discusses_module_selection",
          "does_not_jump_to_full_draft"
        ]
      },
      {
        "id": "draft-001",
        "prompt": "<request that includes a ready plan and should trigger drafting behavior>",
        "expected_traits": [
          "uses_existing_plan",
          "produces_file_oriented_output",
          "stays_within_defined_scope"
        ]
      }
    ],
    "scoring_focus": [
      "correct stage routing",
      "trait consistency across runs",
      "regression visibility after prompt or structure changes"
    ]
  }
}
