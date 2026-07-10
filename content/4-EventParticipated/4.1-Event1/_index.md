---
title: "Event 1"
date: 2026-05-23
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# Attended Events

---

## Event 1: Build Second Brain – Context is Everything



### Event Objectives

* Introduce the role of context in using AI effectively.
* Share how to build a “Second AI Brain” for learning and work.
* Help participants understand how to organize information, documents, and notes.
* Guide students on how to start building useful AI projects.

### Speaker

* **Tinh Truong** - Platform Engineer, GoTymeX

### Key Highlights

#### Context is important when working with AI

The speaker emphasized that current AI models are already powerful, but results are often not good because users provide insufficient context. A vague request often produces a generic, incorrect, or constraint-missing answer.

Important context elements include:

* The goal to achieve.
* The current situation of the user.
* Constraints related to technology, timeline, budget, and output format.
* Related documents, examples, requirements, or source code.

#### Common mistakes when using AI

Some common mistakes presented included:

* Providing too many unrelated documents in the prompt.
* Giving redundant information that AI already knows.
* Not clearly defining the goal, audience, and success criteria.

From this, participants learned that context quality is more important than context quantity.

#### From Prompt to Context and Memory

The session introduced the evolution from asking AI isolated questions to building systems with context and memory. A Second AI Brain can remember what the user is learning, understand projects and goals, and retrieve the right information before generating an answer.

#### How a Second AI Brain works

A simple workflow includes:

* **Store:** Store notes, documents, and source code.
* **Retrieve:** Retrieve relevant information.
* **Generate:** Generate answers based on context.
* **Learn:** Save useful information for future use.

### Key Takeaways

* AI cannot fully understand the goal if users do not provide context.
* Good context makes answers more accurate, concise, and relevant.
* Users should not put all documents into AI, but should select the most important information.
* Context Engineering is becoming an important future skill.
* A Second AI Brain combines context and memory to support long-term learning.

### Applying to Work

* Build a personal note system for AWS services learned during the internship.
* Record errors, solutions, and best practices during labs.
* Organize documents by project, module, and learning objective.
* Use AI to summarize documents, explain code, and support revision.
* Apply the framework: Goal, Relevant Info, Constraints, and Success Criteria when working with AI.

### Event Experience

The session changed my perspective on using AI for learning and work. I realized that AI does not only depend on how powerful the model is, but also depends heavily on how users provide information.

Through the topic of Second AI Brain, I understood the importance of building a well-organized note system with context and reusability. This knowledge is very useful for IT students, especially when learning many AWS services and working on practical projects.

---
## Event 2: Friendly AI Assistant with Amazon Quick


### Event Objectives

* Introduce Amazon Quick Suite and the ability to build a friendly AI Assistant.
* Present how AI supports business users in analysis and workflow automation.
* Share practical use cases such as a PM Assistant.
* Help participants understand the role of agentic AI in enterprises.

### Speaker

* **Pham Ng Hai Anh** - G-AsiaPacific Vietnam, AWS Community Builder

### Key Highlights

#### Problems faced by business users

The speaker explained that a typical working day for business users often includes many difficulties such as:

* Collecting and analyzing information from multiple sources.
* Consulting experts when working with specialized data.
* Repeating manual and time-consuming tasks.
* Difficulty connecting data, actions, and insights in one experience.

#### Amazon Quick Suite

Amazon Quick Suite was introduced as a unified experience for agentic AI in enterprises. The platform combines:

* Company data: spaces, datasets, and user-uploaded files.
* World knowledge and web search.
* Bedrock models.
* More than 40 data connectors.
* Thousands of actions in third-party applications.
* Governance, security, access control, and guardrails.

#### Automation capabilities

Amazon Quick Suite can support teams such as:

* Sales.
* Marketing.
* HR.
* Support.
* Project Management.

Key capabilities include chat, research, insights, dashboards, scenarios, and automation flows.

#### Use case: PM Assistant

One highlighted example was a PM Assistant that can:

* Automatically create meeting minutes.
* Send emails to stakeholders.
* Schedule the next meeting.
* Help reduce repetitive tasks in project management.

### Key Takeaways

