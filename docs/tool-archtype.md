

---
# ======================
# 🔹 BASIC IDENTIFICATION
# ======================

title: "Brittle Prompt Detector"                # Human-readable name of the tool
slug: "brittle-prompt-detector"                 # URL-friendly ID
category: "Stop Micromanaging the AI"           # Category grouping
pattern: "Task-to-Goal Reframing"               # Conceptual pattern type
icon: "🧩"                                      # Optional emoji or SVG reference

# ======================
# 🔹 METADATA
# ======================

summary: "Finds the weak spots in your old prompts that break easily."  
description: >
  A diagnostic tool that analyzes a prompt for brittle spots — over-specified
  instructions, missing context, or stepwise fragility — and offers suggestions
  to rewrite it as a resilient, goal-oriented version.

tags: ["prompt-analysis", "goal-rewriting", "diagnostic"]
author: "AI Tools Lab"
version: "1.0"
date: 2025-10-28
lastmod: 2025-10-28
status: "active"                                # Optional: draft, active, deprecated
layout: "tool"                                  # The template Hugo should use

# ======================
# 🔹 TOOL BEHAVIOR CONFIG
# ======================

# A short sentence for the call-to-action button on the page
action_label: "Run Tool"

# Defines whether this tool runs locally (client-side) or via API
execution_mode: "api"                           # options: static | api | local

# Optional: If api, specify endpoint and method
api:
  endpoint: "/api/run-tool"
  method: "POST"

# ======================
# 🔹 PROMPT TEMPLATE (the logic)
# ======================

prompt_template: |
  You are the Brittle Prompt Detector.
  Analyze the following prompt and identify areas that might cause brittle or failing behavior.
  Return your findings in a YAML structure with:
    - status (Brittle or Resilient)
    - confidence (0–100)
    - issues (list)
    - suggestion (rewrite idea)
  PROMPT: {{ user_input }}

# ======================
# 🔹 EXAMPLES (for display + training)
# ======================

example_input: |
  1. Greet the user
  2. Ask for their name
  3. Ask for their email
  4. Ask for their problem
  5. Say “thank you”

example_output: |
  analysis:
    status: "Brittle"
    confidence: 90
    issues:
      - "Step 2: 'Ask for name' may fail if the name is already known."
      - "Step 4: Too procedural; lacks user context."
    suggestion: >
      Condense this into a goal-oriented prompt like:
      “Politely capture the user's problem and contact info.”

# ======================
# 🔹 PRESENTATION CONFIG
# ======================

theme_color: "#007acc"                          # Accent color per tool
show_examples: true                             # Boolean toggle
show_metadata: true                             # Show version/author info
collapsible_examples: false                     # If true, examples collapse

# ======================
# 🔹 OPTIONAL EXTENSIONS
# ======================

related_tools:
  - "task-list-condenser"
  - "goal-oriented-rewriter"

resources:
  - title: "Prompt Resilience Guide"
    url: "/docs/prompt-resilience-guide"

# For later dynamic visualization (Logic Chain, etc.)
visualizer:
  type: "yaml-tree"
  enabled: true

# ======================
# 🔹 FOOTER / COPYRIGHT
# ======================

license: "CC-BY-SA 4.0"
---

















---







---
learning:
  # 1️⃣ Technique Name
  technique: "Task-to-Goal Reframing"
  # → The core conceptual method this tool demonstrates.
  # Example: “Goal-Oriented Prompting”, “Psychological Persona Design”, “Emergent Logic Chain”

  # 2️⃣ Pattern / Mental Model
  pattern: "Stop Micromanaging the AI"
  # → The “big idea” family this tool belongs to.
  # This connects to your category (so users can navigate conceptually).

  # 3️⃣ Principle
  principle: "Give the AI a goal, not a list of steps."
  # → The distilled one-sentence *law* this tool is teaching.

  # 4️⃣ Problem Statement
  problem_it_solves: >
    Many users over-script their AI by giving 10+ specific steps.
    This causes brittleness and breaks when language or context changes.

  # 5️⃣ Why It Matters
  importance: >
    The tool teaches users how to stop “micromanaging” and start “delegating goals.”
    This is foundational to designing scalable, motive-driven AI systems.

  # 6️⃣ Mental Shift
  mindset_shift: >
    From “I tell the AI *how* to do it” → “I tell the AI *what outcome I want*.”

  # 7️⃣ How to Use It
  usage_guidelines:
    - "Paste an over-engineered prompt."
    - "Click 'Run Tool'."
    - "Study the output YAML for patterns of brittleness."
    - "Rewrite your prompt as a high-level goal statement."

  # 8️⃣ Example in Action
  teaching_example: |
    Old prompt: "1. Ask the user’s name. 2. Ask for their problem. 3. Say thank you."
    New goal: "Politely capture the user’s problem and contact info."

  # 9️⃣ Common Mistakes
  pitfalls:
    - "Giving exact steps instead of goals."
    - "Leaving out context (‘who’, ‘why’name)."
    - "Focusing on word count instead of usefulness."

  # 🔟 Key Takeaways
  takeaways:
    - "Goal-oriented prompts are more flexible and robust."
    - "You can teach the AI ‘why’ instead of scripting every ‘how’."
    - "This method increases creative reasoning and reduces failure rate."
