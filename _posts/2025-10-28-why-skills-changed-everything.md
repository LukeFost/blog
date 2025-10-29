---
layout: post
title: "How Superpowers Changed My Development Workflow"
date: 2025-10-28
categories: claude-code ai-development superpowers
---

# How Superpowers Changed My Development Workflow

## Opening: The Meta-Aggregation Context

The Claude Code ecosystem builds elegant layers. APIs aggregate into MCPs. MCPs aggregate into skills. Skills aggregate into plugins. Plugins aggregate into marketplaces.

A beautiful abstraction.

But understanding the architecture changes nothing. **Discovering which layer solves your problem changes everything.**

Skills changed mine (specifically the [superpowers marketplace](https://github.com/obra/superpowers-marketplace)). Skills changed how I think about building with Claude Code.

![Architecture layers diagram showing APIs aggregating into MCPs, MCPs into skills, skills into plugins, and plugins into marketplaces]({{ '/assets/images/architecture-layers.svg' | relative_url }})

> The Claude Code ecosystem builds in elegant layers. Understanding this architecture is useful, but discovering which layer solves your specific problem changes everything.

## The Skill Stack as a System

Skills force you to think differently. They create **decision checkpoints**.

Three skills matter most: **brainstorm**, **write-plan**, and **superpowers:requesting-code-review** (and how they work together).

- **Brainstorm** forces clarity before code: What problem am I solving? What alternatives exist? What do I want?
- **Write-plan** converts clarity into a structured roadmap any model can execute
- **Requesting-code-review** creates a validation gate where Codex or Haiku verifies work against the original intent

The **delegation model** makes this powerful: You brainstorm with full context, plan at high level, hand off implementation to Haiku (who executes without overthinking), and bring Codex in for thinking-heavy review. Each model does what it does best.

Before superpowers, I held all this mentally (decision context, plan, and review criteria juggled while coding). Skills externalize thinking. They make it visible and repeatable.

![Skill stack workflow diagram showing brainstorm → write-plan → delegate to Haiku → review with Codex]({{ '/assets/images/skill-stack-workflow.svg' | relative_url }})

> Each model does what it does best. Thinking becomes visible and repeatable.

## The Skill Selection Problem

Automatic skill activation powers superpowers. Claude detects "design mode" and surfaces brainstorm. Claude recognizes bugs and activates root-cause-analysis.

The tension: **What happens when Claude's skill selection misses your actual problem?**

![Tools and skill selection concept]({{ '/assets/images/tools-selection.gif' | relative_url }})

> Having many powerful tools doesn't help if you pick the wrong one for the job. The challenge is writing skills that clearly signal when to use them.

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

![Competitive development diagram showing three parallel agents exploring solutions, then their results converging and synthesizing the best elements]({{ '/assets/images/competitive-development.svg' | relative_url }})

> Three agents explore approaches independently. Instead of picking a winner, I synthesize the strongest elements from each.

**Step 1: Set up the problem.** I describe requirements—list Morpho markets, display real SDK data, handle BigInt correctly, make it accessible.

**Step 2: Spawn multiple agents.** I dispatch three agents to solve the same problem independently. Each creates a pull request with its own approach.

**Step 3: Evaluate competitively.** I score all three PRs against a rubric: correctness, maintainability, UX, performance, security, observability. PR 12 wins with 88/100 (real SDK data, clean separation, solid architecture). PR 11 delivers the best UX with search and filtering. PR 13 scores well but raises performance concerns.

**Step 4: Synthesize the best.** The key move: I don't pick a winner and ship. I use the plan skill to create a detailed plan: "cherry-pick the excellent search/sort UI from PR 11 into PR 12's architecture." I explore multiple approaches. I synthesize the best parts.

The difference: I move from "pick the best implementation" to "explore multiple implementations and combine their strengths." Before superpowers, I would have written three implementations myself. Now I delegate exploration and synthesis simultaneously.

## What This Means

**Skills change how you think, not how fast you work.**

Before superpowers, I tried to be everything (designer, planner, implementer, reviewer, quality assurance). I context-switched constantly. The bottleneck was my ability to use AI effectively.

Skills externalize cognitive work. They make thinking visible. They create checkpoints where you must articulate what you're solving before you solve it.

![Coordination and orchestration]({{ '/assets/images/orchestration.gif' | relative_url }})

> The shift from doing everything yourself to orchestrating specialized work. Each component excels at its role.

Now I can:
- **Brainstorm with conviction.** The brainstorm skill forces me to explore alternatives.
- **Plan with clarity.** I document and validate the plan before execution.
- **Delegate with confidence.** Haiku executes against a clear spec, not guessed intent.
- **Review systematically.** Codex validates against original design intent, not just working code.

This unlocks the real power of AI: **moving from "have Claude do the work" to "have Claude do the thinking work humans struggle with, so humans focus on work they excel at."**

Superpowers enables this shift—from doing to coordinating.

## The Real ROI: Failing Fast at Thinking, Before Expensive Execution

Here's what skeptics need to understand: the value of skills isn't speed. It's **preventing waste**.

Before superpowers, I tried running multiple agents in parallel. The workflow looked like: send agent 1 a task → wait for result → read it → send agent 2 a task → wait → read → send agent 3 a task. I was stepping forward two steps, stopping, reading, then planning from there. It felt like *moving in slow motion through a chaotic space*. And my projects kept stumbling. I couldn't see the full landscape before agents executed.

I then tried a different approach: rigid specification. I used SpecKit, a test-driven development framework that forced me to write exhaustive tests before any execution. The promise was clarity and accuracy.

It delivered accuracy. But it also delivered paralysis. I spent so much time writing tests that I stopped executing. When I finally did execute, the feature wasn't what I expected. I'd backtrack, change the tests, but then the tests wouldn't fit together. The whole workflow began to crumple. **I'd increased accuracy by 20% and reduced execution speed by 60%. I was slower and more frustrated.**

I was stuck between two bad options: chaotic manual coordination (fast but error-prone) or rigid specification (accurate but glacial).

Then I discovered superpowers. Here's what changed: **I could finally bridge the gap by validating thinking before execution.**

The workflow now:
1. Brainstorm to expose logical holes and missing constraints
2. Write a solid plan that gates bad ideas before they become code
3. Instantiate multiple git worktrees in parallel with Haiku agents (30-40 min execution each)
4. All agents make PRs simultaneously while I work on something else
5. Reviewer agents synthesize the best approaches
6. Codex picks the absolute best one

The impact was dramatic. Before, I'd ship features and hear: "Why didn't you include that?" Now I cover the entire breadth of possibilities. Instead of wondering if I'd structured the work correctly, I know I've explored all the angles.

**Why does this work?** Because the planning stage gates execution. Bad ideas die before they waste agent compute. Good ideas execute in parallel. The agents aren't smart enough to invent solutions—but they ARE smart enough to explore all the angles of a *well-specified* problem.

This is the ROI skeptics miss: **skills don't make agents faster. They make your thinking better, which makes parallel execution actually work.**

Without solid planning, spawning three agents is just expensive waste. With planning, it's exploration. The difference is the thinking stage.

## The Takeaway

You've hesitated about Claude Code's plugin ecosystem, thinking it collects nice-to-haves. I was skeptical too.

Superpowers shifts how you work with Claude fundamentally. It transforms Claude from a tool into a thinking partner.

![Skills making thinking visible]({{ '/assets/images/thinking-visible.gif' | relative_url }})

> Skills externalize thinking. They transform invisible mental work into visible, repeatable layers.

Here's what I'd tell someone starting:

Install the [superpowers marketplace](https://github.com/obra/superpowers-marketplace). Start with brainstorm on your next design problem. Notice how it forces clarity. Use write-plan on the result. Notice how the plan becomes your contract with implementation. Delegate the execution. Notice how validation at multiple levels changes your confidence.

That experience (where thinking becomes visible, plans become clear, delegation becomes safe) is the unlock.

Skills make you think better. If you're working with Claude, thinking better is everything.

**Tell me how superpowers (or other skills) changed your workflow.** When did it click? What skill unlocked something unexpected? Drop a comment or reach out—I want to know what other developers discover in this ecosystem.