* AI Assistants can help business users save significant time.
* Enterprise data must be integrated securely and with proper control.
* Agentic AI does not only answer questions but can also perform actions.
* Governance, guardrails, and regulatory compliance are important when deploying AI in enterprises.
* AI can support workflow automation across different departments.

### Applying to Work

* Apply the AI Assistant idea to an AWS learning support system.
* Build a chatbot to help search internship documents.
* Automate tasks such as meeting summaries, note-taking, and email sending.
* Learn more about Bedrock, data connectors, and workflow automation.
* Design AI systems with access control and data security.

### Event Experience

The event helped me better understand how AI can be applied in enterprise environments, not only as a chatbot but also as an assistant that can connect data, analyze information, and perform actions.

The PM Assistant demo helped me clearly imagine how AI can support daily work such as creating meeting minutes, sending emails, and scheduling meetings. These tasks may be small, but automating them can save a lot of time and improve work efficiency.

---
## Event 3: From Edge To Origin – CloudFront as Your Foundation


### Event Objectives

* Introduce Amazon CloudFront not only as a CDN but also as a foundation for application protection and optimization.
* Present challenges related to cost, security, resiliency, and performance.
* Share best practices for designing applications from Edge to Origin.
* Help participants understand how CloudFront protects origins and optimizes user experience.

### Speaker

* **Nguyen Tuan Thinh** - DevOps Engineer, First Cloud AI Journey

### Key Highlights

#### CloudFront and cost challenges

The speaker analyzed the challenges of the pay-as-you-go model when traffic suddenly increases or when an application is attacked by DDoS. CloudFront can help predict costs better through fixed-price CDN + security plans, including CDN, WAF, DDoS protection, DNS, logging, and storage credits.

#### AWS Edge Network infrastructure

CloudFront uses a large Edge network with many PoPs, Regional Edge Caches, and private capacity between regions. This allows user requests to be handled closer to users, reducing latency and increasing stability.

#### Protecting systems from the Edge

CloudFront can block unwanted traffic closer to the attack source and reduce load on the origin. Features mentioned included:

* AWS Shield / Shield Advanced.
* WAF rate limiting.
* Request collapsing.
* Origin Shield.
* Geographic restriction.
* Signed URL.
* Origin Access Control.
* VPC Origin and origin cloaking.

#### Performance and reliability optimization

CloudFront supports:

* Multi-layer caching.
* HTTP compression.
* HTTP/3.
* Persistent connections to origin.
* Origin failover.
* Custom error pages.
* CloudFront Functions and Lambda@Edge.

### Key Takeaways

* CloudFront is not only used to cache static content but also acts as a foundation layer for application protection.
* Caching helps reduce origin load, reduce cost, and increase availability.
* Security should be implemented from the Edge, not only at the backend.
* Origins should be hidden from the public internet to avoid bypassing CloudFront.
* HTTP compression, HTTP/3, and persistent connections significantly improve performance.

### Applying to Work

* Apply CloudFront to static websites hosted on S3.
* Combine CloudFront with WAF to protect frontend applications.
* Use OAC to restrict direct access to S3 origins.
* Optimize APIs and web applications using suitable caching strategies.
* Design architecture with origin failover and custom error pages to improve reliability.

### Event Experience

The session helped me understand Amazon CloudFront more deeply. Previously, I only considered CloudFront as a CDN for accelerating websites, but after the event I realized that CloudFront also plays an important role in security, cost optimization, and resiliency.

Examples about DDoS, request collapsing, signed URLs, and origin cloaking helped me understand how to protect real applications on AWS. This content is very useful for the Serverless E-Commerce project I am building because the system uses S3 frontend hosting, CloudFront, WAF, and backend APIs.

---

## Event 4: 36 hrs with LotusHacks – Building UTMorpho from Idea to Reality



### Event Objectives

* Share the journey of joining LotusHacks 2026 within 36 hours.
* Introduce the process of building UTMorpho from idea to demo.
* Present the challenges of developing an AI product in a short time.
* Draw lessons about teamwork, MVP development, and product thinking.

### Speaker

* **Team VIB**

### Key Highlights

#### Why the team joined LotusHacks

