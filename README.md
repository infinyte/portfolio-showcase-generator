# Portfolio Showcase Generator

**Transform your technical projects into compelling portfolio materials optimized for recruiters, hiring managers, and technical interviews.**

A Claude AI skill that analyzes your projects and generates professional portfolio content including executive summaries, technical deep-dives, architecture diagrams, STAR interview stories, and more.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Claude AI](https://img.shields.io/badge/Claude-AI%20Skill-blue)](https://claude.ai)

---

## Table of Contents

- [Why This Skill?](#why-this-skill)
- [Features](#features)
- [What It Generates](#what-it-generates)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Usage Examples](#usage-examples)
- [Input Formats](#input-formats)
- [Output Samples](#output-samples)
- [Use Cases](#use-cases)
- [Contributing](#contributing)
- [License](#license)

---

## Why This Skill?

**The Problem:**
- You've built amazing projects, but translating them into compelling portfolio materials is time-consuming
- Recruiters need quick, high-impact summaries; architects need technical depth
- Interview prep requires structured STAR stories that you haven't written
- Creating architecture diagrams from scratch takes hours

**The Solution:**
This skill acts as your personal portfolio writer and interview coach. Feed it your project (GitHub repo, project notes, or just describe it), and it generates audience-specific content that showcases your work professionally.

**Perfect for:**
- Software engineers in job searches
- Architects building portfolios
- Anyone preparing for technical interviews
- Engineers documenting their impact
- Developers showcasing side projects

---

## Features

### Multi-Audience Output
Generate content tailored to different audiences from the same project:
- Executive summaries for recruiters (150-250 words)
- Technical deep-dives for architects (800-1500 words)
- STAR stories for interviews (90-120 seconds)

### Automatic Architecture Diagrams
Creates professional Mermaid diagrams:
- System architecture
- Data flow
- Deployment topology
- Integration patterns

### Business Impact Analysis
Extracts and presents quantifiable achievements:
- Performance metrics
- Cost savings
- Scale achievements
- Reliability improvements

### Interview Preparation
Generates structured STAR format stories:
- Technical problem-solving
- Architectural decision-making
- Leadership and influence
- Handling constraints

### Code Analysis
Analyzes GitHub repositories to extract:
- Tech stack and frameworks
- Architectural patterns (DDD, microservices, etc.)
- Infrastructure and deployment
- Testing and quality practices

### Multiple Output Formats
- Markdown documents
- Resume bullets (copy/paste ready)
- LinkedIn profile enhancements
- Interview talking points
- GitHub Pages structure

---

## What It Generates

### 1. Executive Summary
A concise, high-impact overview focused on business value:
```
Led development of FLIFO Flight Status V2.0, the first production 
application in our enterprise's new Zero Trust security architecture. 
Achieved 99.9% uptime while supporting 500+ concurrent users and 
processing 10K+ flight status updates daily with sub-200ms API 
response times...
```

### 2. Technical Deep-Dive
Comprehensive architectural analysis with:
- Context and constraints
- Design decisions with rationale
- Technical implementation details
- Challenges and solutions
- Performance metrics
- Trade-offs and compromises

### 3. Architecture Diagrams
Professional Mermaid diagrams showing:
- System architecture (components, integrations)
- Data flow (source → processing → delivery)
- Deployment architecture (cloud resources, security)

### 4. STAR Interview Stories
Complete interview narratives:
```
Situation: Three months into production, we discovered critical 
data freshness issues...

Task: I needed to ensure 99.9%+ data completeness while maintaining 
real-time responsiveness...

Action: I implemented a hybrid push-pull strategy combining webhooks 
for real-time updates with scheduled polling as a safety net...

Result: Achieved 99.9% data completeness and improved webhook success 
rate from 87% to 98%...
```

### 5. Metrics Dashboard
Quantified achievements:
- **Performance**: Reduced API response time by 60% (450ms → 180ms)
- **Scale**: Enabled 10x growth from 1K → 10K concurrent users
- **Cost**: Cut cloud costs by $24K/year through optimization
- **Reliability**: Improved uptime from 95% → 99.5%

### 6. Bonus Materials
- Resume bullets optimized for ATS
- LinkedIn profile enhancements
- Interview talking points
- Technical skills to highlight

---

## Installation

### Prerequisites
- Active [Claude.ai](https://claude.ai) account (Pro, Team, or Enterprise)
- Access to Claude's file creation features

### Quick Install (2 minutes)

**Step 1:** Download the skill file
- Download [`SKILL.md`](SKILL.md) from this repository

**Step 2:** Install in Claude
1. Open a new conversation in [Claude.ai](https://claude.ai)
2. Say: *"Please create a file at `/mnt/skills/user/portfolio-showcase-generator/SKILL.md`"*
3. When Claude creates the file, paste the contents of `SKILL.md`
4. Done! The skill is now available in all your conversations.

**Step 3:** Verify installation
Ask Claude: *"Do you have the portfolio-showcase-generator skill?"*

**Need detailed instructions?** See [INSTALL.md](INSTALL.md)

---

## Quick Start

### Example 1: From GitHub Repository
```
Use the portfolio-showcase-generator skill to create materials 
for my project at github.com/username/my-awesome-project
```

### Example 2: From Project Description
```
I built a real-time analytics pipeline using Python, Kafka, and 
PostgreSQL. It processes 100K events/second and reduced ML model 
training time from 6 hours to 45 minutes. Use the 
portfolio-showcase-generator skill to create an executive summary, 
technical deep-dive, and interview stories.
```

### Example 3: Interview Prep Focus
```
I'm interviewing for a staff engineer role. Use the 
portfolio-showcase-generator skill to create STAR stories from 
my microservices migration project.
```

---

## Usage Examples

### Scenario 1: Job Application Package
**Input:**
> "I need portfolio materials for my flight tracking system. It's a .NET 8.0 API with React frontend on Azure. I integrated data from three vendor APIs, used DDD patterns, and deployed to a Zero Trust environment. Create executive summary, technical deep-dive, and STAR stories."

**Output:**
- Executive summary (212 words)
- Technical deep-dive (2,500 words)
- 3 architecture diagrams
- 4 STAR stories
- Metrics dashboard
- Resume bullets

### Scenario 2: Side Project Showcase
**Input:**
> "I built DocFlow, an AI-powered whiteboard scanner using computer vision and OCR. Create materials for my portfolio site including architecture diagrams."

**Output:**
- Technical deep-dive emphasizing ML/CV skills
- Architecture diagrams (ML pipeline, system design)
- GitHub Pages structure
- Demo walkthrough content

### Scenario 3: Quick Resume Update
**Input:**
> "I led a microservices migration that reduced deployment time from 2 hours to 15 minutes and improved uptime from 95% to 99.5%. Just need an executive summary."

**Output:**
- 180-word executive summary
- 3 resume bullet points
- LinkedIn summary enhancement

**More examples:** See [EXAMPLES.md](EXAMPLES.md) for usage patterns, or browse the [examples/](examples/) folder for complete generated showcases.

---

## Input Formats

The skill accepts multiple input formats (mix and match):

### 1. GitHub Repository
```
"Analyze my project at github.com/username/repo"
```
The skill will analyze:
- Code structure and patterns
- Tech stack and dependencies
- Architecture decisions
- Documentation

### 2. Project Description
```
"I built a system that [what it does]. Tech stack: [technologies]. 
Key achievements: [metrics]."
```

### 3. Existing Documentation
Upload files like:
- README.md
- Architecture docs
- Technical specs
- Project notes

### 4. Conversational
```
"I want to showcase my authentication service. It handles 50K 
requests/second and uses OAuth 2.0..."
```

---

## Output Samples

### Executive Summary Sample
```markdown
Led development of real-time analytics platform processing 100K+ 
events/second, reducing ML model training time from 6 hours to 45 
minutes. Architected event-sourced system using Kafka, PostgreSQL, 
and Python with CQRS patterns, enabling 10x throughput increase 
while maintaining sub-100ms latency. Implemented comprehensive 
observability with distributed tracing and custom metrics, 
achieving 99.9% uptime across 8-month production run.
```

### STAR Story Sample
```markdown
**Situation**: Three months post-launch, our analytics pipeline 
began experiencing cascading failures under peak load...

**Task**: As lead engineer, I needed to redesign the system to 
handle 10x growth (10K → 100K events/sec) without complete rebuild...

**Action**: I implemented event sourcing with CQRS, added backpressure 
handling with Kafka consumer groups, and introduced circuit breakers 
for downstream dependencies...

**Result**: Achieved 100K events/sec throughput (10x improvement), 
reduced ML training time from 6 hours to 45 minutes through real-time 
data freshness, and improved system reliability to 99.9% uptime.
```

---

## Use Cases

### For Job Seekers
- Create ATS-optimized resume bullets
- Build compelling LinkedIn profiles
- Generate interview preparation materials
- Develop portfolio website content

### For Engineers
- Document technical achievements
- Showcase side projects professionally
- Prepare for promotion reviews
- Build GitHub portfolio pages

### For Hiring Managers
- Help team members document their work
- Create project case studies
- Build team capability presentations
- Prepare award nominations

### For Consultants
- Create client deliverable summaries
- Build project showcases
- Develop technical proposals
- Document success stories

---

## Project Structure

```
portfolio-showcase-generator/
├── README.md                    # This file
├── SKILL.md                     # The actual skill definition
├── INSTALL.md                   # Detailed installation guide
├── EXAMPLES.md                  # Comprehensive usage examples
├── ABOUT.md                     # Promotional overview
├── LICENSE                      # MIT License
└── examples/                    # Sample outputs
    ├── flifo-showcase.md        # Enterprise .NET project sample
    ├── ml-pipeline-showcase.md  # ML/Data engineering sample
    └── microservices-showcase.md # Microservices migration sample
```

---

## Contributing

Contributions are welcome! Here's how you can help:

### Report Issues
- Found a bug? [Open an issue](../../issues)
- Have a feature request? [Start a discussion](../../discussions)

### Improve the Skill
- Submit pull requests with improvements
- Add example outputs to help others
- Improve documentation

### Share Your Experience
- Star the repo if you find it useful
- Share your success stories
- Write blog posts about how you used it

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## Acknowledgments

- Built for the Claude AI platform by [Anthropic](https://anthropic.com)
- Inspired by the need for better technical portfolio materials
- Created using the [skill-creator](https://github.com/anthropics/skill-creator) skill

---

## Contact & Support

- **Issues**: [GitHub Issues](../../issues)
- **Discussions**: [GitHub Discussions](../../discussions)
- **Twitter**: Share your results with #ClaudeSkills

---

## Star History

If this skill helped you land an interview or showcase your work, consider giving it a star!

---

**Made for engineers building amazing things**