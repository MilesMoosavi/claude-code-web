---
description: Enforce a sentence limit on all responses. Supports dynamic N via argument (e.g., /sentence-limit 2). Default is 1 sentence.
argument-hint: [N]
---

# Sentence Limit Protocol

The user invoked this with: $ARGUMENTS

## Rules
1. **Dynamic Limit**: Every non-code response must be exactly **N** sentences, where N is the argument provided (e.g., `/sentence-limit 2`).
2. **Default**: If no number is specified, default to exactly **one sentence**.
3. **Compound Sentences**: Use semicolons or conjunctions sparingly; prioritize high-density statements.
4. **No Meta-Talk**: No filler, pleasantries, or status updates.
5. **Code Exemption**: Code blocks and inline code comments are exempt.
6. **Automatic Restatement**: On invocation, immediately restate the preceding response using the specified limit, without meta-commentary.
7. **Persistence**: Stays active for the remainder of the session unless the user says "stop sentence limit" or "normal mode".
