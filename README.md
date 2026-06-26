# Practice: Adding Memory

⌨️ In this practice task, you'll implement episodic and semantic memory for the PR Review Agent and verify each one.

## **👩‍💻 Workflow at a glance**

1. Set up your environment
2. Implement episodic memory
3. Test episodic memory
4. Implement semantic memory
5. Test semantic memory
6. Check your work
7. Submit

## 1. Set up your environment

Keep working in `building-your-mobile-agent` repo. 

## 2. Implement episodic memory

Episodic memory is a record of past runs — an append-only log. Add this instruction to the `## Guardrails` section of your project rules file:

```
After every completed review (whether or not the user confirms posting), append one line to `review_history.md`:
YYYY-MM-DD | PR-[number] | [top finding short description] | [severity]
Example: 2026-05-15 | PR-03 | Hardcoded API token in PaymentService | HIGH
```

## 3. Test episodic memory

Run `/review-pr 1`, `/review-pr 2`, and `/review-pr 3` in three separate sessions. Then ask:

```
Based on review_history.md, what finding type has highest severity?
```

## 4. Implement semantic memory

Semantic memory is a knowledge base the agent searches when it needs reference material. 

First, give the agent something to search. Use the `docs/adr/` section of your practice repo.

### ADR files

```
docs/
└── adr/
    ├── ADR-001-mvvm.md
    ├── ADR-002-networking-stack.md
    └── ADR-003-repository-pattern.md   ← PR-04 violates this one
    └── ADR-004-dependency-injection.md
    
```

Then add this instruction to `agents/architecture-reviewer.md`'s system prompt:

```
Before reporting any architecture finding, search docs/adr/ using Grep for keywords
related to the pattern you observed. If you find a matching ADR, cite it:
"[MEDIUM] ViewModel calls API directly — violates ADR-003 (Repository Pattern)"
If no ADR matches, report the finding without a citation.
```

## 5. Test semantic memory

Run `/review-pr 4`.

Verify: 

- [ ]  The architecture-reviewer reports the repository-layer violation
- [ ]  Its output cites an ADR number (ADR-003)

### Tip

If the ADR citation doesn't appear, verify that the files are at `docs/adr/` in the root of your practice repo (open the folder in your IDE to confirm) and that the Grep instruction is in the architecture-reviewer's system prompt.

## 6. Check your work

- [ ]  `review_history.md` has at least three entries
- [ ]  `docs/adr/` is in place
- [ ]  The `/review-pr 4` run produced an architecture finding that cites an ADR number

## 7. Submit

- Commit your changes.
- Push to GitHub.
- Return to the lesson and click "Submit."
