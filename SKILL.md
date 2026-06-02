---
name: meta-search
description: "Universal methodology-discovery protocol. Before executing any task or search, load this skill whenever no verified best-practice skill exists for the domain. This is a META capability — it discovers how to discover, producing domain-specific skills through Cynefin domain assessment, source ecology inference, branched search, lateral reading, and convergence detection. Uses github-search for GitHub-native precision."
version: 1.0.0
author: KONA
license: MIT
homepage: https://github.com/sekai-dev-team/meta-search
platforms: [linux]
---

# Meta-Search: Universal Methodology Discovery Protocol

## L1: Meta-Mindset (Always On)

Before ANY task or search, run this check:

```
Do we have a verified best-practice skill for this domain/task?
├── YES → Load it, follow it, execute.
└── NO  → Trigger L2: Meta-Search Protocol.
          Goal: DISCOVER the best practice, save to KB, optionally create skill.
```

This is not optional. It is not only for "unfamiliar" domains. Even familiar domains without a codified skill trigger this.

---

## L2: Meta-Search Protocol (Cyclical)

```
┌──────────────────────────────────────────────────┐
│                                                  │
│  Step 0: Domain Assessment                       │
│      ├── Cynefin classification (objective +     │
│      │   subjective)                             │
│      └── Information gap estimation              │
│              ↓                                   │
│  Step 1: Source Ecology Inference                │
│      └── Where does ground truth live in         │
│          this domain?                            │
│              ↓                                   │
│  Step 2: Branched Search                         │
│      ├── Branch A: Academic/Paper                │
│      ├── Branch B: Community/OSS                 │
│      ├── Branch C: Official Docs                 │
│      ├── Branch D: Practitioner Experience       │
│      ├── Branch E: Meta-Curation                 │
│      ├── Branch F: Self-Experiment               │
│      └── Branch G: Local Knowledge Base          │
│              ↓                                   │
│  Step 3: Lateral Cross-Validation                │
│      └── Do independent branches point to        │
│          the same consensus?                     │
│              ↓                                   │
│  Step 4: Re-Assessment                           │
│      ├── Domain clearer? Gap closed?             │
│      ├── YES → Output KB note (+ skill if workflow), execute │
│      └── NO  → Loop back to Step 0               │
│                                                  │
└──────────────────────────────────────────────────┘
```

---

## Step 0: Domain Assessment

Classify along TWO axes (not one label):

### Axis 1: Objective Domain State (inferred)

| State | Definition | Examples |
|-------|-----------|----------|
| **Clear** | Best practices exist and are widely consensus | pip install, git clone, basic API usage |
| **Complicated** | Best practices exist but are scattered; requires expert synthesis | Claude Code optimal setup, investment decision models, security hardening |
| **Complex** | Cause-effect only knowable in retrospect; best practices unstable | Startup strategy, novel AI architecture, emergent tech |
| **Chaotic** | No discernible patterns; act first, understand later | System breach response, novel exploit |

### Axis 2: Subjective Information Level

| Level | Definition |
|-------|-----------|
| **Have best practice** | Already know the verified optimal approach |
| **Know structure** | Understand core concepts but don't know optimal answer |
| **Know problem** | Know what I want but don't know how to approach it |
| **Don't know what I don't know** | Blind spot |

### Output Format (Example)

```
Domain Assessment:
  Objective state: Inferred Complicated (best practices likely exist,
                    scattered across community + docs)
  Subjective level: Know structure (I know CC has subagents/skills/tools,
                     but don't know the optimal configuration)
  Gap: Need community-consensus best setup + risk mitigation strategies
```

