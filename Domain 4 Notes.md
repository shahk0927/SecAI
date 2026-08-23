## Domain 4.0: AI Governance, Risk, and Compliance
 
### 4.1 Explain organizational governance structures that support AI
 
#### Organizational Structures
 
- **AI Center of Excellence (CoE):** Centralized cross-functional team that sets standards, evaluates tools, manages models, and advises business units on AI adoption. Prevents shadow AI and duplicated effort.
- **AI Policies and Procedures:** Written rules governing acceptable AI use, approved models, data handling, human oversight, and incident response. Foundation for enforcement and audit.
#### AI-Related Roles
 
- **Data Scientist:** Builds models, runs experiments, and analyzes data. Focus on statistical rigor and model performance.
- **AI Architect:** Designs the end-to-end AI system architecture including data pipelines, model serving, and integrations.
- **Machine Learning Engineer:** Productionizes models. Handles training pipelines, deployment infrastructure, scaling, and performance.
- **Platform Engineer:** Owns the underlying compute, storage, and networking (Kubernetes, GPU clusters, cloud accounts) that AI workloads run on.
- **MLOps Engineer:** Manages the ML lifecycle: CI/CD for models, versioning, monitoring, retraining, drift detection.
- **AI Security Architect:** Designs the security controls for AI systems: threat modeling, guardrails, access control, data protection.
- **AI Governance Engineer:** Implements governance policies as code. Enforces model approval workflows, usage policies, and audit trails.
- **AI Risk Analyst:** Identifies, quantifies, and tracks AI-specific risks (bias, drift, regulatory exposure) and reports to leadership.
- **AI Auditor:** Independently reviews AI systems for compliance with internal policy and external regulation. Produces audit evidence.
- **Data Engineer:** Builds and maintains the data pipelines that feed AI systems. Owns data quality, lineage, and availability.
### 4.2 Explain risks associated with AI
 
#### Responsible AI
 
- **Fairness:** Model treats individuals and groups equitably. No disparate impact on protected classes.
- **Reliability and Safety:** Model performs consistently under expected conditions and fails gracefully under unexpected ones. Does not cause harm.
- **Transparency:** Users and stakeholders can understand what the AI does, what data it uses, and its limitations. Includes model cards and data sheets.
- **Privacy and Security:** Personal data is protected, and the model itself is defended against attack.
- **Explainability:** Ability to explain in human terms why the model made a specific decision. Required for regulated decisions (credit, hiring, healthcare).
- **Inclusiveness:** Model works for diverse users including different languages, abilities, and demographics.
- **Accountability:** Clear ownership of AI decisions and outcomes. Someone answers when it goes wrong.
- **Consistency:** Same inputs produce the same outputs across time and users, or variation is understood and bounded.
#### Risks
 
- **Introduction of Bias:** Model learns and amplifies bias from training data or design choices. Leads to unfair or discriminatory outcomes.
- **Accidental Data Leakage:** Sensitive data leaks through prompts, responses, logs, embeddings, or training data memorization.
- **Reputational Loss:** Public failure (biased output, hallucinated legal citation, deepfake incident) damages brand and trust.
- **Accuracy and Performance of the Model:** Model produces wrong or degraded results due to drift, poor data, or edge cases. Business decisions based on it fail.
- **Intellectual Property (IP)-related Risks:** Training on copyrighted material without license. Model outputs that reproduce protected content. Employees pasting proprietary code into public LLMs.
- **Autonomous Systems:** AI agents that take actions without sufficient oversight. Excessive agency risk: bad decisions execute in the real world (deleted data, sent money, wrong medical dose).
### 4.3 Summarize the impact of compliance on business use and development of AI
 
- **EU AI Act:** European Union's risk-based AI regulation. Classifies AI systems as unacceptable, high-risk, limited-risk, or minimal-risk. Bans some uses (social scoring), imposes strict requirements on high-risk uses (transparency, human oversight, conformity assessments). Applies extraterritorially if AI is used in the EU.
- **OECD Standards:** Organisation for Economic Co-operation and Development AI Principles. Non-binding international framework promoting inclusive growth, human-centered values, transparency, robustness, and accountability. Adopted by 40+ countries.
- **ISO AI Standards:** International Organization for Standardization publications on AI. Key ones: ISO/IEC 42001 (AI management system), ISO/IEC 23894 (AI risk management), ISO/IEC 23053 (ML framework), ISO/IEC 22989 (AI concepts and terminology).
- **NIST AI RMF:** National Institute of Standards and Technology AI Risk Management Framework. Voluntary US framework with four functions: Govern, Map, Measure, Manage. Widely adopted as baseline for AI risk programs.
#### Corporate Policies
 
- **Sanctioned vs. Unsanctioned:** Sanctioned = officially approved AI tools and models employees can use. Unsanctioned = "shadow AI" outside IT/security review. Enforcement via DLP, CASB, network controls.
- **Private vs. Public Models:** Private = models hosted internally or in a dedicated tenant where data is not used for training and stays under org control. Public = shared consumer/API models where data may be logged or used for training. Sensitive data belongs on private only.
- **Sensitive Data Governance:** Rules for what data can be sent to which AI systems. Classification-driven: e.g., Confidential data goes only to approved private models, no PHI in public LLMs.
- **Third-Party Compliance Evaluations:** Assessing AI vendors and models against your compliance requirements. Includes SOC 2 reports, ISO certifications, data processing agreements (DPAs), model cards, security questionnaires, and independent audits before procurement.
