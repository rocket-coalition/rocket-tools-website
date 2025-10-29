


```yaml
# ======================================================================
# Official Rocket Tools Front Matter Archetype (tool.md)
# ======================================================================
# Purpose:
# Defines the complete metadata schema for every tool page in the site.
# Each tool is a self-contained Hugo content file generated automatically
# by the backend AI agent and rendered via Hugo’s content system.
# ======================================================================

title: "Tool Name"              # (string) Display name of the tool shown in UI
slug: "tool-name"               # (string) URL-friendly identifier (auto-generated)
date: 2025-10-29                # (date) Creation date of the tool page
lastmod: 2025-10-29             # (date) Last modification date
draft: false                    # (bool) Indicates if tool is live or under development

# ----------------------------------------------------------------------
# TOOL CLASSIFICATION
# ----------------------------------------------------------------------
tool_group: "Text Tools"        # (string) Logical group name; maps to sidebar
tool_id: "text-summary"         # (string) Unique short ID for internal reference
tool_tags:                      # (array) Tags specific to tools (not blog tags)
  - "text"
  - "summarization"
  - "prompt-engineering"
difficulty_level: "beginner"    # (enum) beginner | intermediate | advanced
use_case: "Summarize long text into concise points"

# ----------------------------------------------------------------------
# TOOL DESCRIPTION & EDUCATIONAL CONTENT
# ----------------------------------------------------------------------
summary: >
  A short, high-level summary (one or two sentences) describing what the tool does.

description: >
  A detailed description of the tool’s purpose, capabilities, and educational value.

educational_objectives:         # (array) 10 key things a prompt engineer or user learns
  - "Understand LLM summarization patterns."
  - "Recognize prompt structure for concise output."
  - "Experiment with input scaling and truncation."
  - "Observe impact of temperature on output stability."
  - "Analyze semantic compression behavior."
  - "Practice writing structured prompts."
  - "Explore context window optimization."
  - "Review stop sequence handling."
  - "Learn token efficiency metrics."
  - "Compare human vs AI summarization quality."

examples:                       # (array of objects) Example use cases shown on page
  - title: "Summarize a product review"
    input: "The battery lasts 4 hours but the design is sleek and modern..."
    output: "Stylish but limited battery life; good for short use."
  - title: "Condense a news article"
    input: "The recent report by the UN suggests..."
    output: "UN emphasizes urgent climate action and global cooperation."

related_tools:                  # (array) Optional related tools for cross-navigation
  - "text-expander"
  - "keyword-extractor"
  - "tone-analyzer"

# ----------------------------------------------------------------------
# PROMPT ENGINEERING METADATA
# ----------------------------------------------------------------------
system_prompt: |
  You are an expert AI summarizer. Your goal is to distill the user’s text
  into concise and readable summaries. Maintain factual accuracy and
  clarity. Avoid redundancy and opinion.

user_prompt_template: |
  Summarize the following input clearly and briefly:
  {{user_input}}

input_instructions: >
  Enter any paragraph or block of text you’d like summarized.  
  The tool will produce a concise version highlighting main ideas.

example_input: |
  The company achieved record growth but faced challenges in logistics and staffing.

expected_output: |
  Record growth offset by logistics and staffing challenges.

# ----------------------------------------------------------------------
# EXECUTION PARAMETERS
# ----------------------------------------------------------------------
backend_function: "summarizer"  # (string) Netlify function name to call
model: "gpt-5-turbo"            # (string) Default LLM model for this tool
temperature: 0.3                # (float) Sampling temperature (0.0–1.0)
max_tokens: 500                 # (int) Maximum response length
timeout_seconds: 30             # (int) Max wait time for serverless call
response_format: "markdown"     # (enum) plaintext | markdown | html | json

# ----------------------------------------------------------------------
# FRONTEND DISPLAY OPTIONS
# ----------------------------------------------------------------------
show_examples: true             # (bool) Display example section
show_educational_materials: true
show_tags: true
show_related_tools: true
show_article: true              # (bool) Whether to render article text after results
layout: "tool"                  # (string) Hugo layout to use (maps to /layouts/tool.html)

# ----------------------------------------------------------------------
# VISUAL / UI METADATA
# ----------------------------------------------------------------------
icon: "⚙️"                      # (string) Emoji or icon class for sidebar
color_theme: "accent"           # (string) DaisyUI theme color
animation_style: "fade"         # (string) Alpine.js transition for results display
loading_indicator: "spinner"    # (string) Type of visual indicator while processing

# ----------------------------------------------------------------------
# ARTICLE CONTENT
# ----------------------------------------------------------------------
# Markdown article that appears *beneath* the tool results.
# Provides educational reading, deep dives, and example analyses.
# ----------------------------------------------------------------------
article_content: |
  ## Understanding Summarization with AI

  This tool demonstrates how prompt engineering principles affect
  summarization outcomes. By adjusting your input or experimenting with
  parameters, you can see how an LLM compresses information while
  preserving meaning.

  ### Key Concepts
  - **Prompt Templates:** Encourage structured, repeatable output.
  - **Temperature:** Controls creativity vs. precision.
  - **Context Windows:** Large inputs may be truncated or compressed.

  ### Try It Yourself
  Enter different types of content — news, essays, product reviews —
  and observe how the summary style adapts.

# ----------------------------------------------------------------------
# GENERATED METADATA
# ----------------------------------------------------------------------
ai_generated: true               # (bool) Indicates page was created by AI agent
ai_generator_version: "v1.0.0"   # (string) Version of backend AI generator
generation_date: 2025-10-29      # (date) Timestamp of AI generation
validation_status: "pending"     # (enum) pending | approved | rejected
content_reviewer: "auto"         # (string) human | auto | mixed

# ----------------------------------------------------------------------
# OPTIONAL METADATA (EXTENSIBLE)
# ----------------------------------------------------------------------
estimated_run_time_ms: 1800      # (int) Average execution time for backend process
popularity_score: 0.75           # (float) 0–1 scale; updated via analytics
license: "RocketTools Educational License v1"
contributors:                    # (array)
  - name: "Rocket AI Agent"
    role: "content generator"
  - name: "Doug"
    role: "product architect"
  - name: "Web Developer TBD"
    role: "implementation engineer"
```