---
title: "Cognitive Load Gardening — Why Simple Code Grows Better"
date: 2025-10-17 08:00:00 +0200
categories: [Reflections]
tags: [growth, mindset, devops, reflections, cognitive-load]
pin: false
image: /assets/img/post/code-comparision.png
description: "Lessons from Linus Torvalds on reducing cognitive load - why sometimes the simple path is the sustainable one."
---

# Cognitive Load Gardening — Why Simple Code Grows Better 🧠

I came across an interesting piece recently where [Linus Torvalds tore apart some "garbage code"](https://read.engineerscodex.com/p/how-to-not-write-garbage-code-by?ref=dailydev) in a Linux kernel pull request. While his delivery was... characteristically blunt, the underlying principle resonated with me: **optimize for reducing cognitive load**.

This connects perfectly with my [farmer mindset](../think-like-a-farmer-bonsai/) approach to software. Just as a gardener keeps their tools simple and their garden paths clear, we should write code that doesn't exhaust the mind trying to understand it.

> "Sometimes duplication reduces cognitive load because the 'chunk' is self-contained."
{: .prompt-tip }

---

## The Case Against "Helpful" Abstractions

Linus's example was brilliant in its simplicity. A Meta engineer had created a helper function `make_u32_from_two_u16(a,b)` instead of writing `(a << 16) + b`. The helper was supposed to make things clearer, but it actually made them worse.

Why? Because now you have to:
1. **Context switch** to understand what the helper does
2. **Guess the parameter order** (which is `a` and which is `b`?)
3. **Remember** this abstraction exists when reading code later

The inline version `(a << 16) + b` tells you exactly what's happening. No mental gymnastics required.

This reminds me of over-engineered garden tools. You know the ones — multi-function gadgets with seventeen attachments that promise to revolutionize your gardening. In practice, you spend more time figuring out which attachment does what than actually tending your plants.

---

## Micro-Context Switches: The Hidden Tax

Every abstraction is a **cognitive tax**. When I read code with many helper functions spread across files, my brain has to:

- Load new context for each function
- Remember what each abstraction does  
- Track the relationships between them
- Keep the "big picture" in working memory

It's like having a garden where every tool is stored in a different shed. You spend more time walking between sheds than actually gardening.

At Senwes, when I inherited some legacy systems, I found codebases where simple operations were buried under layers of "helpful" abstractions. What should have been a 5-minute change became a 30-minute archaeological dig through multiple files.

---

## When Duplication Is Actually Cleaner Soil

This challenges the traditional "DRY" (Don't Repeat Yourself) principle we've all internalized. Sometimes, **PRY** (Please Repeat Yourself) creates cleaner, more maintainable code.

Consider this scenario: You have similar-but-not-identical validation logic in three places. The DRY approach says "extract a function!" But if that function needs complex parameters to handle the slight differences, you've made things worse.

The PRY approach says: "Keep it local and clear." Three simple, readable functions that do exactly what they need to do, with no mental overhead.

It's like having three different garden beds that need similar but not identical care. You could create one complex watering system with adjustable settings for each bed. Or you could use three simple watering cans, each calibrated for its specific bed.

---

## The Modern Context: AI and Code Readers

The article made an excellent point about today's code having multiple readers: **humans, LLMs, and compilers**. This actually strengthens the case for cognitive simplicity.

When I'm working with GitHub Copilot or ChatGPT on code changes, I notice they perform much better with self-contained, clear code blocks. They don't have to "think" across multiple files or remember complex abstractions.

Just like human working memory, LLMs have token limits. Simple, direct code uses fewer tokens and produces better results.

---

## My Practical Approach to Cognitive Load

Here's how I apply this in my daily work:

**Before abstracting, ask:**
- Does this abstraction remove complexity or just move it somewhere else?
- Will a new team member understand this without documentation?
- Can I explain what this code does in one sentence?

**Keep cognitive chunks small:**
- Functions that fit on one screen
- Clear variable names that explain intent
- Direct operations over clever abstractions

**Optimize for the reader, not the writer:**
- Code is read 10x more than it's written
- Favor explicitness over cleverness
- Make the common case obvious

---

## The Balance: When to Abstract, When to Repeat

This isn't about never abstracting. Good abstractions are like well-designed garden paths — they guide you naturally where you need to go.

Abstract when:
- The logic is complex and error-prone
- You need to enforce consistent behavior across the system
- The abstraction truly simplifies understanding

Repeat when:
- The code is simple and direct
- The "abstraction" just moves complexity elsewhere
- Context switching costs more than duplication

---

## Tending Your Cognitive Garden

Good code, like a good garden, should feel **peaceful to navigate**. When I'm reading well-written code, my brain doesn't strain. The intent is clear, the flow is natural, and I can focus on the problem I'm trying to solve rather than deciphering what the code does.

That's the kind of cognitive environment where good solutions grow.

---

## It Doesn't Cost Anything to Be Nice

Before I wrap up, there's something important to address about Linus's approach. While his technical point about cognitive load was spot-on, his delivery was unnecessarily harsh.

As one developer, Abhinav Upadhyay, put it perfectly:

> "The point that Linus makes is right but his style is not. It sets the wrong precedent for the younger generation to be just as toxic as this. You can criticise the code without being abusive... If I tell my colleague I will not merge their code because of a style issue, they will learn and fix it, i don't have to call it garbage to cause trauma."

**Being rude makes committing code a risk.** Nobody wants to write code and risk being publicly berated. This creates an environment where people are afraid to contribute, experiment, or learn from mistakes.

In my experience at both BBD and Senwes, the best code reviews came from teammates who could point out issues constructively. When someone explained **why** a certain approach increased cognitive load, I learned. When someone just called my code "garbage," I learned to avoid them.

Good gardens grow with encouragement, not fear.

---

## Final Thoughts — Simple Tools, Clear Paths, Kind Words

Linus was right about the code being problematic, but we can learn the lesson without adopting the tone. The best tools are often the simplest ones — clear, direct, and purposeful. The best teams are built the same way.

When you're writing code, ask yourself: "Am I creating a clear garden path, or am I building a maze?"

When you're reviewing code, ask yourself: "Am I helping this garden grow, or am I trampling the seedlings?"

Your future self, your teammates, and the next generation of developers will thank you for choosing both the simple path and the kind words.