**Crucial**: When looping back to Step 0, re-evaluate BOTH axes. Discovery may reveal the domain was Clear all along (you just didn't know it).

---

## Step 1: Source Ecology Inference

Ask: **"In this domain, who holds the ground truth, and what form does it take on the internet?"**

| Domain Type | Ground Truth Holders | Source Forms | Example |
|-------------|---------------------|--------------|---------|
| **Open-source tool/framework** | Core maintainers, power users, community | GitHub awesome-*, official docs, practitioner blogs, issue discussions | Claude Code, Docker, React |
| **Financial/Investment** | Academics, quants, institutional practitioners | SSRN/arXiv papers, factor models, textbooks, quant forums | Factor investing, risk models |
| **Security/Privacy tools** | Security researchers, professional testers | Specialized review sites (DuyaoSS-like), professional forums, private repos | VPN/proxy evaluation |
| **Software debugging** | Source code, issue tracker, core devs | git blame, official issue tracker, reproducible test cases | Bug root-cause analysis |
| **Academic/Scientific** | Researchers, peer-review process | Literature reviews, citation graphs, canonical textbooks, top conferences | Cynefin, Information Foraging |
| **Consumer products** | Actual users with hands-on experience | Unboxing videos, friend testimonials, return-rate data | Hardware purchases |
| **Novel/Narrow domain** | Nobody yet — YOU are the pioneer | Self-experimentation logs, synthesized hypotheses | New tool with no community |

**Decision**: Based on domain type, select 1-3 most promising branches from Step 2 to pursue in parallel.

---

## Step 2: Branched Search

Execute the selected branches in parallel. Lateral reading is applied THROUGHOUT — when a branch produces a claim, verify it against other branches before accepting.

### Branch A: Academic/Paper Source

**When**: Financial models, theoretical frameworks, algorithmic foundations, formal methodologies.

```
Search patterns:
  site:arxiv.org OR site:ssrn.org [topic]
  "[topic] literature review" OR "[topic] survey" OR "[topic] systematic review"
  "[topic] state of the art" OR "[topic] taxonomy" OR "[topic] framework"
  "seminal paper [topic]" OR "classic [topic]"

AI query (if web_search insufficient):
  "What are the core theoretical frameworks/models in [domain]?
   Who are the key authors? What are the canonical textbooks?"

Extract: web_extract on paper abstracts + introductions + conclusions
Trace: citation graph (who cites this? who does this cite?)

Output: Core frameworks, accepted taxonomies, key authors, major schools of thought
```

### Branch B: Community/OSS Source

**When**: Open-source tools, developer frameworks, self-hosted solutions, CLI tools.

```
Search patterns:
  "awesome [domain]" site:github.com
  "awesome-awesome" site:github.com               ← meta: index of all awesome lists
  "[tool] best setup" OR "[tool] optimal config" site:reddit.com
  "[domain] guide" OR "[domain] tutorial" site:github.com
  github.com/topics/[domain]                       ← direct GitHub topic page
  "[domain] comparison" OR "[domain] vs [alternative]"

For GitHub-native precision search (repos + code), load github-search skill.
Key tools from github-search:
  gh search repos --limit 10 --sort stars -- "topic:mcp language:python"
  gh api "search/code?q=restart_self+language:python&per_page=10"
  gh api graphql → structured repo metadata + content search
Never use 'gh search code' (legacy engine). Always 'gh api search/code'.

Evaluate: star count, last commit date, community activity (issues/PRs)
Look for: meta-collections (like superpowers for CC), "awesome-*" that aggregate resources plus methods

**When multiple competing PRs exist for the same feature:**
Load `references/github-pr-landscape-navigation.md` for the full method.
Key shortcuts: find the original issue → identify the common reviewer (gatekeeper) 
→ read their consolidation comment → distinguish self-closure from rejection.

Output: Community-consensus best tool/approach, common pitfalls, meta-collections
```

### Branch C: Official Documentation

**When**: Software/tools with official docs, platforms with formal guides.

```
Search patterns:
  Direct navigation: docs.[domain].com, readthedocs.io, [domain].dev
  "[tool] best practices" site:docs.[domain].com
  "[tool] architecture" OR "[tool] core concepts" OR "[tool] design principles"
  "[tool] getting started" → "[tool] advanced" → "[tool] in production"
  "[tool] security" OR "[tool] hardening" OR "[tool] deployment guide"

Output: Officially recommended practices, architecture boundaries, security model, configuration reference
```

### Branch D: Practitioner Experience

**When**: Real-world usage insights, production war stories, failure modes, tradeoff wisdom.

```
Search patterns:
  "[domain] in production" OR "[domain] at scale"
  "[domain] lessons learned" OR "[domain] war story"
  "[domain] postmortem" OR "[domain] horror story" OR "[domain] don't"
  "[domain] common mistakes" OR "[domain] pitfalls"
  site:news.ycombinator.com "[domain]"
  "[domain] in practice" site:substack.com OR site:medium.com

Identify: known practitioners/experts → follow their blogs, repos, talks

Output: Real tradeoffs, failure cases, boundary conditions, practitioner-validated approaches
```

### Branch E: Meta-Curation

**When**: Quickest path to "what exists" — use before diving deep into other branches.

```
Search patterns:
  "awesome-awesome" site:github.com               ← find the awesome-list-of-awesome-lists
  "[domain] resource list" OR "[domain] curated list"
  "[domain] roadmap" site:github.com               ← learning/implementation roadmaps
  "[domain] best of" OR "[domain] ultimate guide"
  "awesome [domain]"                               ← first thing to try for any domain

Output: Index of all major resources in the domain — skip individual resources, get the map first
```

### Branch F: Self-Experiment

**When**: Branches A-E exhausted with no convergence, domain too new/narrow, existing information untrustworthy.

```
Process:
  1. Synthesize fragments from A-E into a hypothesis
  2. Design a minimal verification experiment
  3. Execute and record results
  4. Extract methodology from results
  5. This BECOMES the best practice (you are the first)

Output: Original practice summary — the seed for a future community best practice
```

### Branch G: Local Knowledge Base

**When**: As a **peer-level source** alongside external branches. The vault may surface forgotten context, adjacent-domain research, or conceptual backlinks that complement — but do not replace — external discovery. If the answer were already cleanly captured in the KB, meta-search wouldn't have been triggered in the first place.

```
Search patterns:
  mcp_knowledge_search(query="[topic]")                 ← hybrid semantic + keyword
  mcp_knowledge_search(query="[domain] best practice")
  mcp_knowledge_search(query="[domain] comparison")
  mcp_knowledge_list_notes()                            ← browse all vault notes

Deep read if search hits:
  mcp_knowledge_get_note(path="...")                    ← full markdown with frontmatter + backlinks

Backlink traversal:
  After reading a relevant note, follow its backlinks to discover connected concepts.
  Example: a note on "agent memory paradigms" backlinks to "DS-004 pipeline"
           → the cross-domain relationship may inform the current search.

Index maintenance:
  mcp_knowledge_reindex(path="...")                     ← reindex single file after edit
  mcp_knowledge_reindex()                               ← incremental vault reindex

Output: Prior research fragments, domain taxonomies, cross-domain backlinks.
        Feeds into Step 3 cross-validation as an additional independent source.
        Does NOT replace external branches — the KB is complementary memory, not a cache.
```

---

## Step 3: Lateral Cross-Validation

After running branches, perform cross-check:

```
For each key claim/finding from one branch:
  → Does another independent branch confirm it?
  → Does another branch contradict it?

Convergence patterns:
  ✅ 2+ branches → same conclusion → HIGH confidence
  ⚠️ Branches disagree → domain is contested → mark as Complicated, document tradeoffs
  ❌ Only one branch has info → incomplete → continue looping
  ❌ No branches have useful info → domain is Complex/Chaotic or too new → Branch F
  🔄 Local KB has prior research → treat your past self as an additional independent source;
     cross-check: does the external search align with what you already knew?
```

**Key anti-pattern**: Do NOT accept a finding from a single branch without verification. Even official docs can be outdated. Even community consensus can be a local maximum.

---

## Step 4: Re-Assessment & Loop Control

### Re-evaluate

```
1. Has the objective domain state changed?
   (Did we discover the domain is actually Clear, not Complicated?)

2. Has our subjective information level improved?
   (Did we go from "know problem" → "know structure" → "have best practice"?)

3. Is the gap closed?
   (Do we have a converged answer from multiple independent sources?)
```

### Exit Conditions (any one triggers exit)

```
CONVERGENCE:
  Multiple independent sources point to same consensus
  → Output: knowledge base note + optionally skill (see Output Routing below)

DIMINISHING RETURNS:
  After 3 full loops, gap reduced to acceptable residual uncertainty
  → Output: knowledge base note with "current best understanding", tagged with uncertainty

EXHAUSTION + PIONEER:
  Branches A-E exhausted, no convergence found
  → Switch to Branch F (self-experiment)
  → Output: knowledge base note based on original practice, marked "pioneer"

DEGENERATE LOOP:
  Same information found repeatedly across loops, no new insight
  → Stop. Domain is in Complex/Chaotic state. Output note with "no stable best practice yet"
```

### Output Routing: Knowledge Base Note vs Skill

**ALL research results go to the knowledge base first.** Then route based on content type:

| Content Type | Destination | Examples |
|---|---|---|
| **Workflow / Procedural** | Knowledge base note **+** Skill | Debugging protocol, deployment checklist, CI/CD setup steps, code review process |
| **Reference / Declarative** | Knowledge base note only | Domain taxonomy, framework comparison, concept explanation, tool evaluation, source ecology map |

**Decision rule**: Can someone read this and immediately execute a multi-step procedure?
- YES → also create a skill (actionable, step-by-step, with commands)
- NO → knowledge base note is sufficient (concept, comparison, reference)

### Output Format

```
After loop exit, produce:
  1. Knowledge base note (always) — research results, key findings, source citations
  2. Skill (only if workflow) — codified step-by-step procedure with concrete commands
  3. Metadata: Cynefin classification, confidence level, source branches used
  4. Known gaps or uncertainties (for future re-evaluation)
```

---

## Integration with Information Credibility Hierarchy

The user's credibility hierarchy is applied during branch evaluation:

| Source Level | Application in Meta-Search |
|---|---|
| **L1: Meta-Curation** | Branch E — community-consensus explicit encoding. Highest initial signal. |
| **L2: Practitioner Summary** | Branch D — validated by real-world use. Cross-check with B/C. |
| **L3: Community Discussion** | Branch B — requires cross-reference with other branches. |
| **L4: Official Docs** | Branch C — authoritative but may be incomplete or outdated. |
| **L5: AI Summary** | Used as pointer/starting point only. NEVER as authoritative source. Always verify. |

For the full cross-disciplinary map — Information Foraging Theory, Evidence-Based Medicine Pyramid, Admiralty Code (NATO AJP-2.1), CRAAP Test, Lateral Reading (Stanford SHEG), Bayesian Epistemology, and KONA's practical hierarchy cross-mapped to each — see `references/information-credibility-frameworks.md`.

---

## Examples

### Example 1: Claude Code Setup (User's Process)

```
Step 0: Objective Complicated, Subjective "know structure"
Step 1: OSS tool → Branches B + C + D
Step 2:
  B: "awesome claude code" → superpowers plugin (highest star meta-collection)
  C: Official docs → core concepts: subagents, skills, tools
  D: "claude code security" → system-level risk, docker sandbox pattern
Step 3: B confirms C's concepts + extends with community best practices
        D identifies risks B and C didn't cover
        → Convergence: superpowers + docker sandbox = best practice
Step 4: Gap closed → Output KB note + skill (workflow type)
```

### Example 2: Investment Decision Model (Hypothetical)

```
Step 0: Objective Complicated, Subjective "know problem"
Step 1: Financial → Branches A + D (not B — community blogs are noise)
Step 2:
  A: site:ssrn.com "factor investing" → Fama-French, momentum, quality factors
     AI query: "core investment decision frameworks" → MPT, Black-Litterman, Kelly
  D: "factor investing in practice" → AQR papers, practitioner critiques
Step 3: A and D diverge on factor timing → domain is contested, document tradeoffs
Step 4: Gap partially closed → Output KB note with "contested domain" tag
```

### Example 3: VPN/Tool Selection (Hypothetical)

```
Step 0: Objective Complicated, Subjective "know problem"
Step 1: Security/privacy → Branches B + E + D
  NOTE: Do NOT use general web_search — results are affiliate-link noise
Step 2:
  E: "awesome privacy" site:github.com → curated list of resources
  B: Specialized forums + DuyaoSS-type sites → hands-on speed tests
  D: "VPN review experience" from trusted security researchers
Step 3: Cross-check: Do B and D agree on top performers?
Step 4: If converging → Output KB note (+ skill if workflow). If conflicting → continue loop.
```

---

## Pitfalls

0. **Frontmatter incompatibility**: When syncing from GitHub, `platforms: all` and `triggers` fields cause "not supported on this platform" errors in Hermes. Fix: use `platforms: [linux]` and remove `triggers`. Description should be a quoted string, not YAML literal block (`|-`). See hermes-agent-skill-authoring skill for valid frontmatter spec.

1. **Skipping Step 0**: Jumping straight to search without domain assessment leads to wrong search strategy
2. **Single-branch trap**: Accepting findings from one branch without cross-validation. Even official docs can be wrong.
3. **Wrong source ecology**: Searching GitHub for investment models, or searching SSRN for CLI tool configs. The Step 1 inference is critical.
4. **Linear thinking**: Treating Phase 1→2→3→4 as sequential rather than cyclical. Always loop.
5. **AI as authority**: Using AI answers as ground truth rather than as pointers to actual sources.
6. **Stopping too early**: Accepting the first seemingly-good answer without verifying against other branches.
7. **Not outputting a knowledge base note**: Meta-search without saving research results to the knowledge base is wasted effort. The output MUST include a knowledge base note. Only create a skill if the result is a workflow/procedure — reference material goes to the KB only.

8. **SDK availability ≠ trivial integration cost.** Finding a Python/TS SDK during meta-search signals protocol maturity, not integration simplicity. The adapter layer (session model mapping, streaming lifecycle, error recovery, context injection) dominates development effort regardless of SDK quality. Each agent's extension mechanism differs — what's a thin plugin for one agent (Claude Code MCP server) may require a platform-level fork for another (Hermes gateway). When estimating integration cost after SDK discovery: assume 150-300 lines of adapter code, not 50. This pitfall triggered: A2A Relay research session 2026-05-14, where Synadia Python SDK was found but Hermes adapter complexity was underestimated.

## Domain Knowledge Banks

Completed meta-search research results are saved as reference files. Load relevant ones before re-researching the same domain:

| Reference File | Domain | Key Sources |
|---------------|--------|-------------|
| `references/lifelong-learning-llm-agents.md` | AI agent continuous perception, memory architecture, lifelong learning | Zheng et al. TPAMI 2026, PMA protocol, Second-Me, LifelongAgentBench |
| `references/agent-memory-paradigms.md` | Episodic→Semantic memory transition, consolidation triggers, concept-mediated graphs, KNN density clustering | RecMem (2026), GAAMA (2026), SYNAPSE, Dual-Process, Human-Inspired Memory |
| `references/concept-lookup-mechanisms.md` | Concept page discovery when new episodic info arrives — lookup strategies across 5 memory paradigms | RecMem, GAAMA, SYNAPSE, Dual-Process, Human-Inspired — with DS-004 design implications |
