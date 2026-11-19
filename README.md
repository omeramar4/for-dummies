# for-dummies

A skill for Claude Code (and other agent-skill tools) that explains anything clearly: concepts, code, errors, systems.

Every answer has the same shape: **one-sentence answer, analogy, concrete example, diagram, common mix-up, recap.**

## Try it

```
/for-dummies what is a database index?
/for-dummies this stack trace
/for-dummies Rust ownership familiar
/for-dummies Raft leader election fluent
/for-dummies
```

The last one, with no topic, explains whatever was just discussed. Follow up with `simpler` or `deeper` to move a level.

Plain phrases also trigger it: "ELI5", "in simple terms", "I don't get it". If you installed it as a plugin, the command is `/for-dummies:for-dummies`.

## What you get

Prompt: `/for-dummies what is an API?`

---

**An API is a menu that lets one program ask another program to do something, without knowing how it works inside.**

**Analogy: a restaurant.** You (the app) don't walk into the kitchen. You read the menu (the API's list of allowed requests), tell the waiter (the API) what you want, and the kitchen (the server) cooks it. You get a plate back (the response).

```mermaid
sequenceDiagram
    participant App as You (the app)
    participant API as Waiter (the API)
    participant Server as Kitchen (the server)
    App->>API: "One weather report for Paris, please"
    API->>Server: Look up Paris weather
    Server-->>API: 18°C, cloudy
    API-->>App: {"city": "Paris", "temp": 18}
```

**Example.** A weather app asks `GET /weather?city=Paris`. The reply is a small bundle of data, `{"city": "Paris", "temp": 18}`. The app never sees the weather company's database.

**Common mix-up.** Not "an API is a website". It's a doorway for programs; a website is a doorway for people.

**Why it matters.** Apps can borrow features (maps, payments, weather) instead of rebuilding them.

**In short**
- An API = a menu of requests a program is allowed to make.
- You ask, it answers; the inside stays hidden.

**Check yourself:** In the restaurant story, what is the "menu"? *(The list of requests the API accepts.)*

*Level: newcomer. Say "deeper" for more detail.*

---

## Features
- **Three levels:** `newcomer` (default, zero background), `familiar` (you know the basics or a neighbouring field), `fluent` (internals, edge cases, trade-offs). Picked from how you ask; never asks you.
- **A diagram that fits the topic:** flowchart, sequence diagram, table or chart. Mermaid where it renders, ASCII in a terminal.
- **End-to-end examples** for multi-step workflows: one input followed from start to finish.
- **Your code, not a generic version**, when you point at something in your project.
- **The common mix-up** at your level, in one line.
- **Follow-ups:** "simpler" gets a different analogy, not the same one again.

## Install

**Claude Code plugin**
```
/plugin marketplace add omeramar4/for-dummies
/plugin install for-dummies@for-dummies
```

**Any skills-compatible agent**
```
npx skills add omeramar4/for-dummies
```

**Manual**
```
git clone https://github.com/omeramar4/for-dummies && cp -r for-dummies/skills/for-dummies ~/.claude/skills/
```

## Contributing
Open an issue with a topic where the explanation missed. The best fixes are one-line rule changes in `skills/for-dummies/SKILL.md`.

## License
MIT
