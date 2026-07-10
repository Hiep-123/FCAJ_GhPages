---

title: "Event 2"
date: 2026-06-27
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

---



## Event 1:Deep Response Engine: From Detection to Autonomous Resolution



### Event Objectives

* Share a career journey from studying, working, joining AWS, and building a technology startup.
* Help students understand the importance of predicting market trends and choosing the right direction.
* Introduce real-world problems in Cloud Infrastructure operations.
* Present how AI Agents can support humans in incident investigation, cost optimization, security, and cloud operation.

### Speaker

* **Steve Tran** – Founder, Cloud Thinker

### Key Highlights

#### Career journey with Cloud

The speaker shared that he initially worked in a contact center environment where operating physical servers was complex, labor-intensive, and prone to hardware issues. From that experience, he started learning Cloud, studied AWS, and earned certifications to develop his career.

One important point emphasized was the ability to recognize market demand. During the strong growth of Cloud, enterprises needed many professionals in Cloud Engineering, DevOps, Reliability Engineering, and Solution Architecture.

#### AI and its impact on the job market

The speaker explained that AI will strongly affect hiring demand, especially for traditional developer roles. However, AI will not completely replace humans in critical fields such as Cloud Infrastructure, Production Operation, and Incident Response.

Instead, the market will require stronger engineers who can work effectively with AI and deeply understand production systems.

#### Cloud Infrastructure operation challenges

As enterprises move to the Cloud, their systems become larger and more complex. They need to manage many observability, monitoring, security, FinOps, and incident response tools. This creates high complexity and requires experienced engineers.

Cloud Thinker aims to build an agentic platform that supports engineers in operating systems faster, reducing investigation time, and improving productivity.

#### Multi-Agent and Single Agent

An important topic was the comparison between single-agent and multi-agent systems. A single agent can handle many tasks if designed well, but in large systems, multi-agent architecture helps optimize context, separate roles, and control task boundaries.

Multi-agent systems are useful when there is a need for:

* Specialized agents for different tasks.
* Role-based access control.
* Reduced context dilution.
* Better cost and performance optimization.
* Support for complex enterprise environments.

#### Problems solved by Cloud Thinker

The speaker shared several key areas:

* Incident investigation.
* Code review before production.
* FinOps and Cloud cost optimization.
* Security assessment.
* Helping developers debug CI/CD and infrastructure issues.

### Key Takeaways

* Choosing the right technology trend can strongly affect one’s career path.
* Cloud remains important, but Cloud engineers need to know how to use AI effectively.
* AI Agents should support humans, especially in critical systems.
* Multi-agent design helps divide responsibilities and control permissions better.
* Startups need to solve real customer problems, not just build interesting ideas.

### Applying to Work

* Learn AWS, DevOps, Cloud Infrastructure, and AI Agent concepts together.
* Build projects with monitoring, logging, alerting, and incident response.
* Apply FinOps thinking to optimize Cloud costs.
* When designing AI Agents, consider access control, approval flow, and task boundaries.
* Focus on solving real user problems in personal projects.

### Event Experience

Steve Tran’s sharing gave me a more practical view of career development in Cloud. I realized that learning technology is not only about following trends, but also about understanding market needs and preparing the right skills.

The discussion about AI Agents in Cloud Operation also helped me understand that AI can support more than coding. It can participate in complex operational processes such as incident response, cost optimization, and security. This knowledge is very useful for my Cloud Engineer direction and AWS project.


---

## Event 2: Voice Agents: Building Human-Like AI Conversations at Scale



### Event Objectives

* Introduce the basic components of a Voice AI system.
* Explain common architectures for building voice-based AI systems.
* Demonstrate a Voice Agent capable of answering questions based on a knowledge base.
* Share challenges when deploying Voice AI in enterprise environments, especially for Vietnamese.

### Speakers

* **Hieu Nghi** – Founder & CEO, R AI

### Key Highlights

#### Opportunities for Voice AI in Vietnam

The speaker shared that voice-based AI models have strong potential in Vietnam. However, Vietnamese voice data and Vietnamese speech models are still limited, creating many opportunities for research, project development, and real-world applications.

#### Voice AI architectures

The session presented two main architecture approaches:

* **Speech-to-Speech:** The user speaks, the model directly processes audio and returns audio.
* **Speech-to-Text → LLM → Text-to-Speech:** The system converts speech to text, sends the text to an LLM, and then converts the response back to speech.

For Vietnamese and enterprise use cases, the second approach is often easier to control because text output can be moderated, logged, and protected with guardrails before being converted into speech.

#### Voice Agent demo

The demo showed a Voice Agent answering questions about Apple products. The system was deployed on AWS, using Amazon Bedrock AgentCore and a knowledge base to provide domain-specific information.

The demo helped participants clearly imagine how a voice-based AI Agent can work in practice.

