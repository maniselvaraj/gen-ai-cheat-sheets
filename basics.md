

#

# LLM Basics

## Controlling Randomness and Diversity

Three Key Parameters​

1. Temperature​
   1. Controls probability distribution of word selection​
   2. Low (→0): Selects high-probability words → deterministic responses​
   3. High: Allows lower-probability words → creative/random responses​
2. Top K​
   1. Limits selection to K most probable next words​
   2. Example: K=50 means choose from top 50 candidate words​
   3. Prevents selection of highly unusual words
3. Top P​
   1. Caps word choices based on cumulative probability threshold​
   2. P<1.0 focuses on most probable options, ignoring unlikely ones​
   3. Alternative to Top K that uses probability sum instead of word count​
4. Example: "I hear the hoof beats of..."​
   1. High temp + no limits: May get "unicorns" (creative but unusual)​
   2. Temp = 0: Likely gets "horses" (most probable)​
   3. High temp + Top K/P limits: Gets "horses" or "zebras" (balanced creativity)


---

## Prompt Engineering Tips


* **Start Simple, Iterate:** Begin with a broad request, then refine it.
    * *Example:* "Summarize text" $\rightarrow$ "Summarize text in 3 bullet points."

* **Use Clear Action Verbs:** Tell the model precisely what to do.
    * *Example:* "Write a product description."

* **Place Instructions First:** Put your main command at the beginning of the prompt.
    * *Example:* "### Instruction ### Translate to Spanish: Text: Hello."

* **Use Separators:** Clearly delineate different parts of your prompt.
    * *Example:* "### Task ### Classify sentiment ### Text ### I love this."

* **Be Specific & Detailed:** Provide ample context and explicit requirements.
    * *Example:* "Write a formal email to a client apologizing for a 2-day shipping delay."

* **Include Example Outputs:** Show the model the desired format and style.
    * *Example:* "Extract names. Format: Name: John, Mary from text: John and Mary."

* **Keep Details Relevant:** Avoid unnecessary or distracting information.
    * *Example:* (Avoid) "Write a story about dogs, make it interesting and engaging."

* **Be Direct, Not Clever:** Prioritize clarity and straightforwardness.
    * *Example:* "Explain quantum physics to a 12-year-old in 2 sentences" (better than "Explain quantum physics simply").

* **State What To Do:** Use positive instructions instead of negative ones.
    * *Example:* "Recommend movies from trending list" vs. "Don't ask for personal preferences."

* **Experiment Extensively:** Try different phrasing and approaches.
    * *Example:* Try "List pros and cons" then "Create a comparison table."

* **Break Down Complex Tasks:** Divide a big problem into smaller, manageable steps.
    * *Example:* "Analyze market data" $\rightarrow$ "1. Identify trends 2. Calculate averages."

* **Balance Detail with Length:** Include necessary context without being overly verbose.
    * *Example:* Provide key context but avoid lengthy background information.

* **Use Proper Formatting:** Apply structured inputs and outputs like newlines.
    * *Example:* "Task: Classify\nInput: This movie was amazing\nOutput:"

* **Structure Prompts Clearly:** Define the model's role, the task, and the audience.
    * *Example:* "Role: Teacher\nTask: Explain photosynthesis\nAudience: 5th graders."

* **Define Output Audience/Persona:** Tailor the output to a specific type of recipient.
    * *Example:* "Write a product review for a tech-savvy gamer."

* **Specify Output Format:** Explicitly request formats like JSON, tables, or lists.
    * *Example:* "Extract entities into a JSON array."

* **Manage Ambiguity:** Instruct the model on how to handle unclear information.
    * *Example:* "If any part is unclear, state the ambiguity rather than making an assumption."

* **Use Chain-of-Thought:** Guide the model to show its step-by-step reasoning.
    * *Example:* "First, identify the premise. Second, analyze its validity. Finally, provide your assessment."

* **Assign Model Persona:** Instruct the model to adopt a specific character or tone.
    * *Example:* "You are a seasoned financial analyst. Explain the market trends."


For various prompting techniques like below, check https://www.promptingguide.ai/techniques


Here's the table with "When to Use" split into its own column:

