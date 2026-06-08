# get-lazy-with-agents-clinic

```
> Take a step back: when was the last time something really surprised you?
```

When you work with AI agents, genuinely surprising yourself is often **one right question away**. The reason: a specific slice of humanity's knowledge, finely tuned to your question, can spark your imagination.

So the only question left is:
**How do you ask the right question?**

AI agents are **the most powerful question-answering machines ever invented**. If now isn't the time to start figuring out the right questions, I don't know what is.

---

Here are 5 questions that might be the first steps onto the road:

```sh
1. "help me figure out what I really want and it might be different from what I ask: ... " # "make the model run on an HPC"
2. "help me design a process of working with you for ..." # "keeping my field notes in order"
3. "interview me until you are 98% sure what I want and how to do it: ..." # generate an ODD protocol for my model
4. "give me a meta-frame for: ..." # "building a house in the forrest"
5. "what are the best questions to ask in order to understand how ..." # "LLMs work"
```
## What is this clinic about?

> The [first edition](https://github.com/comses-education/get-lazy-with-llms-clinic) of this clinic was about **how to use LLMs effectively**, focused mainly on **better prompting techniques**.
>
> This edition is about how to go from installing an AI agent to **making it do useful work for you**.
>
> We focus on **designing a way of working with AI agents** that works around **current human and AI limitations**, with the goal of **mutual amplification**. We prioritize deriving from first-principles over coverage.
>

Pick your comfort level for working with AI agents:

- **Level 1:** **Solve tasks directly**, through free-form communication with your agent.
- **Level 2:** Before solving a task, **design the process for solving it**. What you build takes the form of one or more agent skills, or a plugin. The worked example is [odder](https://github.com/comses/odder) — an installable Claude Code skill that, when invoked walks you through the process of generating an [ODD protocol](https://www.jasss.org/23/2/7.html) for an agent-based model of your choice.
- **Level 3:** **Design a process designer** — a process that designs processes, producing a custom process for any task. What you build is, again, one or more agent skills or a plugin. The worked example produces [`skills/process-designer/`](skills/process-designer/) — an installable Claude Code skill that, when invoked on a future task of yours, walks you through producing a process that solves your task with AI agents. The build is documented end to end at [`examples/process-designer/walkthrough.md`](./examples/process-designer/walkthrough.md).

## Prerequisites for this clinic:

- **Get an agent.** Common ones: [Claude Code](https://claude.ai/), [gemini CLI](https://geminicli.com/), [codex](https://openai.com/codex/), [hermes-agent](https://hermes-agent.nousresearch.com/), [opencode](https://opencode.ai/), [pi.dev](https://pi.dev/), etc.
- **Pick a task.** *Refactor a legacy function. Summarise a research paper. Design a database schema. Draft. Plan a renovation.*
- [agents-101](./guides/agents-101.md) - everything you need to know about what an agent is, what it can do and how to control it

## Recommended read
- Every prompt has a prompt behind it: [Hierarchical Prompt Generation Framework](./guides/hpg.md)


> **A note on Claude Code.** This clinic references Claude Code throughout, but the reasoning is agent-agnostic. Agents differ on surface — syntax, command names, hook formats, skill packaging — and converge on the same principles for working around human and AI limits.

# Level 1: Your agent is quite powerful out of the box.
When using an LLM through a chat interface:

```sh
1. "here is my code: <buggy_code.py>. find the bug."
2. copy answer from browser
3. paste answer to your computer
```

When using an agent:
```sh
"@buggy_code.py fix the bug and rerun the test suite" # @ usually appends the content of a file or folder to the context
```

You see the difference.

Ask your agent:
```sh
"what can you do?"
"what tools do you have?"
"what skills do you have?"
"what are your limitations?"
"how do I use you most efficiently for X?"
"what are the best questions to ask in order to explore your limitations and ways to work around them?"
```
If you are not an expert in AI agents, the last question taps into your known or unkonwn unkonws. This is the magic moment: you acquire domain knowledge stored in the LLM's weights — tapping into the knowledge of humanity, if you will...

### Get a *meta-frame* for your task

You write:
```sh
"Draft the abstract for my paper."
```

The agent produces something. Plausible. Often misses what your target journal expects.

You write instead:
```sh
"What are the parts of an abstract for my target journal? In what order?
What's the word limit? What does an editor scan for before forwarding to reviewers?"
```

The agent gives you a *meta-frame* — reusable for every abstract you draft from here on.

### Brittle prompts, reliable skills

A handcrafted prompt is like a hand-made car: brittle, not scalable in production. A skill created with the [`/skill-creator` skill](https://github.com/anthropics/skills/blob/main/skills/skill-creator/SKILL.md) is a stamped car: robust, repeatable. You can even evaluate your skills.

Don't handcraft a prompt. Use the `/skill-creator` skill to design a skill that reliably executes your task. **This is programming in English.**

### Create an Agent Skill

Ask your agent:
```sh
"create a skill that does X"
```

If you're using claude-code, the [`/skill-creator` skill](https://github.com/anthropics/skills/blob/main/skills/skill-creator/SKILL.md) will be automatically invoked and the agent will guide you through the process of creating a skill that you can later use to do your tasks. For example `/marker-converter` is a skill that I use to convert pdf files on my computer using [marker-pdf](https://github.com/datalab-to/marker) like this:

```sh
"/marker-converter extract all images from the first 3  pages of this pdf"
```

You can create such a skill yourself.
Ask your agent:

```sh
"create a skill that uses https://github.com/datalab-to/marker to convert pdfs. Make sure to use all image extraction features of the library."
```

Once your agent is done, you should have a working skill your agent can use.

---

If you are new to agents, I recommend to close this guide and work with agents on your own tasks. Come back when you start hitting problems like:
```
- agent outputs slop
- agent doesn't follow important instructions
- agent is failing to retrieve existing information
- ...
```
---
# Why Human+AI collaboration fails?

### 1. Human constraints:
1. Bound cognition
2. Scarce time
3. Unknown unknowns

### 2. Agent/LLM constraints:
1. Context size
   1. limited work can be done in an agent session
   2. limited content can be added to the context
2. Knowledge cut-off, Field churn
3. Confident ≠ correct (hallucinations)
4. Non-determinism
5. Security exposure

### 3. Systemic constraints:
1. mutual unverifiability - you never know what the agent "understands" and vice versa.

# The Process: Human+AI collaboration

In this repository, a **process** means:

>**all the interactions between a human and one or more AI agents while working toward a goal.**

This is the central subject of everything that follows.


Examples of processes:

```sh
"I want a process for synthesising a literature review across many papers on the same topic."

"I want to design, build, deploy and operate a digital library"

"I want to renovate my house"
```

A process is or is not:

- interactive
- multi-session
- long-running
- with side effects
- idempotent
- shared
- collaborative
- distributed
- scheduled
- recurrent
- updatable
- ...

In later sections we will use our AI agent to help us design **a process** that doesn't fail.

# Process Goal: Mutual Amplification

## What humans are good at

- **Intent** — know what they want, and why it's worth wanting.
- **Intuition** — feel that something's wrong before they can explain why.
- **Decision-making** — commit when the trade-off is real and no option is clean. *Latency or maintainability — which matters today?*
- **Domain Taste** — tell elegant from merely correct. *A beautiful proof versus a brute-force one.*
- **Stakes awareness** — know what a failure costs, who it hits, and how reversible it must be.

## What AI agents are good at

- **Language** — catch what you meant from a half-formed prompt, and hand you the words you didn't know you were missing.
- **Code, structure & patterns** — a formal special case of language: see the pattern, grasp the structure.
- **Tool use** — chain many tools toward a goal without being told each step.
- **Parallel context** — you hold four-to-seven things in your head; an agent holds the whole 500-page spec.
- **Coverage** — you sample a few points; it covers the space. Edge cases you'd never list; ten variants where you'd manage two.
- **Domain knowledge** — fluent across many domains
- **Tireless thoroughness** — checks line 4,832 as carefully as line 7.

We want to design the **Human+AI collaboration process** to compensate for the weaknesses and amplify the strengths of both:

>**Whenever a human is doing what an agent could do, given the right context, it's not mutual amplification.**

# Process Methods: design against constraints

Each method routes around one or more constraints. Methods stack: a stubborn constraint may need two. The methods don't eliminate constraints — they make them manageable.

## Human | Bound cognition ⟶ `simplify`

A picture you read in seconds beats a spec you'd slog through for an hour.

```sh
"explain as if I am 5-years-old"
"draw a mermaid sequence diagram of the auth handshake"
"render the data flow as a mermaid flowchart — one node per transform"
"build a single-page interactive site to step through the model's behavior, parameter by parameter"
```

## Human | Scarce time ⟶ `delegate the task end-to-end`

You review the diff, not the loop.

Design a closed loop: give the agent full context, authority limits, a stopping condition. Don't give it implicit assumptions or anything irreversible.

```sh
"implement the function for X. The existing test is the spec.
Stop when tests pass. Do not change the test."
```

## Human | Unknown unknowns ⟶ `interview, meta-frame`

Unknown unknowns and mutual unverifiability — same move: surface silent premises before acting on them. Aim for 98% understanding. Surface the meta-frame.

```sh
"before drafting, interview me until you're 98% sure you understand the task.
Name my silent assumptions and yours.
Premortem: imagine this has already failed — why?
Invert: what would make this go wrong?"
```

Minutes spent here. The work that follows lands.

## Agent | Huge context ⟶ `decompose`

One omnibus prompt fits neither working memory nor context. Identify the **Parts** of the meta-frame; run them as separate prompts.

```sh
# instead of:
"review my entire grant application"

# decompose:
"review the Specific Aims for clarity and feasibility"
"review the Methodology for reproducibility"
"review the Budget for justification gaps"
```

Each part: one input, one output, one checkable result.


## Agent | Session Limit: Hitting session limit? ⟶ `compact` or `handoff document`

A session approaches its context limit, the agent starts generating slop, but you haven't finished your work yet.

- use the `/compact` skill - the agent replaces your entire session with an auto-generated summary
- you ask the agent to `"write a handoff document"`

The difference between the 2 methods is subtle and depends on the nature of your work.
Use a handoff document when you need the exact source files to be loaded in the context to continue work:

```sh
# end of session:
"write HANDOFF.md: what we did, what's next, what's decided, what's open.
Be terse and specific. Include file paths."

# next session:
"@HANDOFF.md continue the work."
```


## Agent | Context Limit: A side-quest from the main session? ⟶ `sub-agents`

Exploration eats the main context. A sub-agent has its own fresh context window.

```sh
"spawn a sub-agent: find every file that imports X. Return paths only."
"spawn 3 sub-agents: try three approaches to Y. Return tradeoffs only."
"spawn 5 sub-agents: read these five papers. Extract methods sections only."
```

The parent reads the summary; the noise stays in the child. Bad fit for back-and-forth tasks — keep those in the parent. Spawn N at once for wall-clock speed.

## Agent | Context Limit: Polluted context? ⟶ `progressive disclosure`

You might have extensive documentation in your project.
Usually not all this documentation is needed at the same time.
Layer it — short index up front, details fetched only when the task reaches them. Agents can follow references in your documents.

```sh
"what is this project about?" # agent reads a small CLAUDE.md at the root of the repo by default

# then it might read deeper depending on what you ask
"how does the authentication module work?" # agent reads src/modules/auth/README.md

# it will not read individual tool schemas if there is enough information in the index
"list deferred tools"             # agent reads .../tools/index.md - tool names + one-line descriptions
"fetch schema for X"              # full input/output right before invoking .../tools/X/schema.json
```

## Agent | Knowledge cut-off or field churn ⟶ `research`

The training cutoff is in the past. The field changes quarterly. Memory of an API is a guess.
Anything that touches an API, or a public service, or the agent itself — research it first.

```sh
"web-search the current Claude Code hooks schema. Cite official docs. Write findings to refs/hooks-2026-05.md."
"research your own capabilities from the official docs and save them in refs/agent-capabilities.md"
```

## Agent | Confident ≠ correct (hallucinations) ⟶ `verify`

LLM fluency reads as confidence. Confidence is not evidence.

```sh
"all tests pass"                # → run them yourself, instruct the agent to run the tests
"citation X supports claim Y"   # → read the source, instruct another agent to verify each claim
"I checked the docs"            # → check the docs, instruct another agent to cite the docs
```

Better: a Stop hook that refuses *done* until the test command exits 0.


## Agent | Non-determinism ⟶ `evaluate`

A single output is a draw from a distribution, not a measurement. To measure: N draws, criteria, a score.

```sh
"run @prompts/literature-search.md 10 times against the same criteria.
Score each output 0-10 for relevance. Output: prompt | mean | std."
```

Without the eval, you can't tell which variant moves 6/10 to 8/10.

## Agent | Security ⟶ `hooks`

The agent cannot police itself — prompts can be ignored, talked around, hijacked. Hooks sit below the model and intercept every tool call. Gate your agent actions at the harness layer. Configuration, not prompts; nothing for the agent to talk around.

```sh
# PreToolUse:  refuse `rm -rf` unless confirm.txt exists
# PreToolUse:  block `git push --force` to main
# Stop:        refuse "done" until pytest exits 0
# PostToolUse: log every write/shell/network call
```

For anything that touches files, the network, or shared infrastructure — write a hook before you write a prompt.

# Level 2: Putting it all together: odder - a process example

[Here](https://github.com/comses/odder) is an example of an interactive, multi-session process that generates an [ODD Protocol](https://www.jasss.org/23/2/7.html) for an agent-based model.

The [ODD generation process](./examples/odder/odder-execution.md) follows a 4-step process with each step triggered manually:
```sh
/odd-interview .   # Phase 1: interview + source files exploration
/odd-plan          # Phase 2: generate instrucstions for ODD protocol generation
/odd-draft         # Phase 3: generate draft ODD protocol
/odd-check         # Phase 4: verify ODD draft and generate a verification report
```
If you have a lot of context, we recommend one step per agent session. After each step, artifacts are generated by the agent and should be reviewed by the human. This catches hallucinations or cognitive drift early.

As you might have noticed the [ODD generation process](./examples/odder/odder-execution.md) is packaged as a [claude plugin](https://code.claude.com/docs/en/plugins). Different agent providers will have their conventions, but in its essence, this is a bundle of agent skills.

The plugin itself was also [generated](./examples/odder/odder-process.md) by an AI agent.



## Exercise: "Design a process to do X"

Think of a process you want to do right now.
Attach this file to your prompt and ask your agent:

```sh
"
@README.md

I want to design a process for Human+AI collaboration for X.
Interview me until you're 98% sure you understand the process and know what to do.
"
```

You can go to the next level only if you find yourself tweaking the prompt above for different processes that you design. Otherwise you do not need it.

# Level 3: design a process designer

If you find yourself designing many processes for yourself or other people, or producing many variants of a process based on some parameters, you'll keep asking the same meta-frame questions:


```
- what is a process?
- what parts does a process designer consist of?
- what steps must every process designer have, regardless of the use case?
- ...
```

These are the same meta-frame questions a Meta²-Prompt from the [Hierarchical Prompt Generation Framework](./guides/hpg.md) must answer to generate a process designer.

In this section we build a `/process-designer` skill:

```sh
/process-designer "I want a process for generating the ODD protocol for any agent-based model in social science."
/process-designer "I want a process for synthesising a literature review across many papers on the same topic."
/process-designer "I want to renovate my house. I want an AI agent to keep track of progress and guide me through the entire process: from the basement to the roof."
```

Let's start building:

```sh
"
@README.md

I want to design a process-designer process.
Interview me until you're 98% sure you understand the process and know what to do.
"
```
We attach this `README.md` file to give the agent some context to think from.
After a few back and forth iterations, we settle on a set of features:

1. grounded in current agent capabilities using web search
2. adapt the process to user's cognitive level
3. interview with user about the dimensions of the process
4. design the process (pick the right methods, tie to constraints, produce a process that agent(s) follow);
5. split design and installation in 2 separate skills

Your set of features might differ, but the core will be similar.
During back and forth with the agent following **process dimensions** emerge:

| Dimension | Method it dials | Turned low → turned high |
|---|---|---|
| **Reversibility** | Hooks | no hooks → hooks block every dangerous action, plus a "never without confirmation" list |
| **Domain distance** | Research | trust the model's knowledge → fetch a source before any claim |
| **Iteration cost** | Evaluate | ~20 eval cases, iterate freely → a few cases, a hypothesis before each run |
| **Autonomy** | Hand off | approve every step → high-trust default, only the non-negotiables gated |
| **Memory horizon** | Session hand-off | nothing persists → a notes/decisions layer reloaded each session |
| **Parallelism** | Sub-agents | one agent, one conversation → sub-agents in parallel, keep the best |

The goal of the interview with the user is to gather individual dials for the process we're designing.

After 1 design session, 1 build session and several iterations on obvious mistakes, we have two installable Claude Code skills:

1. [`/process-designer`](./skills/process-designer/SKILL.md) — interviews you about your task, then stages your process files in a `process-designer-output/` folder.
2. [`/process-installer`](./skills/process-installer/SKILL.md) — reads that output and installs it into your project: surveys conflicts, scaffolds the runtime files, verifies the install.

The full build is retrospectively documented in the [walkthrough](./examples/process-designer/walkthrough.md)

## Exercise: install and run `/process-designer`

### Install both skills in a new process folder
1. Create a folder where your process will live - your process folder
2. Install the skills: `npx skills add comses-education/get-lazy-with-agents-clinic` or copy them into your `.claude/skills` folder
3. Launch your agent in the process folder

If you don't have a use case at hand, you can test-drive the process-designer with:

```sh
# Step 1 - design your process

/process-designer "I'm developing a NetLogo agent-based model of opinion polarisation in a small online community. I work on it across weeks, calibrating parameters against survey data. I want the agent to help me modify model code, run parameter sweeps, generate the ODD protocol documentation, and produce reproducible analysis scripts."
```
Five stages run in order — capability discovery, interview (~10 min), synthesis, verification, refinement loop — and the artifacts land at `process-designer-output/` for you to inspect.

Then:

```sh
# Step 2 - install your process into the process folder
/process-installer
```
```sh
# Step 3 - run your new process. depending on your prompt you might have different skills available

/calibrate
/parameter-sweep
/analyze
...
```

# The End. Are we done now?

Not quite. You created a new folder for your process, ran `/process-designer` to create and `/process-installer` to install your process  — congratulations! You've taken the first step toward **making your agent do meaningful work for you.** Each time you start a session in your process folder, the agent should be able to understand your process, know what state it's in, and talk to you about it in a meaningful way.

But the work isn't done, because:
- agents hallucinate and don't always follow your instructions
- LLM context windows aren't always big enough
- edge cases slip past your instructions
- some instructions turn out too prescriptive, others too vague
- etc.

You're stepping into an iteration loop: every time the agent misbehaves, you note it and fix it in the process definition (skills) files. This is how your agent gets better.

# Where this repo's limits are and where to look next

This clinic prioritizes principles over coverage. This is a short list of topics for the curious:

**Adjacent dimensions the clinic doesn't cover:**

- **Memory layer** — persistent semantic/episodic memory, auto-memory systems, vector stores, structured journals. We only show session hand-off (write a doc), the cheapest form. Anything with retrieval, eviction, or cross-process recall is out of scope.
- **Domain-specific process atoms** — programming has its own vocabulary (specs, spikes, silver bullets, ATDD, code review, refactor patterns); research has lit-review/citation/replication; ops has incident response/runbooks; legal has review/redline. We teach general process design without going too deep into domain atoms.
- **Cost & latency design per step** — model routing (Opus vs Sonnet vs Haiku per step), prompt caching, latency budgets, sync vs async. The methods stay model-agnostic; tuning lives elsewhere.
- **Process lifecycle** — versioning a process, sharing/publishing, discovery, eval-driven evolution. We end at "the process runs"; not "the process gets better over time." - This is a step that can be added as part of the process itself, but is out of scope here.
- **Reasoning patterns inside one step** — chain-of-thought, tree-of-thought, reflection loops, self-consistency, confidence calibration. The first edition touches prompting; we treat the step as a black box.
- **Reliability patterns** — failure recovery, checkpointing, idempotent retry, partial-progress resume. We name *idempotent* as a process property but don't show how to build for it.
- **Multi-human collaboration on one process** — team handoff, review workflows, role separation, shared scratchpads. We assume one human + agent(s).
- **Knowledge ingestion / corpus grounding** — RAG patterns, corpus curation, citation provenance. We say `@file` and stop.

**Where to look:**
- [Orchestrate subagents at scale with dynamic workflows](https://code.claude.com/docs/en/workflows)
- Harness Engineering:
  - [Continuous Claude v3](https://github.com/parcadei/Continuous-Claude-v3)
  - [Continuous Claude v4.7](https://github.com/parcadei/ContinuousClaudeV4.7)
  - [Anthropic Harness design for long-running application development](https://www.anthropic.com/engineering/harness-design-long-running-apps)
- Memory:
  - [Anthropic memory tool](https://platform.claude.com/docs/en/agents-and-tools/tool-use/memory-tool)
  - [mem0](https://github.com/mem0ai/mem0)
  - [Letta](https://github.com/letta-ai/letta)
- Spec-driven development:
  - [GitHub Spec Kit](https://github.com/github/spec-kit)
  - [spec-kitty](https://github.com/Priivacy-ai/spec-kitty)
  - [openspec](https://github.com/Fission-AI/OpenSpec)
- Cost & latency:
  - [Anthropic models overview](https://platform.claude.com/docs/en/about-claude/models/overview)
  - [Prompt caching docs](https://platform.claude.com/docs/en/build-with-claude/prompt-caching)
- Process lifecycle & eval-driven iteration:
  - [skill-creator skill](https://github.com/anthropics/skills/blob/main/skills/skill-creator/SKILL.md) - Anthropic's canonical skill-builder.
- Reasoning patterns:
  - [Anthropic prompt engineering docs](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview)
- Reliability:
  - [Temporal for AI](https://temporal.io/solutions/ai)

**This clinic's lineage:**

- [First edition: get-lazy-with-llms-clinic](https://github.com/comses-education/get-lazy-with-llms-clinic) — focused on prompting.
- [Hierarchical Prompt Generation Framework](./guides/hpg.md) — every prompt has a prompt behind it.