#### Enterprise deployment challenges

The speaker emphasized that deploying Voice AI for banks or large enterprises requires many considerations:

* Low latency and real-time streaming.
* Speech-to-Text and Text-to-Speech for Vietnamese.
* Tool calling so AI can perform actions, not only answer questions.
* Control over what the AI says.
* Audit logs and versioning.
* Knowledge base integration.
* Human handoff when AI cannot handle a situation.
* Handling gender, interruptions, conversation context, and regional accents.

### Key Takeaways

* Voice AI is not only speech-to-answer; it is a multi-component system.
* For Vietnamese, speech-to-text combined with LLM and text-to-speech may be more suitable than direct speech-to-speech.
* Tool calling is important for Voice AI to perform real tasks.
* Production systems need audit logs, versioning, knowledge bases, and human handoff.
* Vietnamese creates unique challenges such as pronouns, accents, gender, and interruption context.

### Applying to Work

* Learn how to build chatbots or voicebots using Amazon Bedrock.
* Apply the Speech-to-Text → LLM → Text-to-Speech architecture in AI projects.
* Design AI Assistants with knowledge base and tool calling capabilities.
* Consider guardrails, logging, and human handoff when building production AI.
* Research more about Vietnamese language processing in AI.

### Event Experience

The Voice AI session helped me understand how a voice-based AI Agent is built and operated. I was especially impressed by the demo because it showed that AI can interact more naturally through voice instead of only through a chat interface.

The discussion about enterprise deployment challenges also helped me realize that a production AI product requires much more than an initial demo, including speed, security, output control, knowledge base, and human handoff.

---

## Event 3: AWS DevOps Agent: Your Always-Available Operations Teammate



### Event Objectives

* Introduce the concept of DevOps AI Agent in system operations.
* Present difficulties when manually handling incidents in medium and large systems.
* Share how an agent can learn system context, analyze logs and traces, and suggest solutions.
* Help participants understand how AI supports DevOps Engineers in production environments.

### Speakers

* **Nguyen Nguyen** – Cloud Engineer, Cloud Kinetics
* **Bao Phan** – Cloud Engineer, Cloud Kinetics

### Key Highlights

#### Problems in system operations

The speaker gave an example where customers complain that a website is slow or has many errors. A DevOps Engineer must investigate the root cause using many sources of logs, traces, and monitoring data. However, telemetry is often fragmented, logs belong to different teams, and each system has its own domain context.

This increases the mean time to investigate and mean time to recovery, while also causing context loss when engineers cannot fully connect different incident signals.

#### DevOps AI Agent

DevOps Agent was introduced as a solution to automate incident investigation. The agent can be triggered by a CloudWatch alert or by a direct request from an engineer, then automatically analyzes data to identify possible causes and suggest solutions.

#### Context Learning and Agent Space

One key concept was Agent Space — a logical area that defines which resources, environments, and permissions the agent can access. The agent can learn system topology, understand relationships between components, and accumulate experience through memory after each incident.

#### Control, Integration, and Collaboration

A DevOps Agent needs clear control mechanisms:

* Which resources the agent can access.
* Resources selected by tag or environment.
* Ability to connect to Cloud, on-premises, or other environments.
* Ability to extend capabilities through MCP tools or integrations.
* Ability to support engineers during analysis and decision-making.

#### Agent limitations

The speaker also emphasized that the agent can only observe data exposed by the system. If application logs are not exported to CloudWatch or an observability system, the agent will struggle to analyze accurately. Therefore, good observability remains a critical foundation.

### Key Takeaways

* Manual incident handling takes time because data is distributed and context is missing.
* DevOps Agent can reduce investigation time and suggest solutions.
* The agent needs to learn topology, logs, metrics, and system dependencies.
* Control and access permissions are critical when deploying agents in production.
* Good observability is required for AI Agents to work effectively.

### Applying to Work

* Design AWS projects with CloudWatch Logs, Metrics, and X-Ray.
* Tag resources to support permission control and environment grouping.
* Build clear dashboards and alerts to support incident response.
* When using AI Agents, limit access using IAM least privilege.
* Learn more about MCP, Agent Space, and AI integration with DevOps workflows.

### Event Experience

The session helped me better understand the real difficulties DevOps Engineers face when handling incidents in large systems. Previously, I thought debugging only meant checking logs, but in reality, it requires combining multiple data sources, understanding system context, and connecting incident signals.

The DevOps Agent topic was very useful because it showed how AI can support engineers in repetitive and complex tasks, while still requiring proper permission control, data quality, and observability.


---

## Event 4: AI-Powered Productivity: Workforce Planning For Enterprise



### Event Objectives

* Analyze HR challenges in the AI era.
* Introduce Amazon Quick as a tool for HR and business users.
* Present how AI can transform scattered data into valuable business insights.
* Demonstrate how Amazon Quick supports HR-related tasks.