Team VIB shared that LotusHacks is one of the largest hackathons in Vietnam, where teams have 36 hours to build a complete product. The goal was not only to compete but also to learn, challenge themselves, and experience working under time pressure.

#### From idea to UTMorpho

At first, the team had difficulty choosing an idea. After several brainstorming sessions, they identified a real problem: AI UI generation tools often create interfaces that are difficult to edit. If users want to change a small detail, they have to prompt again, which can easily change the entire layout, colors, or spacing.

From this problem, UTMorpho was created with the goal of generating UI with AI while still allowing users to edit directly on the canvas.

#### Building within 36 hours

The team built the product through several stages:

* Set up the repository, AWS access, and role division.
* Build the backend skeleton and generation endpoint.
* Integrate the first AI call.
* Develop the generator, inline editor, and state synchronization.
* Cut features to protect the demo path.
* Finalize the demo flow, video, and pitch.

#### UTMorpho product overview

UTMorpho has several key features:

* Prompt to UI in seconds.
* Edit directly on the canvas without re-prompting.
* Keep consistency across edits.
* Token-aware design to reduce iteration cost.
* Export UI to React.

### Key Takeaways

* Good ideas often come from real problems experienced by the builders themselves.
* Hackathons test pressure handling, teamwork, and quick decision-making.
* MVP should focus on the demo path instead of too many features.
* Token cost is an important design constraint in AI products.
* AI can act as a teammate during the product development process.

### Applying to Work

* Apply MVP thinking when building AWS projects.
* Focus on solving real user pain points.
* Divide tasks clearly when working in a team.
* Integrate AI into the frontend development workflow.
* Design AI systems with attention to token cost and user experience.

### Event Experience

Team VIB’s sharing was very inspiring because it was not only about technology but also about the process of building a real product under time pressure. I learned that a good product does not always start from a very big idea, but can start from a small problem that genuinely frustrates users.

The story of UTMorpho helped me better understand the role of teamwork, focus, and feature-cutting to complete an MVP. These are very practical experiences for my graduation project and personal project development.

---
## Event 5: Deep Dive Talk – How LLM Actually Works?



### Event Objectives

* Explain how Large Language Models generate responses.
* Clarify the role of temperature, top-p, and top-k.
* Analyze why “deterministic” settings can still produce different outputs.
* Share risk mitigation strategies when building production AI applications.

### Speaker

* **Dao Duc** - Solution Architect, Cloud Kinetics

### Key Highlights

#### How LLMs choose the next token

The speaker explained that LLMs generate text one token at a time. At each step, the model produces scores for tokens in its vocabulary, converts them into probabilities through softmax, and then selects the next token.

#### The role of Temperature

Temperature adjusts the probability distribution:

* T > 1: More random outputs.
* T = 1: Natural and creative outputs.
* T near 0: More consistent outputs.
* T = 0: Theoretically selects the token with the highest probability.

However, the speaker emphasized that temp = 0 does not guarantee fully reproducible results in practice.

#### Non-determinism in LLMs

An important finding was that the same prompt, same settings, and same seed can still produce different outputs. Causes include:

* Floating-point arithmetic on GPUs is not fully associative.
* GPUs execute operations in parallel with non-deterministic order.
* Inference batching on shared endpoints changes computation depending on the batch.

#### Impact in production

Non-determinism is important for high-reliability applications such as:

* Medical information retrieval.
* Legal document analysis.
* Financial planning.
* Benchmarking and regression testing.

#### Risk mitigation strategies

Some mitigation strategies include:

* Running multiple times and using majority voting.
* Using structured output such as JSON mode or function calling.
* Self-hosting models when infrastructure control is required.
* Designing systems that accept variance.
* Testing carefully and handling disagreements in downstream logic.

### Key Takeaways

* LLMs work by predicting the next token.
* Temperature = 0 does not remove all sources of non-determinism.
* GPU infrastructure and inference batching can affect outputs.
* Production AI applications should be designed to handle variance.
* Structured output and testing are important when building reliable AI systems.

### Applying to Work

