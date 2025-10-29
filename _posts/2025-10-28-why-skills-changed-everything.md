---
layout: post
title: "Why Skills Changed Everything: My Journey with Superpowers"
date: 2025-10-28
categories: claude-code ai-development superpowers
---

# Why Skills Changed Everything: My Journey with Superpowers

## Opening: The Meta-Aggregation Context

The Claude Code ecosystem builds elegant layers. APIs aggregate into MCPs. MCPs aggregate into skills. Skills aggregate into plugins. Plugins aggregate into marketplaces.

A beautiful abstraction.

But understanding the architecture changes nothing. **Discovering which layer solves your problem changes everything.**

Skills changed mine—specifically, the [superpowers marketplace](https://github.com/obra/superpowers-marketplace). Skills changed how I think about building with Claude Code.

## The Skill Stack as a System

Skills force you to think differently. They create **decision checkpoints**.

Three skills matter most: **brainstorm**, **write-plan**, and **requesting-code-review**—and how they work together.

- **Brainstorm** forces clarity before code: What problem am I solving? What alternatives exist? What do I want?
- **Write-plan** converts clarity into a structured roadmap any model can execute
- **Requesting-code-review** creates a validation gate where Codex or Haiku verifies work against the original intent

The **delegation model** makes this powerful: You brainstorm with full context, plan at high level, hand off implementation to Haiku (who executes without overthinking), and bring Codex in for thinking-heavy review. Each model does what it does best.

Before superpowers, I held all this mentally—decision context, plan, and review criteria juggled while coding. Skills externalize thinking. They make it visible and repeatable.

## The Skill Selection Problem

Automatic skill activation powers superpowers. Claude detects "design mode" and surfaces brainstorm. Claude recognizes bugs and activates root-cause-analysis.

The tension: **What happens when Claude's skill selection misses your actual problem?**

I've caught myself:
- Reaching for **brainstorm** when I should use **root-cause-analysis** (debugging, not designing)
- Using **write-plan** when **requesting-code-review** would work better (I need validation, not tasks)
- Letting **TDD** run its rigid cycle when a looser approach would move faster

Automatic activation works most times. When it fails, you follow a skill designed for a different problem.

This raises a deeper question about how agentic models reason about tool selection. Models learn patterns from usage, from context, from what resembles a problem. But the best tool depends on something subtler: your actual intent and constraints.

**Skill developers face the real design challenge here.** Writing a great skill means nothing. You must write a skill that signals when to use it—through clear naming, explicit guardrails, and distinctive patterns that models recognize. The skill test room validates that models choose skills for the right reasons, not by accident.

Skills unlock clarity. But they expose how agentic models must grow smarter about when to apply them. Skill developers must grow smarter about signaling their purpose.

## The Workflow in Action

This stays abstract until you see it work. Here's what this looks like in practice.

Before superpowers, my process wandered:
- I'd have an idea
- I'd start coding immediately
- Halfway through, I'd discover missed edge cases or a fragile approach
- I'd refactor, blame myself for shallow thinking
- I'd ship something that worked but felt fragile

Here's a real example. I built a Morpho Markets listing page for a DeFi dashboard. Instead of guessing the best approach, I used **competitive development**.

**Step 1: Set up the problem.** I describe requirements—list Morpho markets, display real SDK data, handle BigInt correctly, make it accessible.

**Step 2: Spawn multiple agents.** I dispatch three agents to solve the same problem independently. Each creates a pull request with its own approach.

**Step 3: Evaluate competitively.** I score all three PRs against a rubric: correctness, maintainability, UX, performance, security, observability. PR 12 wins with 88/100 (real SDK data, clean separation, solid architecture). PR 11 delivers the best UX with search and filtering. PR 13 scores well but raises performance concerns.

**Step 4: Synthesize the best.** The key move: I don't pick a winner and ship. I use the plan skill to create a detailed plan: "cherry-pick the excellent search/sort UI from PR 11 into PR 12's architecture." I explore multiple approaches. I synthesize the best parts.

The difference: I move from "pick the best implementation" to "explore multiple implementations and combine their strengths." Before superpowers, I would have written three implementations myself. Now I delegate exploration and synthesis simultaneously.

## What This Means

**Skills change how you think, not how fast you work.**

Before superpowers, I tried to be everything—designer, planner, implementer, reviewer, quality assurance. I context-switched constantly. The bottleneck was my ability to use AI effectively.

Skills externalize cognitive work. They make thinking visible. They create checkpoints where you must articulate what you're solving before you solve it.

Now I can:
- **Brainstorm with conviction.** The brainstorm skill forces me to explore alternatives.
- **Plan with clarity.** I document and validate the plan before execution.
- **Delegate with confidence.** Haiku executes against a clear spec, not guessed intent.
- **Review systematically.** Codex validates against original design intent, not just working code.

This unlocks the real power of AI: **moving from "have Claude do the work" to "have Claude do the thinking work humans struggle with, so humans focus on work they excel at."**

Superpowers enables this shift—from doing to coordinating.

## The Takeaway

You've hesitated about Claude Code's plugin ecosystem, thinking it collects nice-to-haves. I was skeptical too.

Superpowers shifts how you work with Claude fundamentally. It transforms Claude from a tool into a thinking partner.

Here's what I'd tell someone starting:

Install the [superpowers marketplace](https://github.com/obra/superpowers-marketplace). Start with brainstorm on your next design problem. Notice how it forces clarity. Use write-plan on the result. Notice how the plan becomes your contract with implementation. Delegate the execution. Notice how validation at multiple levels changes your confidence.

That experience—where thinking becomes visible, plans become clear, delegation becomes safe—that's the unlock.

Skills make you think better. If you're working with Claude, thinking better is everything.

**Tell me how superpowers (or other skills) changed your workflow.** When did it click? What skill unlocked something unexpected? Drop a comment or reach out—I want to know what other developers discover in this ecosystem.