### Speakers

 * **Minh Anh** – Solution Architect, Noventis

### Key Highlights

#### HR challenges in the AI era

The speakers shared that HR teams now face many challenges in building workforce strategies, recruiting suitable employees, and handling scattered data. In the fast-growing AI era, HR not only manages people but also needs to use digital tools to make better decisions.

#### Amazon Quick for HR

Amazon Quick was introduced as a tool that can support HR in many tasks, from data analysis to workflow automation. It helps turn scattered data into insights, supporting enterprises in making more accurate decisions.

#### Agentic AI at work

Amazon Quick does not only answer questions but can also turn answers into actions. This helps users not only receive information but also complete tasks faster and reduce manual work.

#### Demo and real-world applications

The demo showed that Amazon Quick can be used across multiple platforms such as web, desktop, and mobile. It can remember context through a memory graph, connect data, and support users during work.

### Key Takeaways

* HR can use AI to analyze data and optimize recruitment workflows.
* Amazon Quick helps transform scattered data into usable insights.
* Agentic AI can support actions, not only answer questions.
* Memory and context help AI understand users better over time.
* AI helps people focus on higher-value professional work.

### Applying to Work

* Apply Amazon Quick or AI Assistant concepts to support internship document management.
* Build a chatbot to search HR or project information.
* Use AI to summarize documents, analyze data, and generate insights.
* Design AI systems with memory, context, and data permission control.
* Learn more about AI applications in enterprise management.

### Event Experience

The session helped me understand that AI is not only for developers but can also support departments such as HR, Sales, Marketing, and Operations. For HR specifically, AI can help process large amounts of data, reduce manual work, and create insights for workforce decisions.

The Amazon Quick content gave me a clearer view of how enterprises can deploy AI Assistants to support employees in daily work.

---

## Event 5: Building Secure Private MCP Connection with Amazon Quick



### Event Objectives

* Present security requirements when deploying Amazon Quick in enterprise environments.
* Introduce how to connect Amazon Quick with MCP Server privately and securely.
* Analyze risks when MCP Server is exposed publicly on the internet.
* Share an architecture using VPC Connection, private subnet, ALB, Cognito, and TLS to protect the connection.

### Speakers

* **Toan Nguyen** – AWS Security Builder
* **Hieu Nghi** – Renova Cloud

### Key Highlights

#### Amazon Quick in enterprise environments

The speaker explained that when using Amazon Quick at the enterprise level, the concern is not only whether the tool works. Enterprises also need to care about security, policies, private connectivity, and how data moves between systems.

#### MCP Server and third-party integration

MCP Server acts as a bridge between Amazon Quick and external systems such as Gmail, Jira, Zalo, WhatsApp, Facebook, YouTube, or internal APIs. If a third party provides an API and proper permissions are granted, Amazon Quick can connect through MCP Server to perform tasks.

#### Risks of public endpoints

If MCP Server is exposed to the public internet, the system may face risks such as:

* DoS attacks.
* Increased attack surface.
* Man-in-the-Middle attacks.
* Data traveling through the public internet.
* Failure to meet Zero Trust or data residency requirements.

#### Secure connection with VPC Connection

The proposed solution is to place MCP Server in a private subnet and use VPC Connection so Amazon Quick can access it internally. The architecture may include:

* Amazon Quick.
* VPC Connection.
* Private DNS.
* Interface endpoint.
* ALB.
* Cognito for authentication/authorization.
* TLS certificate through ACM.
* MCP Server in a private subnet.

This approach avoids public endpoints, reduces security risks, and better fits enterprise requirements.

### Key Takeaways

* Enterprise AI Assistants must be designed with security from the beginning.
* MCP Server helps AI connect to many external systems through APIs.
* Public endpoints can create many security risks.
* VPC Connection and private subnets enable private connectivity and reduce internet exposure.
* Authentication, authorization, TLS, and private DNS are important security components.

### Applying to Work

* When designing AI Assistants, avoid exposing sensitive endpoints publicly if not necessary.
* Use private subnets, ALB, TLS, and IAM/Cognito to protect systems.
* Apply Zero Trust and least privilege principles.
* Design AI backends that securely connect with internal APIs.
* Learn more about VPC, private connectivity, MCP Server, and enterprise AI security.

### Event Experience

The session helped me understand that when deploying AI in enterprises, security is a mandatory requirement, not an optional add-on. An AI Assistant can be powerful, but if it connects to internal systems through the public internet, it creates many risks.

The presentation about Amazon Quick connecting to MCP Server through VPC Connection helped me better imagine how to build secure AI architecture suitable for large enterprises and systems with strict security requirements.

#### Some event photos

![Images event](/images/4-EventParticipated/4.2-Event2/event2.jpg)
![Images event](/images/4-EventParticipated/4.2-Event2/event2a.png)
---