* Do not treat LLM outputs as absolutely correct or always stable.
* Use JSON mode, function calling, or schema validation when structured output is needed.
* Design AI workflows with validation, retry, and majority voting when necessary.
* Increase testing for important AI features.
* Apply a “probabilistic system” mindset when building AI assistants.

### Event Experience

The session helped me understand more deeply how LLMs work behind the chat interface. Previously, I thought that setting temperature = 0 would always produce exactly the same result, but through this session I learned that there are still many sources of non-determinism from hardware, inference optimization, and batching.

This knowledge is very useful when building real AI applications, especially systems that require stable outputs such as enterprise chatbots, document analysis tools, or decision-support AI assistants.

---
## Event 6: Enterprise-Grade Multi-Agent System – The Case of Startup Credit Scoring


### Event Objectives

* Introduce multi-agent system architecture in the startup credit scoring problem.
* Analyze the difference between traditional banking data and startup data.
* Present how to build enterprise-grade AI systems.
* Share key factors related to security, compliance, guardrails, and ROI.

### Speaker

* **Vy Lam** - Senior Business Systems Analyst, VPBank

### Key Highlights

#### The difference between banking data and startup data

The speaker explained that traditional credit scoring systems are often suitable for established businesses with many years of financial statements, credit history, collateral assets, and predictable revenue.

Meanwhile, startups often have:

* Short operating history.
* No credit history.
* Key assets such as IP, team, and traction.
* New business models.
* Unstructured data from multiple sources.

Therefore, startups may be rejected not because they have poor potential, but because they do not fit the traditional data model.

#### Limitations of Single Agent

A single agent is suitable for simple tasks, one domain, linear workflows, or fast prototypes. However, in credit scoring, a single agent has many limitations:

* Context limit.
* Expertise dilution.
* Lack of checks and balances.
* Single point of failure.
* Not suitable for high-stakes decisions that require auditing.

#### Multi-Agent as a Virtual Credit Committee

The multi-agent architecture was presented as a virtual credit committee including:

* Manager.
* Financial Analyst.
* Market Analyst.
* Team Evaluator.
* Risk Assessor.
* Compliance Agent.

Each agent analyzes a separate domain and then produces a consensus output including credit score, risk rating, confidence, and audit trail.

#### Enterprise-Grade AI

An enterprise AI system needs to consider several pillars:

* Security: authentication, encryption, secrets management.
* Data Governance: PII handling, audit logging, data residency.
* Network: VPC isolation, private endpoints, zero-trust.
* Operations: monitoring, incident response, DR strategy.
* Human Factors: training, runbooks, knowledge transfer.
* Compliance: regulatory requirements, internal policies, certifications.

#### Guardrails and real deployment

The speaker also presented a guardrails framework consisting of input guardrails, processing guardrails, and output guardrails. In addition, the system can be deployed using the flow CrewAI → AgentCore Runtime → Docker → ECR → Bedrock → API Gateway.

### Key Takeaways

* Multi-agent systems are suitable for multi-domain problems that require auditability.
* Single agent is not always suitable for enterprise systems.
* Enterprise AI must be designed with security and compliance from the beginning.
* Guardrails are important for controlling input, processing, and output.
* ROI is an important factor when convincing businesses to deploy AI.

### Applying to Work

* Apply multi-agent thinking to complex problems.
* Design AI assistants with clear roles instead of using one agent to handle everything.
* Use IAM least privilege, Secrets Manager, CloudWatch, and X-Ray when deploying systems.
* Integrate guardrails to reduce risks such as prompt injection, hallucination, and bias.
* Build an AI implementation roadmap in stages: foundation, integration, pilot, and scale.

### Event Experience

The session gave me a more practical view of deploying AI in enterprise environments. I realized that for AI to work in production, creating a demo is not enough. The system needs security, monitoring, access control, compliance, and stable operations.

The startup credit scoring example was easy to understand because it showed why multiple specialized agents are needed instead of one single agent. This helped me expand my thinking when designing complex AI systems in the future.

#### Some event photos

{{< img src="images/4-EventParticipated/4.1-Event1/event1.jpg" alt="Images event" >}}
{{< img src="images/4-EventParticipated/4.1-Event1/event1a.png" alt="Images event" >}}