---








```yaml

# Basic Page Info
name:
category:

# Tool AI Instructions
system-prompt:
user-prompt:

# Tool Info
this should be varius detailed information about this tool / patter
relavant thr the lens of a developer or target audience.


example-input:
example-output:

core-concept:
primary-use-case:
real-use-cases:

when-to-use:
when-not-to-use:
variations:

related-prompt-patterns: []

developer-notes:
implementation-tips:



target-audience:


```
















```yaml
# ===============================================
# 1. CATALOG METADATA
# (Fields for sorting, filtering, and managing the catalog)
# ===============================================
id: # (A unique ID for this pattern, e.g., "P-001")
status: # (e.g., Stable, Experimental, Deprecated)
difficulty: # (e.g., Beginner, Intermediate, Advanced)
version: # (e.g., 1.0)
tags: # (Keywords for search)
  - # (e.g., reasoning, output-formatting, self-correction, creative, rag)
  - # (e.g., json, markdown, few-shot)

# ===============================================
# 2. OVERVIEW
# (Answers "What is this?")
# ===============================================
name: # (The common name, e.g., "Chain of Thought (CoT)")
category: # (A high-level bucket, e.g., "Reasoning Patterns")
core-concept: |
  # (A 1-2 sentence "elevator pitch" of the pattern.)
description: |
  # (A more detailed paragraph explaining the pattern, its purpose, and its mechanism.)

# ===============================================
# 3. APPLICABILITY & STRATEGY
# (Answers "Why, when, and where do I use this?")
# ===============================================
primary-use-case: |
  # (The single, most common problem this pattern solves.)
when-to-use: |
  # - (Bulleted list of "green flags" or ideal scenarios)
  # - e.g., "When solving multi-step math or logic problems."
when-not-to-use: |
  # - (Bulleted list of "red flags" or bad fits)
  # - e.g., "For simple, factual retrieval where speed is critical."
strengths: |
  # - (Bulleted list of proven benefits)
  # - e.g., "Dramatically improves accuracy on reasoning tasks."
  # - e.g., "Provides a transparent reasoning path for debugging."
weaknesses: |
  # - (Bulleted list of known downsides or risks)
  # - e.g., "Significantly increases token count and latency."
  # - e.g., "Can be brittle; a single error in the chain can derail the result."

# ===============================================
# 4. TECHNICAL BLUEPRINT
# (Answers "How do I build it?")
# ===============================================
system-prompt: |
  # (The recommended system prompt, if any. Use | for multi-line.)
user-prompt-template: |
  # (The user-facing prompt. Use {variables} to show where input goes.)
  # Example: "Solve the following problem. Think step-by-step. Problem: {user_problem}"

# ===============================================
# 5. IMPLEMENTATION NOTES (For Developers)
# (Answers "What are the tricks and gotchas?")
# ===============================================
implementation-notes: |
  # - (e.g., "Output Parsing: The reasoning steps can be extracted for display.")
  # - (e.g., "Token Cost: This pattern is token-heavy. Not for high-volume, low-cost APIs.")
model-compatibility: |
  # - (e.g., "Works best with high-capability models (GPT-4+, Claude 3+).")
  # - (e.g., "Smaller models may fail to follow the reasoning steps.")
dependencies: |
  # - (e.g., "None", "Requires a Vector DB", "Requires a Search API tool")
recommended-parameters:
  # (Optional settings that help this pattern work best)
  # - temperature: 0.5

# ===============================================
# 6. EVIDENCE & EXAMPLES
# (Answers "Show me it working.")
# ===============================================
example-input: |
  # (A filled-in version of the 'user-prompt-template')
example-output: |
  # (The expected LLM response to the 'example-input', showing the pattern in action)

# ===============================================
# 7. RELATIONSHIPS & REFERENCES
# (Answers "What's next?" and "Where did this come from?")
# ===============================================
variations: |
  # - (Bulleted list of known variations)
  # - e.g., "Zero-Shot CoT: A simplified version where you just add 'Let's think step-by-step.'"
  # - e.g., "Tree of Thoughts (ToT): A more complex version that explores multiple reasoning branches."
related-prompt-patterns:
  # (List of other 'id's or 'name's in the catalog)
  - # (e.g., "P-002: Tree of Thoughts")
  - # (e.g., "P-003: Step-Back Prompting")
references: |
  # (Links to papers, blog posts, or the origin of the pattern)
  # - (e.g., "Wei et al. (2022) - 'Chain-of-Thought Prompting Elicits Reasoning...' [link]")
```








