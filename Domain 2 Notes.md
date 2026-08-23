## Domain 2.0: Securing AI Systems
 
### 2.1 Given a scenario, use AI threat-modeling resources
 
#### OWASP Top 10
 
- **OWASP:** Open Web Application Security Project. Publishes vendor-neutral security guidance.
- **OWASP LLM Top 10:** Top 10 security risks for LLM applications. Covers prompt injection, insecure output handling, training data poisoning, model DoS, supply chain, sensitive info disclosure, insecure plugin design, excessive agency, overreliance, and model theft.
- **OWASP ML Security Top 10:** Top 10 risks specific to ML systems more broadly. Covers input manipulation, data poisoning, model inversion, membership inference, model theft/extraction, corrupted packages, transfer learning attacks, model skewing, output integrity attacks, and neural net reprogramming.
#### Other Threat Resources
 
- **MIT AI Risk Repository:** Massachusetts Institute of Technology's structured database of documented AI risks, categorized by cause (human vs AI), intent, and timing. Reference source for risk identification.
- **MITRE ATLAS:** Adversarial Threat Landscape for Artificial-Intelligence Systems. MITRE's ATT&CK-style knowledge base of tactics, techniques, and case studies for attacks on ML systems.
- **CVE AI Working Group:** Common Vulnerabilities and Exposures working group extending the CVE system to cover AI/ML-specific vulnerabilities.
- **Threat-Modeling Frameworks:** Structured approaches like STRIDE, PASTA, LINDDUN, and MITRE ATT&CK adapted for AI systems. Force teams to systematically identify threats before build.
### 2.2 Given a set of requirements, implement security controls for AI systems
 
#### Model Controls
 
- **Model Evaluation:** Testing the model against benchmarks, adversarial inputs, and bias suites before and after deployment.
- **Model Guardrails:** Rules and filters built into or around the model that block unsafe input or output (violence, PII, off-topic, jailbreaks).
  * **Prompt Templates:** Predefined prompt structures with fixed instructions and validated placeholders. Reduces prompt injection and enforces consistent behavior.
#### Gateway Controls
 
- **Prompt Firewalls:** Inline layer that inspects prompts and responses for injection, PII, policy violations, and malicious patterns before they reach or leave the model.
- **Rate Limits:** Caps on requests per second/minute/user to prevent DoS and abuse.
- **Token Limits:** Caps on input and output tokens per request. Controls cost and prevents context flooding attacks.
- **Input Quotas:** Limits on volume of data submitted.
  * **Data Size:** Maximum bytes per input (e.g., file upload size).
  * **Quantity:** Maximum number of items per request or per session.
- **Modality Limits:** Restricting which input types are allowed (text only, no images, no audio). Reduces attack surface.
- **Endpoint Access Controls:** Restricting which users, apps, or networks can reach the model API. Enforced via IAM, API keys, mTLS, IP allowlists.
- **Guardrail Testing and Validation:** Red-teaming the guardrails with jailbreaks, injection payloads, and edge cases to confirm they hold. Guardrails are only as good as their tests.
### 2.3 Given a scenario, implement appropriate access controls for AI systems
 
- **Model Access:** Who can query, fine-tune, or modify the model itself. Enforced by RBAC/ABAC, API keys, and workspace isolation.
- **Data Access:** Who can read, write, or modify the training data, fine-tuning data, and RAG source documents. Row/column-level controls where possible.
- **Agent Access:** Which tools, APIs, files, and systems an AI agent is authorized to invoke on the user's behalf. Least privilege is critical since agents act autonomously.
- **Network/API Access:** Firewalling and gating the model endpoints. Private endpoints, VPC peering, service accounts, and API gateways to isolate the model from the open internet.
### 2.4 Given a scenario, implement data security controls for AI systems
 
#### Encryption Requirements
 
- **In Transit:** Data protected during network transfer. TLS 1.2+/1.3, mTLS, HTTPS between client, gateway, and model.
- **At Rest:** Data protected when stored on disk. AES-256, KMS-managed keys, encrypted databases and object stores.
- **In Use:** Data protected while being processed in memory. Confidential computing, secure enclaves (Intel SGX, AWS Nitro Enclaves), homomorphic encryption.
#### Data Safety
 
- **Data Anonymization:** Irreversibly removing identifiers so a record cannot be linked back to an individual. Stronger than pseudonymization.
- **Data Classification Labels:** Tagging data by sensitivity (Public, Internal, Confidential, Restricted) so controls can be applied programmatically.
- **Data Redaction:** Permanently removing or blacking out sensitive fields from documents or responses.
- **Data Masking:** Replacing real values with realistic but fake ones (e.g., "555-01-1234" for an SSN). Preserves format for testing.
- **Data Minimization:** Collecting and retaining only the data actually needed for the stated purpose. Core GDPR principle and reduces breach blast radius.
### 2.5 Given a scenario, implement monitoring and auditing for AI systems
 
#### Prompt Monitoring
 