| Prompting Technique | Definition | When to Use |
|---|---|---|
| **Zero-shot Prompting** | Directly ask the model to perform a task without examples. | When the task is simple and straightforward. |
| **Few-shot Prompting** | Provide a few examples of the task within the prompt. | To guide the model's desired output format or style. |
| **Chain-of-Thought Prompting** | Instruct the model to show its step-by-step reasoning. | For complex reasoning or multi-step problems. |
| **Meta Prompting** | Focuses on the structural and syntactical aspects of tasks rather than specific content details, using abstract frameworks and patterns to guide LLM responses in a more structured, token-efficient manner. | Use meta prompting for complex reasoning tasks, mathematical problem-solving, coding challenges, and theoretical queries where you want to emphasize structure and pattern over specific content examples while maintaining token efficiency. |
| **Self-Consistency** | Generate multiple outputs and take the majority vote or most consistent answer. | To improve reliability for reasoning tasks. |
| **Generate Knowledge Prompting** | Ask the model to generate relevant knowledge before answering a question. | When external knowledge is beneficial for the task. |
| **Prompt Chaining** | Link multiple prompts together, where one's output is another's input. | For complex workflows or sequential tasks. |
| **Tree of Thoughts** | Explore multiple reasoning paths and evaluate intermediate steps. | For highly complex problems requiring deeper exploration. |
| **Retrieval Augmented Generation** | Combine an LLM with an external knowledge retriever. | For factual accuracy and to access up-to-date information. |
| **Automatic Reasoning and Tool-use** | Enable the model to autonomously use external tools (e.g., search, calculator). | When tasks require capabilities beyond the LLM's inherent knowledge. |
| **Automatic Prompt Engineer** | Use an LLM or another algorithm to automatically generate and refine prompts. | For optimizing prompt performance. |
| **Active-Prompt** | An interactive approach where the model queries for missing information or clarifies ambiguities. | For tasks requiring precise input or iterative refinement. |
| **Directional Stimulus Prompting** | Provide specific keywords or phrases to steer the model's generation. | To guide the model towards a desired direction or topic. |
| **Program-Aided Language Models** | Guide the LLM to generate code (e.g., Python) to solve problems. | For tasks requiring precise calculation, logical operations, or structured output. |
| **ReAct** | Combine reasoning traces with actions (tool use) for problem-solving. | For complex tasks requiring both thought processes and external interaction. |
| **Reflexion** | Enable the model to reflect on its previous outputs and iteratively refine them. | For improving the quality of generated content through self-correction. |
| **Multimodal CoT** | Apply chain-of-thought reasoning to inputs involving multiple modalities (e.g., text and image). | For complex tasks that blend different types of input. |
| **Graph Prompting** | Use graph structures to represent knowledge or relationships in prompts. | For tasks requiring understanding or generation based on complex relationships. |

## Prompt + Parameters

| **Example use case**​ | **Temperature**​ | **top\_p**​ | **Description**​ |
| --- | --- | --- | --- |
| Brainstorming session​ | High​ | High​ | High randomness with large pool of potential tokens. The results will be highly diverse, often leading to very creative and unexpected results.​ |
| Email generation​ | Low​ | Low​ | Deterministic output with high probable predicted tokens. This results in predictable, focused, and conservative outputs.​ |
| Creative writing​ | High​ | Low​ | High randomness with a small pool of potential tokens. This combination produces creative outputs but still remains coherent.​ |
| Translation​ | Low​ | High​ | Deterministic output with high probable predicted tokens. Produces coherent output with a wider range of vocabulary, leading to outputs with linguistic variety. |


---

## Hallucination

An LLM hallucination occurs when a large language model (LLM) generates a​

response that is either​:

* factually incorrect,​
* Nonsensical​
* or disconnected from the input prompt.​

Hallucinations are a byproduct of the probabilistic nature of language models which generates responses based on patterns learned from vast datasets​ rather than factual understanding.

### Reducing Hallucination

1. Data Quality is King​

* Clean, Diverse, & Relevant Data: Train on high-quality, balanced, and domain-specific datasets.​
* Regular Updates: Keep training and grounding data current.​

2. Grounding with RAG​

* Retrieval-Augmented Generation (RAG): Anchor AI responses to external, authoritative knowledge bases.​
* Prepare Grounding Data: Organize and curate your enterprise data for accurate retrieval.​

3. Model & Prompt Engineering​

* Advanced Models: Leverage larger, more sophisticated models.​
* Self-Correction: Implement mechanisms for the AI to verify its own outputs.​
* Clear Prompts: Give explicit, contextual, and example-driven instructions.​
* Lower Temperature: Reduce model creativity for factual accuracy.​

4. Human Oversight & Testing​

* Fact-Checking: Validate AI outputs, especially for critical use cases.​
* Continuous Monitoring: Regularly test and refine models based on real-world performance.


**References**
1. <https://www.promptingguide.ai/>
2. <https://help.openai.com/en/articles/6654000-best-practices-for-prompt-engineering-with-the-openai-api/>

