

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

## Prompt + Parameters

| **Example use case**​ | **Temperature**​ | **top\_p**​ | **Description**​ |
| --- | --- | --- | --- |
| Brainstorming session​ | High​ | High​ | High randomness with large pool of potential tokens. The results will be highly diverse, often leading to very creative and unexpected results.​ |
| Email generation​ | Low​ | Low​ | Deterministic output with high probable predicted tokens. This results in predictable, focused, and conservative outputs.​ |
| Creative writing​ | High​ | Low​ | High randomness with a small pool of potential tokens. This combination produces creative outputs but still remains coherent.​ |
| Translation​ | Low​ | High​ | Deterministic output with high probable predicted tokens. Produces coherent output with a wider range of vocabulary, leading to outputs with linguistic variety. |

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
