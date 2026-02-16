# 💡 Usage Examples & Scenarios

> **Sample outputs:** Looking for complete generated showcases? See the [examples/](examples/) folder for full portfolio materials generated from real projects.

Comprehensive examples showing how to use the Portfolio Showcase Generator skill for different project types and use cases.

---

## 📋 Table of Contents

- [Quick Reference](#quick-reference)
- [By Project Type](#by-project-type)
- [By Use Case](#by-use-case)
- [By Output Format](#by-output-format)
- [Advanced Usage](#advanced-usage)
- [Real-World Examples](#real-world-examples)

---

## ⚡ Quick Reference

### Minimal Request
```
Use portfolio-showcase-generator to create materials for [project description]
```

### Full-Featured Request
```
Use portfolio-showcase-generator skill:
- Project: [description or GitHub URL]
- Outputs: [executive summary, technical deep-dive, STAR stories, diagrams]
- Target audience: [recruiters, architects, interviewers]
- Focus: [specific achievements or challenges]
```

---

## 🏗️ By Project Type

### Example 1: Enterprise Backend System

**Input:**
```
Use the portfolio-showcase-generator skill for my project:

I built DocFlow, an AI-powered documentation toolkit that transforms 
whiteboard photos into working code. Tech stack: .NET 8.0, C#, OpenCV, 
PyTorch/ONNX, Tesseract OCR. Key features:
- Computer vision pipeline with 92%+ accuracy on hand-drawn diagrams
- Genetic algorithm for diagram layout optimization
- Bidirectional C# ↔ Mermaid transformation
- 91+ automated tests with CI/CD integration

I need all materials: executive summary, technical deep-dive, 
STAR stories, and architecture diagrams.
```

**Output Includes:**
- Executive summary (230 words)
- Technical deep-dive (4,500 words)
- 3 architecture diagrams (System, Vision Pipeline, Genetic Algorithm)
- 4 STAR interview stories
- Metrics dashboard
- Resume bullets
- Interview talking points

---

### Example 2: Machine Learning Project

**Input:**
```
Use the portfolio-showcase-generator skill:

Project: DocFlow - AI-powered documentation toolkit
- Computer vision for whiteboard scanning
- OCR with custom-trained models (TensorFlow)
- Object detection for diagram extraction
- Python, FastAPI, PostgreSQL
- Achieved 92% accuracy on hand-drawn diagrams
- Reduced documentation time by 60%

Need: Technical deep-dive and architecture diagrams
```

**Output Includes:**
- ✅ ML-focused technical deep-dive
- ✅ ML pipeline architecture diagram
- ✅ Model training workflow diagram
- ✅ Accuracy metrics and benchmarks
- ✅ Challenge-solution narratives

---

### Example 3: Microservices Migration

**Input:**
```
Use portfolio-showcase-generator skill:

Led microservices migration:
- Broke 5 monolithic services into 23 microservices
- Java Spring Boot → Spring Cloud
- Deployed on Kubernetes (AWS EKS)
- Reduced deployment time: 2 hours → 15 minutes
- Improved uptime: 95% → 99.5%
- Led team of 4 engineers over 8 months

Just need executive summary for resume.
```

**Output Includes:**
- ✅ Executive summary (180 words)
- ✅ 3 resume bullet points
- ✅ Key metrics highlighted
- ✅ Leadership emphasis

---

### Example 4: Full-Stack Application

**Input:**
```
I built a SaaS task management platform:
- React + TypeScript frontend
- Node.js + Express backend
- PostgreSQL + Redis
- Real-time collaboration with Socket.io
- Stripe payment integration
- 1,000+ active users
- $5K MRR in 6 months

Use portfolio-showcase-generator to create GitHub Pages content.
```

**Output Includes:**
- ✅ Project overview for landing page
- ✅ System architecture diagram
- ✅ Feature highlights
- ✅ Technical implementation details
- ✅ Growth metrics
- ✅ Demo walkthrough structure

---

### Example 5: Infrastructure/DevOps Project

**Input:**
```
Use portfolio-showcase-generator:

Built CI/CD pipeline and observability platform:
- GitHub Actions → ArgoCD → Kubernetes
- Prometheus + Grafana monitoring
- ELK stack for logging
- Reduced deployment time: 45 min → 5 min
- 10x improvement in MTTR (mean time to recovery)
- Zero production incidents in 12 months

Need technical deep-dive and STAR stories.
```

**Output Includes:**
- ✅ Infrastructure-focused deep-dive
- ✅ CI/CD pipeline diagram
- ✅ Observability architecture diagram
- ✅ Incident response STAR story
- ✅ Deployment metrics

---

## 🎯 By Use Case

### Use Case 1: Job Application Package

**Scenario:** Applying for Senior Software Engineer position

**Input:**
```
I'm applying for a senior engineer role at [Company]. Use 
portfolio-showcase-generator for my authentication service project:

- OAuth 2.0 + OIDC implementation
- Handles 50K requests/second
- Multi-factor authentication
- Redis-backed session store
- 99.99% uptime
- Node.js, TypeScript, PostgreSQL

Create materials optimized for engineering hiring managers.
```

**Output Strategy:**
- Lead with business impact (50K req/sec, 99.99% uptime)
- Technical depth for engineers (OAuth, OIDC, session management)
- 2-3 STAR stories showing problem-solving
- Resume bullets with ATS keywords

---

### Use Case 2: Staff/Principal Interview Prep

**Scenario:** Preparing for staff engineer interview loop

**Input:**
```
Use portfolio-showcase-generator for interview prep:

Project: Real-time analytics platform
- Kafka + PostgreSQL + Python
- 100K events/second throughput
- Event sourcing + CQRS
- Reduced ML training time: 6h → 45min
- Handled 10x growth in 8 months

Need 4-5 STAR stories for staff-level interview focusing on:
- System design decisions
- Handling scale challenges
- Technical leadership
- Trade-off analysis
```

**Output Strategy:**
- 5 STAR stories targeting different competencies
- Emphasis on architectural thinking
- Trade-offs and alternatives discussed
- Impact on team and organization
- 90-120 second delivery per story

---

### Use Case 3: Portfolio Website

**Scenario:** Building personal portfolio site

**Input:**
```
I need GitHub Pages content for 3 projects:

1. E-commerce platform (React, Node.js, Stripe)
   - 10K orders/month
   - $100K revenue

2. Discord bot (Python, Discord.py)
   - 50K+ servers
   - 1M+ active users

3. Open source CLI tool (Rust)
   - 2K GitHub stars
   - 50K downloads

Use portfolio-showcase-generator to create showcase pages.
```

**Output Strategy:**
- Project overview for each
- Architecture diagrams
- Key features and metrics
- Demo/screenshot guidance
- GitHub Pages HTML structure
- Navigation between projects

---

### Use Case 4: Promotion Review

**Scenario:** Preparing for promotion to senior/staff level

**Input:**
```
Use portfolio-showcase-generator for promotion materials:

Past 12 months achievements:
- Led 3 major projects (fraud detection, payment processing, API gateway)
- Mentored 2 junior engineers
- Reduced infrastructure costs: $200K/year savings
- Improved system reliability: 99% → 99.9%
- Established engineering best practices (code review, testing standards)

Need comprehensive documentation showing impact and leadership.
```

**Output Strategy:**
- Leadership emphasis (mentoring, establishing standards)
- Business impact ($200K savings, reliability improvement)
- Technical contributions across multiple projects
- Organizational influence
- Metrics demonstrating growth

---

### Use Case 5: Conference Talk Proposal

**Scenario:** Submitting talk proposal about technical project

**Input:**
```
Use portfolio-showcase-generator:

Talk topic: "Building Real-Time Analytics at Scale"
Project: Event processing platform (100K events/sec)

Need:
- Compelling abstract (300 words)
- Technical depth showing expertise
- Architecture diagrams for slides
- Lessons learned
```

**Output Strategy:**
- Engaging abstract with hook
- Technical credibility established
- Architecture diagrams for presentation
- Key insights and takeaways
- Relatable challenges and solutions

---

## 📄 By Output Format

### Output Type 1: Executive Summary Only

**When to Use:**
- Resume/LinkedIn updates
- Quick project highlights
- Elevator pitches
- Cover letters

**Example Request:**
```
Use portfolio-showcase-generator:

Create ONLY executive summary for my API gateway project:
- GraphQL federation layer
- Handles 1M requests/day
- Reduced API latency by 40%
- Node.js, TypeScript, Redis
```

**Expected Output:**
- 150-250 words
- Business impact emphasized
- Key metrics highlighted
- Professional tone
- Copy/paste ready

---

### Output Type 2: Technical Deep-Dive Only

**When to Use:**
- Engineering blog posts
- Technical documentation
- Architecture reviews
- Portfolio site content

**Example Request:**
```
Use portfolio-showcase-generator:

Create technical deep-dive (no executive summary) for:
- Distributed cache implementation
- Redis Cluster + Consistent hashing
- Handled 100K QPS
- 99.99% cache hit rate

Target audience: Senior engineers and architects
```

**Expected Output:**
- 800-1500 words
- Architecture decisions with rationale
- Technical implementation details
- Challenges and solutions
- Performance analysis
- Trade-offs discussed

---

### Output Type 3: STAR Stories Only

**When to Use:**
- Interview preparation
- Performance reviews
- Promotion packets
- Award nominations

**Example Request:**
```
Use portfolio-showcase-generator:

Create 3 STAR stories for my database migration project:
- PostgreSQL → distributed database (CockroachDB)
- Zero downtime migration
- 50TB of data
- 1000+ tables

Stories should highlight:
1. Technical problem-solving (migration strategy)
2. Risk management (zero downtime approach)
3. Leadership (coordinating with 3 teams)
```

**Expected Output:**
- 3 complete STAR stories
- Each 150-200 words (90-120 seconds spoken)
- Different competencies highlighted
- Quantified results
- Interview-ready format

---

### Output Type 4: Architecture Diagrams Only

**When to Use:**
- Technical presentations
- Design documents
- Blog post illustrations
- Portfolio visuals

**Example Request:**
```
Use portfolio-showcase-generator:

Create architecture diagrams for my event-driven system:
- Kafka message broker
- Multiple consumer services
- PostgreSQL storage
- Redis cache layer
- REST API gateway

Need: System architecture, data flow, and deployment diagrams
```

**Expected Output:**
- 3 professional Mermaid diagrams
- Clear component relationships
- Labeled connections
- Deployment context
- Editable Mermaid source

---

## 🚀 Advanced Usage

### Advanced Example 1: Multiple Projects Portfolio

**Input:**
```
Use portfolio-showcase-generator to create comparative portfolio:

Projects:
1. Payment processing system (high-scale)
2. Admin dashboard (rapid development)
3. Background job processor (reliability focus)

Create overview showing diverse skills and consistent impact.
```

**Output Strategy:**
- Comparative analysis showing breadth
- Different strengths per project
- Consistent pattern of impact
- Comprehensive skill demonstration

---

### Advanced Example 2: Custom Formatting

**Input:**
```
Use portfolio-showcase-generator with customization:

Project: [description]

Custom requirements:
- Executive summary: 100 words max (very concise)
- Technical deep-dive: Focus on security aspects
- STAR stories: Emphasis on customer impact
- Diagrams: Include security boundaries
```

**Output Strategy:**
- Respects custom length requirement
- Focuses on specified aspects (security)
- Tailored STAR stories (customer impact)
- Specialized diagrams

---

### Advanced Example 3: Iterative Refinement

**First Request:**
```
Use portfolio-showcase-generator:
Create executive summary for my ML recommendation engine
```

**Follow-up:**
```
The executive summary is good, but:
- Add more emphasis on business metrics (revenue impact)
- Reduce technical jargon
- Make it more accessible to non-technical recruiters

Please revise.
```

**Strategy:**
- Start with default output
- Iterate based on specific needs
- Refine for target audience
- Adjust tone and emphasis

---

## 🌍 Real-World Examples

### Real Example 1: Career Transition

**Context:** Backend engineer transitioning to ML engineering

**Input:**
```
Use portfolio-showcase-generator:

I'm a backend engineer pivoting to ML. Showcase my hybrid project:
- Built recommendation system for e-commerce
- Backend: Python, FastAPI, PostgreSQL (my expertise)
- ML: TensorFlow, collaborative filtering (new skill)
- Improved conversion rate by 23%

Emphasize both backend strength and ML competency.
```

**Output Strategy:**
- Bridge experience (backend) with goal (ML)
- Show learning and adaptation
- Demonstrate impact in both domains
- Position as T-shaped engineer

---

### Real Example 2: Open Source Maintainer

**Context:** Showcasing open source contribution

**Input:**
```
Use portfolio-showcase-generator:

Project: Open source CLI tool (10K GitHub stars)
- Built in Rust
- 100K+ downloads/month
- 50+ contributors
- I'm lead maintainer
- Featured in [publication]

Need materials for jobs at companies valuing open source.
```

**Output Strategy:**
- Community impact metrics
- Technical contribution depth
- Leadership and mentorship
- Collaboration across organizations
- Public recognition

---

### Real Example 3: Startup Founding Engineer

**Context:** Employee #2 at startup, building portfolio

**Input:**
```
Use portfolio-showcase-generator:

Founding engineer at [Startup]:
- Built entire platform (full-stack)
- Scaled from 0 → 10K users
- Hired and led 4-person eng team
- Established all technical architecture
- React, Node.js, PostgreSQL, AWS

Showcase both building AND scaling skills.
```

**Output Strategy:**
- Zero-to-one capabilities highlighted
- Scaling challenges addressed
- Leadership development shown
- End-to-end ownership demonstrated
- Startup context emphasized

---

## 📝 Templates for Common Requests

### Template 1: Quick Update
```
Use portfolio-showcase-generator:
Project: [name]
Tech: [stack]
Impact: [key metric]
Need: Executive summary only
```

### Template 2: Full Portfolio Piece
```
Use portfolio-showcase-generator skill:
Project: [detailed description]
Context: [business problem, constraints]
Tech Stack: [technologies]
Key Achievements: [metrics]
Challenges: [what was hard]
Need: All materials (summary, deep-dive, STAR stories, diagrams)
Target: [recruiter/architect/interviewer]
```

### Template 3: Interview Prep
```
Use portfolio-showcase-generator for interview prep:
Project: [description]
Interview Type: [company, role level]
Focus Areas: [competencies to demonstrate]
Need: 3-4 STAR stories, 90-120 seconds each
```

---

## 💡 Pro Tips

### Tip 1: Provide Context
More context = better output. Include:
- Why the project mattered (business context)
- What was challenging (technical constraints)
- How you solved it (your approach)
- What the impact was (metrics)

### Tip 2: Specify Your Audience
Output varies significantly by audience:
- Recruiters: Business impact, clear results
- Engineers: Technical depth, implementation details
- Executives: Strategic value, organizational impact

### Tip 3: Include Metrics
Quantify everything possible:
- Performance (latency, throughput)
- Scale (users, requests, data volume)
- Business (revenue, cost savings, efficiency)
- Quality (uptime, error rates, test coverage)

### Tip 4: Iterate
Don't expect perfection on first try:
1. Start with basic request
2. Review output
3. Request specific adjustments
4. Refine until satisfied

### Tip 5: Save Your Work
The skill generates markdown - save outputs for:
- Resume updates
- LinkedIn profiles
- Interview prep docs
- Portfolio websites

---

## FAQ

**Q: Can I use this for multiple projects?**

A: Yes! Run the skill for each project, then combine outputs for a comprehensive portfolio.

---

**Q: How detailed should my input be?**

A: More detail = better output. Minimum: project description, tech stack, 1-2 key achievements.

---

**Q: Can I customize output length?**

A: Yes! Specify desired length: "Create a 150-word executive summary" or "Keep technical deep-dive under 1000 words."

---

**Q: What if I don't have metrics?**

A: The skill will work with what you have, but try to include:
- Approximate scale (users, data volume)
- Relative improvements (faster, more reliable)
- Qualitative impacts (enabled new features, improved UX)

---

**Q: Can I use this for team projects?**

A: Yes! Focus on your specific contributions: "I built the authentication layer..." or "I led the database migration..."

---

**Ready to create amazing portfolio materials? Check out the [README](README.md) for installation instructions!**