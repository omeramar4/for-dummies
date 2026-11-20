---
name: for-dummies
description: Explain a concept, code, error, or system clearly, with a one-sentence answer, a real-life analogy, a concrete example, and a small diagram. Use when the user says "for dummies", "explain like I'm 5", "ELI5", "in simple terms", "dumb it down", "I don't get it", "explain this to a beginner", asks for a beginner-friendly explanation, or asks for an explanation at a named level (newcomer, familiar, fluent), e.g. "I know Python but not Rust, explain ownership" or "explain Raft at fluent level".
argument-hint: "<topic> [newcomer|familiar|fluent]"
---

# For Dummies

## Purpose
Explain the topic so the reader understands it on the first read, at the level they need.

## Inputs
- **Topic** (optional): what to explain, from the arguments or the user's message. If none is named (bare `/for-dummies`, "I don't get it"), explain the last thing discussed.
- **Level** (optional): `newcomer`, `familiar` or `fluent`. A level word in the arguments sets it; otherwise it is inferred as described below.

## Examples
```
/for-dummies what is a database index?
/for-dummies Rust ownership familiar
/for-dummies Raft leader election fluent
/for-dummies
```
Plain phrases work too: "ELI5 this stack trace", "I know Python but not Rust, explain ownership".

## Pick the level
The level describes how much the reader already knows **about this topic**. Default is **newcomer**.

| Level | Reader | What changes |
|---|---|---|
| **newcomer** (default) | Never met the topic ("ELI5", "for dummies", "I don't get it") | Everyday words, every term defined where it first appears, analogy required, one new idea at a time. For "ELI5" go simpler still: no jargon at all. |
| **familiar** | Knows the basics or a neighbouring topic ("I use Git but not rebase", "I know Python, new to Rust") | Skip definitions they already know. Anchor on what they know ("like Python's `with`, but..."). Analogy optional. Focus on *how it works* and *when to use it*. |
| **fluent** | Works in the field, wants the real picture ("expert", "deep dive", "the actual mechanism") | No analogy, no hand-holding. Precise terms, internals, edge cases, trade-offs, failure modes. Say what the simple version leaves out. |

Choose by, in order: an explicit request ("familiar level", "explain as fluent"), then clues in how the user phrased the question, then newcomer. Never ask which level. End with one short line naming the level used, so the user can ask to go up or down.

## Instructions
Use these parts in this order. Skip any part that doesn't add understanding.

1. **One-sentence answer first.** Say what it is or what it does before any detail.
2. **Real-life analogy** (required for newcomer, optional for familiar, skipped for fluent). Compare it to an everyday situation (restaurant, post office, library, traffic, kitchen...). Map the parts explicitly: "the waiter = the API, the kitchen = the server". Say where the analogy breaks if that could mislead.
3. **Concrete example.** A small, specific walk-through with real numbers or names, or a tiny code snippet for code topics. Go step by step. For a multi-step workflow or system (a deploy pipeline, a login flow, a request through several services), make it end-to-end: follow one concrete input from start to finish, saying what happens at each stage and what comes out.
4. **Diagram, when it helps.** Pick the shape that fits:
   - steps or decisions -> flowchart
   - who talks to whom, in what order -> sequence diagram
   - comparing things ("X vs Y") or defining terms -> markdown table
   - change over time, size, trade-offs -> small chart
   - parts of a whole, nesting -> indented tree or boxes

   Use Mermaid only where it will render (a chat app, GitHub, a markdown file being written). In a plain terminal, or if unsure, draw it in ASCII: raw Mermaid code is noise to a newcomer. Label every box and arrow in the reader's words, max ~8 nodes. If the UI can show richer visuals (an artifact or HTML preview) and the topic is truly spatial or interactive, you may offer a one-file HTML explainer after the text answer; never make the reader wait for it.
5. **Common mix-up.** If people at this level usually get something wrong, say the wrong belief and the fix in one line ("Not X. It's actually Y."). For fluent, this is the subtle pitfall, not the beginner mistake.
6. **Why it matters.** One or two sentences: what problem it solves. Skip for fluent.
7. **In short.** 2-3 bullets recap.
8. **Check yourself (optional).** One question that tests understanding, with the answer on the next line. Use for concepts, skip for errors and for fluent.

## Special cases
- **Error message:** what it means, the most likely cause, the fix, in that order. Analogy only if the cause is conceptual.
- **"X vs Y":** lead with the one-sentence difference, then a table, then when to pick each.
- **Code or an error in the current project:** read the relevant code first and explain *that* code with its real names, not a generic version.
- **Follow-ups:** "simpler" or "still don't get it" -> drop one level (or, at newcomer, use a *different* analogy and a smaller example; never repeat the same explanation louder). "Deeper" or "more detail" -> go up one level and skip what was already covered.

## Rules
- Short sentences, everyday words. Jargon only at the level that already speaks it.
- Build up from what the reader already knows; one new idea at a time.
- One strong analogy beats several weak ones.
- Visuals support the words, never replace the one-sentence answer. One clear visual beats several busy ones.
- Short. Simple doesn't mean long.
- Accurate: simplify, never say something false. If a simplification hides an important caveat, add it in one line.

## Limitations
- Mermaid diagrams only render in some interfaces; the ASCII fallback is less precise.
- Every analogy breaks somewhere, and a simplified answer can hide caveats. The skill flags the important ones, not all of them.
- For code in the current project, the explanation is only as good as the code that was read.
