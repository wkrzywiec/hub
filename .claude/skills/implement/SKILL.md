---
name: implement
description: "Implement a ticket, spec, or set of tickets in code. Use when the user or another skill asks to implement a ticket."
---

Implement the work described by the user in the spec or tickets.

If the user passes a ticket reference, fetch it from the issue tracker and state its title before starting. If the reference is ambiguous, ask.

Before changing anything, run the repo's full test command once on the clean branch. If it cannot run (a service such as Docker is down), record that as a **Gap** and say so up front; the suite is the baseline every later run compares against.

Call the Skill tool with "tdd" where possible, at pre-agreed seams.

Run typechecking regularly, single test files regularly, and the full test suite once at the end.

Commit your work to the current branch, then call the Skill tool with "code-review" to review the commits, and commit any fixes it prompts.
