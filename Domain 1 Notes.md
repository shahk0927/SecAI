## Domain 1.0: Basic AI Concepts Related to Cybersecurity
 
### 1.1 Compare and contrast various AI types and techniques used in cybersecurity
 
#### Types of AI
 
- **Generative AI (GenAI):** AI that produces new content (text, images, code, audio) rather than only classifying or predicting. Built on models like LLMs and diffusion models.
- **Machine Learning (ML):** Systems that learn patterns from data instead of being explicitly programmed. Umbrella term covering supervised, unsupervised, and reinforcement learning.
- **Statistical Learning:** ML approach grounded in statistical theory (regression, Bayesian methods, hypothesis testing). Focuses on inference and quantifying uncertainty, not just prediction.
- **Transformers:** Neural network architecture using self-attention to process sequences in parallel. Foundation of modern LLMs like GPT and Claude.
- **Deep Learning:** ML using multi-layer neural networks that automatically learn hierarchical features from raw data. Powers image recognition, NLP, and speech.
- **Natural Language Processing (NLP):** Field enabling machines to read, interpret, and generate human language.
  * **Large Language Models (LLMs):** Massive transformer models trained on huge text corpora (billions of parameters) for broad language tasks.
  * **Small Language Models (SLMs):** Smaller, more efficient models tuned for narrow tasks or edge/on-device use. Lower cost, lower latency, easier to secure.
  * **Generative Adversarial Networks (GANs):** Two networks (generator + discriminator) trained against each other. The generator creates fake data, the discriminator tries to detect it. Used for deepfakes and synthetic data.
#### Model Training Techniques
 
- **Model Validation:** Testing a model against data it did not train on to check accuracy and generalization. Prevents overfitting.
- **Supervised Learning:** Training on labeled data (input + known correct output). Used for classification and regression.
- **Unsupervised Learning:** Training on unlabeled data to find patterns or clusters. Used for anomaly detection and grouping.
- **Reinforcement Learning:** Agent learns by taking actions in an environment and receiving rewards or penalties. Used in game-playing, robotics, RLHF for LLMs.
- **Fine-tuning:** Taking a pre-trained model and further training it on a smaller, domain-specific dataset to specialize its behavior.
  * **Epoch:** One full pass of the training dataset through the model during training. More epochs = more learning, but risk of overfitting.
  * **Pruning:** Removing unnecessary weights or neurons from a trained model to shrink size and speed inference without major accuracy loss.
  * **Quantization:** Reducing the numerical precision of model weights (e.g., 32-bit float to 8-bit int) to cut memory and compute cost.
#### Prompt Engineering
 
- **System Prompts:** Instructions given to the model by the developer/operator that define its role, constraints, and behavior. User cannot normally see or change these.
- **User Prompts:** The actual input or question submitted by the end user during the conversation.
- **One-shot Prompting:** Giving the model exactly one example of the desired input/output before the real task.
- **Multi-shot Prompting (Few-shot):** Providing multiple examples in the prompt to guide the model's response format and reasoning.
- **Zero-shot Prompting:** Asking the model to perform a task with no examples, relying only on its pre-trained knowledge.
- **System Roles:** Persona or function assigned to the AI (e.g., "You are a security analyst"). Shapes tone and scope of responses.
- **Templates:** Pre-built prompt structures with placeholders for variable input. Ensures consistency, reduces injection risk, and standardizes output.
### 1.2 Explain the importance of data security in relation to AI
 
#### Data Processing
 
- **Data Cleansing:** Removing errors, duplicates, and inconsistencies from training data. Bad data = bad model.
- **Data Verification:** Confirming that data is correct, complete, and matches its intended source before use.
- **Data Lineage:** Tracking data's journey from origin through every transformation to final use. Critical for audits and troubleshooting bias.
- **Data Integrity:** Ensuring data remains accurate and unaltered from collection through processing and storage.
- **Data Provenance:** Documented history of where data came from, who owned it, and how it was collected. Answers "can we trust this source?"
- **Data Augmentation:** Artificially expanding training data by transforming existing samples (rotating images, paraphrasing text). Improves model robustness.
- **Data Balancing:** Adjusting class distribution in a dataset so the model does not favor over-represented classes. Reduces bias.
#### Data Types
 
- **Structured Data:** Organized in rows/columns with a defined schema (SQL tables, spreadsheets). Easy to query and validate.
- **Semi-structured Data:** Has some organizational tags but no rigid schema (JSON, XML, logs). Flexible but harder to enforce integrity.
- **Unstructured Data:** No predefined format (free text, images, audio, video). Bulk of enterprise data and hardest to secure.
- **Watermarking:** Embedding a hidden or visible marker in AI-generated content or training data. Used to prove ownership, detect AI-generated media, or trace leaks.
#### Retrieval-Augmented Generation (RAG)
 
- **RAG:** Architecture where the model retrieves relevant external documents at query time and uses them as context. Reduces hallucination and lets the model use fresh or private data without retraining.
  * **Vector Storage:** Database that stores numerical representations (vectors) of documents for fast similarity search. Examples: Pinecone, Chroma, Weaviate, pgvector.
  * **Embeddings:** Numerical vector representations of text/images/audio that capture semantic meaning. Similar content = similar vectors.
### 1.3 Explain the importance of security throughout the life cycle of AI
 
- **Business Use Case:** Clearly defined problem the AI is meant to solve before any development starts. Avoids AI-for-AI's-sake projects.
  * **Alignment with Corporate Objectives:** The use case must map to actual business goals (revenue, risk reduction, efficiency). Ungrounded projects fail governance review.
- **Data Collection:** Gathering the data used to train and evaluate the model.
  * **Trustworthiness:** Data sources must be reliable and free of tampering. Untrusted data poisons the model.
  * **Authenticity:** Confirming the data actually came from who and where it claims to. Prevents ingestion of fabricated or spoofed data.
- **Data Preparation:** Cleansing, labeling, transforming, and splitting data into train/validation/test sets. Where most ML project time is spent.
- **Model Development/Selection:** Choosing the algorithm/architecture and training the model, or picking a pre-trained model to fine-tune.
- **Model Evaluation:** Measuring performance against validation and test sets. Metrics like accuracy, precision, recall, F1, and fairness scores.
- **Deployment:** Moving the model into production infrastructure with proper access controls, logging, and rollback capability.
- **Validation:** Confirming the deployed model behaves as expected in the live environment, including under adversarial input.
- **Monitoring and Maintenance:** Continuous tracking of accuracy, drift, cost, and security events after deployment. Models degrade as data drifts.
- **Feedback and Iteration:** Using real-world performance data and user feedback to retrain and improve the model over time.
#### Human-centric AI Design Principles
 
- **Human-in-the-loop (HITL):** A human reviews or approves AI decisions before they take effect. Used for high-risk actions (medical, financial, security response).
- **Human Oversight:** Humans retain the ability to monitor, override, and shut down AI systems. Required by most AI governance frameworks including EU AI Act.
- **Human Validation:** Humans verify model outputs against ground truth before those outputs are trusted or acted on. Catches hallucinations and bias.
 