- **Query:** Logging the input prompts sent to the model. Needed for abuse detection, injection forensics, and cost attribution.
- **Response:** Logging the model output. Needed to detect data leakage, hallucinations, and policy violations.
- **Log Monitoring:** Actively watching logs for suspicious patterns (repeated jailbreak attempts, unusual data volumes, off-hours access).
- **Log Sanitization:** Stripping or masking sensitive data (PII, secrets, PHI) from logs before storage. Logs are a data leak vector.
- **Log Protection:** Encrypting logs, restricting access, and using write-once storage or SIEM ingestion to prevent tampering.
- **Response Confidence Level:** Score indicating how sure the model is about its answer. Low confidence responses can be flagged for human review.
- **Rate Monitoring:** Tracking request frequency per user, key, or IP to detect abuse, scraping, or model extraction attempts.
#### AI Cost Monitoring
 
- **Prompts:** Tracking cost of input tokens per user, app, or team. Prompt injection can drive costs up.
- **Storage:** Cost of storing training data, embeddings, vector DBs, model artifacts.
- **Response:** Cost of output tokens generated. Output tokens usually cost more than input.
- **Processing:** Cost of compute (GPU/TPU hours) for training, fine-tuning, and inference.
#### Auditing for Quality and Compliance
 
- **Hallucinations:** Auditing outputs for fabricated facts, sources, or citations. Common LLM failure mode.
- **Accuracy:** Comparing model output to known-correct answers or ground truth on a regular basis.
- **Bias and Fairness:** Testing whether the model performs equally across demographic groups. Required for regulated use cases.
- **Access:** Auditing who accessed the model, data, and outputs. Needed for compliance (SOC 2, ISO 27001, HIPAA).
### 2.6 Given a scenario, analyze the evidence of an attack and suggest compensating controls for AI systems
 
#### Attacks
 
- **Prompt Injection:** Attacker crafts input that overrides the system prompt or hijacks the model's behavior. Direct (in the user prompt) or indirect (hidden in retrieved documents/web content).
- **Poisoning:** Corrupting the model or its training pipeline.
  * **Model Poisoning:** Tampering with the model weights or fine-tuning data to install backdoors or biases.
  * **Data Poisoning:** Injecting malicious samples into training data so the model learns attacker-controlled behavior.
- **Jailbreaking:** Bypassing the model's safety guardrails using role-play, obfuscation, or crafted prompts to make it produce restricted content.
- **Hallucinations:** Model confidently outputs false information. Can be weaponized (fake case law, fake package names for supply chain attacks).
- **Input Manipulation:** Crafting inputs (adversarial examples) that cause misclassification while looking normal to humans.
- **Introducing Biases:** Skewing training or fine-tuning data to make the model discriminate or produce attacker-preferred outputs.
- **Circumventing AI Guardrails:** Techniques (encoding, translation, indirect phrasing) that get past safety filters without formal jailbreak.
- **Manipulating Application Integrations:** Abusing the AI's connections to plugins, tools, or APIs to trigger unintended actions.
- **Model Inversion:** Reconstructing training data from the model by querying it strategically. Privacy attack.
- **Model Theft:** Copying the model weights directly (insider, breach) or reconstructing them via extensive querying (extraction).
- **AI Supply Chain Attacks:** Compromising upstream components: base models from HuggingFace, training datasets, Python packages, container images.
- **Transfer Learning Attacks:** Exploiting a pre-trained base model whose weights already contain a backdoor placed by the original attacker.
- **Model Skewing:** Feeding biased feedback into a system that retrains on user input, gradually shifting the model's behavior.
- **Output Integrity Attacks:** Tampering with model outputs in transit or storage so the receiver acts on false results.
- **Membership Inference:** Determining whether a specific record was in the training set. Privacy violation.
- **Insecure Output Handling:** Downstream systems trust and execute model output without validation. Leads to XSS, SQLi, RCE if the model outputs code or markup.
- **Model Denial of Service (DoS):** Sending expensive queries (huge context, recursive prompts) to exhaust compute and drive up cost.
- **Sensitive Information Disclosure:** Model leaks training data, system prompts, or context from other users through its responses.
- **Insecure Plug-in Design:** Model plug-ins with weak auth, no input validation, or excessive scope. Common LLM app vulnerability.
- **Excessive Agency:** Giving an AI agent more permissions or autonomy than needed, so a compromise or hallucination causes real damage (deleted files, sent emails, transferred funds).
- **Overreliance:** Users trust model output without verification. Leads to bad decisions, propagated hallucinations, and skill atrophy.
#### Compensating Controls
 
- **Prompt Firewalls:** Detect and block malicious prompts before they reach the model.
- **Model Guardrails:** In-model filters and refusal training to prevent unsafe output.
- **Access Controls:** RBAC, ABAC, MFA on model, data, and agent endpoints.
- **Data Integrity Controls:** Hashing, signing, and verifying training data and model artifacts to detect tampering.
- **Encryption:** Protects data in transit, at rest, and in use from interception and theft.
- **Prompt Templates:** Fixed structures with validated variables reduce injection surface.
- **Rate Limiting:** Blunts DoS, extraction, and brute-force jailbreak attempts.
- **Least Privilege:** Agents, users, and services get the minimum access needed. Limits blast radius of any compromise.