```yaml
---
# ===============================================
# 1. CATALOG METADATA
# ===============================================
id: "T-001"
status: "Stable"
difficulty: "Beginner"
version: "1.0"
tags:
  - prompt-analysis
  - brittleness
  - resilience
  - prompt-engineering
  - goal-oriented
  - yaml-output

# ===============================================
# 2. OVERVIEW
# ===============================================
name: "Brittle Prompt Detector"
category: "Stop Micromanaging the AI"
core-concept: |
  Detects weak or brittle instructions in overly procedural AI prompts.
description: |
  The Brittle Prompt Detector analyzes prompts for signs of fragility—commands that
  are too rigid, overly detailed, or context-dependent. It identifies where your
  AI prompt could fail, then explains *why* and suggests how to rewrite it as a
  goal-oriented instruction. This tool teaches developers to design resilient,
  self-adaptive prompts that focus on *outcomes*, not steps.

# ===============================================
# 3. APPLICABILITY & STRATEGY
# ===============================================
primary-use-case: |
  Diagnose and improve prompts that break easily when slightly reworded or used
  in new contexts.
when-to-use: |
  - When your AI stops producing reliable results after minor phrasing changes.
  - When you notice your prompt depends too much on step-by-step scripting.
  - When you want to convert “how-to” prompts into “goal-based” ones.
when-not-to-use: |
  - When testing simple, factual, or one-shot questions.
  - When optimizing for speed and token efficiency over interpretability.
strengths: |
  - Identifies failure points before deployment.
  - Encourages more generalizable, motive-driven prompt design.
  - Produces clear YAML diagnostic reports for analysis or tooling.
weaknesses: |
  - Does not automatically fix the prompt — it provides analysis only.
  - May over-flag creative prompts as “brittle” if they use step-like formatting.

# ===============================================
# 4. TECHNICAL BLUEPRINT
# ===============================================
system-prompt: |
  You are the Brittle Prompt Detector.
  Your task is to evaluate prompts for fragility and over-specificity.
  Return your analysis in YAML with:
    - status: "Brittle" or "Resilient"
    - confidence: (0–100)
    - issues: (list of weak points)
    - suggestion: (rewrite idea)
  Be concise, constructive, and objective.

user-prompt-template: |
  Analyze this prompt for brittleness or fragility:
  {user_input}

# ===============================================
# 5. IMPLEMENTATION NOTES (For Developers)
# ===============================================
implementation-notes: |
  - Output Parsing: The YAML response can be parsed into a table or diagnostic view.
  - This pattern works well for prompt QA systems or LLM training validation.
  - The output can also be used as metadata in version-controlled prompt libraries.
model-compatibility: |
  - Works best with GPT-4+, Claude 3+, or any model with strong reasoning capabilities.
  - Smaller or instruction-only models may skip detailed analysis.
dependencies: |
  - None (can run as a standalone text-based diagnostic)
recommended-parameters:
  temperature: 0.2
  max_tokens: 800

# ===============================================
# 6. EVIDENCE & EXAMPLES
# ===============================================
example-input: |
  1. Greet the user.
  2. Ask for their name.
  3. Ask for their email.
  4. Ask for their problem.
  5. Say "thank you."
example-output: |
  analysis:
    status: "Brittle"
    confidence: 88
    issues:
      - "Step 2: 'Ask for name' may fail if user data is already known."
      - "Step 4: Too procedural; lacks a defined end goal."
    suggestion: >
      Rewrite this prompt as a goal: "Politely capture the user's name,
      contact info, and problem description."

# ===============================================
# 7. RELATIONSHIPS & REFERENCES
# ===============================================
variations: |
  - "Resilience Analyzer" — compares two prompts for robustness differences.
  - "Prompt Health Check" — tests prompts under multiple phrasings.
related-prompt-patterns:
  - "T-002: Task List Condenser"
  - "T-003: Goal-Oriented Rewriter"
references: |
  - "OpenAI Prompt Engineering Guide"
  - "Anthropic Prompt Patterns — Reframing Tasks as Goals"
---

# 🧩 Brittle Prompt Detector

The **Brittle Prompt Detector** helps you find *weak spots* in your AI prompts — places where your instructions depend too heavily on specific wording or steps.  
Think of it as a **prompt stress test**: it looks for logic that’s too rigid or under-contextualized.

### 🧠 What It Teaches
- How to recognize *brittleness*: prompts that fail when one step changes.
- Why goal-oriented prompts are more reliable and adaptive.
- How to turn step-by-step “scripts” into flexible “objectives”.

### 🧭 Why Developers Use It
Prompt engineers, AI architects, and technical teams use this tool to build **resilient** systems that perform consistently under varied inputs.  
It’s perfect for auditing LLM workflows, pipelines, or conversation templates.

### ⚙️ How to Use
1. Paste your full prompt (even if it’s ugly).  
2. Run the detector — it returns YAML analysis.  
3. Study the issues and rewrite your prompt as a goal statement.  
4. Use the suggestion as a base for the **Task-to-Goal Reframing** pattern.

### 🎯 Example
**Input Prompt:**
```








