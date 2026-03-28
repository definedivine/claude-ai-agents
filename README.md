# Claude Web App Agent System

A five-agent workflow for building web apps and landing pages with Claude in a way that feels structured, reviewable, and much more human-made.

This repository contains the agent definitions I use when building demo apps and tools at brainylab. Each agent has a clear role, hard rules, handoff boundaries, and documentation responsibilities. The goal is simple: stop treating Claude like a magic box and start treating it like a system.

Instead of one giant prompt that generates a wall of code, this setup breaks work into stages:

**INA designs → RON reviews → BEN builds → RON reviews again → QUINN tests**

When something breaks or behaves strangely, **DEX** steps in to diagnose the issue before anyone starts randomly changing files.

## What this repo includes

- **BEN**. Builder agent. Plans first, builds second, documents everything. fileciteturn0file2
- **INA**. Front-end and visual design agent. Creates a distinct visual system and refuses generic AI-looking UI. fileciteturn0file4
- **RON**. Reviewer and gatekeeper. Reviews plans, code, security, architecture, and design integrity. fileciteturn0file0
- **QUINN**. QA agent. Runs functional, visual, responsive, accessibility, SEO, and performance checks before final handoff. fileciteturn0file1
- **DEX**. DevOps and diagnostics agent. Finds root causes, documents evidence, and creates a fix plan before BEN touches anything. fileciteturn0file3

## Why this exists

Most AI-assisted builds go wrong for the same reason. The model starts coding too early, makes hidden assumptions, loses context between sessions, and produces something that technically works but feels generic, fragile, and hard to continue later.

This system solves that by enforcing a few non-negotiables:

- clear ownership per agent
- documented handoffs
- no skipped review steps
- no silent architecture changes
- no visual patching by the wrong agent
- session notes and milestone documentation for every work cycle

If you only work on side projects occasionally, this matters even more. Context loss is real. The documentation layer is what makes the system reusable.

## The five agents

### 1. BEN. The Builder

BEN writes code, but only after producing a written plan. He reads the docs, maps affected files, explains architectural decisions, lists risks, then stops for review. Only after review and approval does he build. He also maintains documentation, milestone summaries, and conventional commits. fileciteturn0file2

**BEN is responsible for:**
- implementation
- modular file structure
- milestone checkpoints
- project documentation
- conventional commits

**BEN never:**
- starts building before review
- skips RON
- hardcodes secrets
- leaves undocumented architecture decisions

### 2. INA. The Design Agent

INA owns the look, feel, motion, visual identity, and front-end design system. Her job is not just to make things pretty. Her job is to make the result feel intentionally designed by a human.

She starts by choosing one aesthetic direction, then creates design tokens before touching components. She uses strong layout variation, visual rhythm, purposeful motion, and a strict anti-pattern checklist to avoid the usual AI-generated UI clichés. fileciteturn0file4

**INA is responsible for:**
- visual direction
- design tokens
- layout patterns
- motion and interaction design
- structured image placeholders
- anti-pattern avoidance

**INA never:**
- ships generic templates
- uses default Tailwind colors as final brand colors
- repeats the same section pattern everywhere
- skips reduced-motion support

### 3. RON. The Reviewer

RON is the gatekeeper. He reviews BEN's plans before they are built, reviews code at milestones, and checks security, architecture, and design integrity. He is specifically there to stop weak work from slipping through just because everyone wants to move faster. fileciteturn0file0

**RON is responsible for:**
- plan review
- code review
- security review
- architecture validation
- design integrity checks
- security review log maintenance

**RON never:**
- rubber-stamps output
- approves work that fails the checklist
- lets BEN override INA's visual decisions
- says “we’ll fix it later” and moves on

### 4. QUINN. The QA Agent

QUINN is the final automated gate before human review. She runs structured QA across functionality, visuals, motion, copy, images, SEO, performance, responsive behavior, and accessibility. Her output is always a structured QA report with passed checks, failed checks, severity, verdict, and fix routing. fileciteturn0file1

**QUINN is responsible for:**
- functional QA
- responsive QA
- visual system validation
- Lighthouse and performance checks
- metadata and SEO checks
- accessibility basics

**QUINN never:**
- passes placeholder content
- ignores console errors
- skips mobile checks
- reports PASS when critical issues still exist

### 5. DEX. The DevOps Diagnostic Agent

DEX exists for the moments when the project is broken, slow, or misconfigured. She does not fix the issue herself. She diagnoses first, cites evidence, finds the root cause, and creates a prioritized fix plan. Only then does the issue go through review and back to implementation. fileciteturn0file3

**DEX is responsible for:**
- build and config diagnosis
- performance bottleneck analysis
- architecture-level diagnostics
- dependency and environment checks
- diagnostic reports with evidence and verification steps

**DEX never:**
- guesses
- patches code blindly
- hands fixes directly to BEN without review

## How the system works

The value is not in the prompts individually. The value is in the order.

### Standard build flow

