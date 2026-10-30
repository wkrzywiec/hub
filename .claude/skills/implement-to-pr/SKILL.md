---
name: implement-to-pr
description: "Implement a ticket end to end and open a PR against main/master, with open concerns noted on the PR. Usage: /implement-to-pr <#issue>"
argument-hint: "<#issue>"
disable-model-invocation: true
---

Take the ticket from `$ARGUMENTS` to an open pull request without stopping to ask. The user reviews the PR afterwards, so every doubt goes onto the PR instead of into a question.

The ticket is assumed ready to implement.

## Steps

1. **Resolve the repo.** This workspace is the hub, so run git and `gh` inside the one project repo the ticket belongs to. If `git rev-parse --show-toplevel` is the hub, find the repo from the ticket or `$ARGUMENTS`. Ask only if it stays ambiguous, since there is nothing to review yet.

2. **Branch.** Detect the base (`main`, else `master`). Branch off its tip as `<issue-number>-<short-slug>`; the number in the name lets `pr-description` link the issue. Reuse the branch if you are already on one for this ticket.

3. **Implement.** Call the Skill tool with `implement` and the ticket reference. While it runs, keep a running **concerns list**, each entry one line with the file or decision it concerns:
   - **Assumption**: anything unclear in the ticket where you picked an interpretation instead of asking.
   - **Finding**: each `code-review` finding left unfixed. Fix the unambiguous ones first.
   - **Gap**: failing or skipped checks, untested paths, work left out.

4. **Push and open the PR.** Push the branch, then `gh pr create --base <base> --head <branch> --title "<ticket title>" --body "<one line>"`. The PR opens even with a non-empty concerns list or red checks. If the branch has no commits ahead of base, stop and say so.

5. **Describe.** Call the Skill tool with `pr-description`. It finds the open PR and replaces the placeholder body.

6. **Post concerns.** With a non-empty concerns list, write it to a temp file and run `gh pr comment <number> --body-file <file>`. Group by Assumption, Finding, Gap, phrased as decisions the user must confirm or fix. With an empty list, skip the comment.

7. **Report.** Give the PR URL and the concerns count.