1. **You define the task**
2. **INA** defines the visual direction and front-end system
3. **RON** reviews the design direction and constraints
4. **BEN** creates a written implementation plan
5. **RON** reviews the plan
6. **BEN** builds in milestones
7. **RON** reviews milestone output
8. **QUINN** runs QA before final handoff
9. **You** decide what gets published

### When something breaks

1. **DEX** diagnoses the issue
2. **RON** reviews the diagnostic report
3. **BEN** implements the approved fix
4. **QUINN** verifies the result if needed

## Expected project stack

These agents were written for a modern web app workflow built around:

- Next.js 14+
- TypeScript
- Tailwind CSS v4
- Framer Motion / motion
- Vercel-style deployment workflows

That does not mean you cannot adapt them. It just means the prompts, checks, and terminology are optimized for this stack. fileciteturn0file1turn0file3turn0file4

## Repository structure

This repo can stay simple:

```txt
.
├── ben-builder-agent.md
├── ina-frontend-design-agent.md
├── ron-reviewer-agent.md
├── quinn-QA-agent.md
├── dex-devops-agent.md
└── README.md
```

For every project where you use these agents, I recommend a matching docs structure like this:

```txt
project/
├── agents/
│   ├── ben-builder-agent.md
│   ├── ina-frontend-design-agent.md
│   ├── ron-reviewer-agent.md
│   ├── quinn-QA-agent.md
│   └── dex-devops-agent.md
├── docs/
│   ├── PRD.md
│   ├── architecture.md
│   ├── STYLE_GUIDE.md
│   ├── ina-anti-patterns.md
│   ├── security-review-log.md
│   └── session-notes/
└── src/
```

The agents assume those docs exist. If they do not, the system becomes weaker immediately.

## Installation

This repo does not install a standalone app. It gives you a reusable agent system.

### 1. Clone the repo

```bash
git clone https://github.com/your-username/your-repo.git
cd your-repo
```

### 2. Add the agent files to your Claude project or Claude Code workflow

Use each `.md` file as the system prompt or role definition for a dedicated agent/skill inside your Claude setup.

How you do this depends on your exact Claude workflow, but the idea is always the same:

- one file = one agent
- one agent = one role
- shared project docs = shared context
- strict handoffs = predictable output

### 3. Create the required project documentation

Before asking BEN or INA to do real work, prepare the minimum docs:

- `docs/PRD.md`
- `docs/architecture.md`
- `docs/STYLE_GUIDE.md`
- `docs/ina-anti-patterns.md`
- `docs/security-review-log.md`
- `docs/session-notes/`

These are not optional if you want the system to work properly.

### 4. Start with the correct agent

Use the right entry point for the task:

- starting a new interface or landing page. start with **INA**
- planning and implementation. move to **BEN** after review
- reviewing plans or code. call **RON**
- validating a milestone or pre-release build. call **QUINN**
- investigating slow builds, broken configs, or weird runtime issues. call **DEX**

## Recommended usage

### For a new app or landing page

1. Write a short brief or PRD
2. Ask **INA** to define the aesthetic direction and visual system
3. Send INA’s output to **RON** for review
4. Ask **BEN** to produce an implementation plan
5. Send the plan to **RON**
6. After approval, let **BEN** build in milestones
7. Route milestone output back through **RON**
8. Run **QUINN** before you publish anything

### For an existing app that needs improvements

1. Update the docs first
2. Ask **BEN** for a scoped plan
3. Route the plan through **RON**
4. Let **INA** handle any visual changes
5. Let **BEN** handle logic and integration
6. Run **QUINN** on the affected scope

### For broken or slow projects

1. Ask **DEX** to diagnose the issue
2. Review DEX’s report through **RON**
3. Let **BEN** implement the approved fix
4. Re-run **QUINN** if the fix impacts the UI or behavior

## Important operating rules

These rules are what make the system useful.

- **BEN plans before building**. Always. fileciteturn0file2
- **INA owns visual decisions**. BEN wires functionality, not design. fileciteturn0file0turn0file4
- **RON reviews before things move forward**. Review is not ceremonial. fileciteturn0file0
- **QUINN is the last automated gate before human review**. fileciteturn0file1
- **DEX diagnoses before anyone starts fixing**. fileciteturn0file3
- **Documentation is part of the work**. Not a cleanup step at the end. fileciteturn0file2turn0file3turn0file4

## What gets documented

A big part of this system is continuity between sessions.

At minimum, projects should keep:

- implementation plans
- milestone summaries
- security review notes
- QA reports
- diagnostic reports
- session notes in `docs/session-notes/YYYY-MM-DD.md`

This is what allows you to stop work, come back later, and continue without rebuilding the whole context from memory.

## Who should use this

This repo is useful if you:

- build web apps or landing pages with Claude
- want stronger design output, not generic templates
- want a repeatable workflow instead of one giant prompt
- care about code review, QA, and documentation
- work in bursts and need context preserved between sessions

It is probably not for you if you want a one-click site generator with no process.

## Final note

These agents are not the point on their own. The system is the point.

One prompt can generate code. A good workflow can generate momentum, continuity, and much better outcomes.

If you use this setup, adapt it to your own stack, your own review standards, and your own taste. But keep the boundaries. That is where most of the value comes from.
