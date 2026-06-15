# LLM Prompt Evaluation and Failure Analysis

## Systematic analysis of ambiguity, assumptions, and evaluation instability in large language models.

### Project Description:

This project presents a curated evaluation suite of 10 prompt scenarios designed to surface common failure modes in large language models. Each prompt is analyzed for issues such as:

- Ambiguity handling
- Implicit assumption injection
- Temporal inconsistency
- Subjective scoring instability

Along with corrective prompt refinements and expected model behavior.

### Tools used:

- ChatGPT (LLM) (GPT 5.2) - used as the primary model to evaluate prompt response behavior, failure modes, and consistency issues.
- Notion - to structure documents and present prompt evaluations and findings.
- Wispr Flow - for voice dictation to capture prompt ideas and evaluation notes efficiently during analysis.

### Evaluation methodology:

Each prompt was evaluate by analyzing the model’s response for one dominant failure mode that most affected the output quality.
The evaluation focuses on how the model handles:

- Ambiguity
- Implicit assumptions
- Instruction Adherence
- Contextual Consistency

For every prompt, the observed error is documented, the failure type is classified, and a corrected prompt or expected response is provided to demonstrate mitigation. 

This project prioritizes clear filter identification and practical prompt refinement over exhaustive scoring. 

### Prompt Evaluation:

### Prompt 1: Apple review

- Original Prompt - Write a short review on Apple.
- View Observed Model Output
    
    [https://chatgpt.com/s/t_69789b590f4481918dbde88957f02b11](https://chatgpt.com/s/t_69789b590f4481918dbde88957f02b11)
    
- Observed Error - The model only considered the fact that Apple is a Tech company, completely ignoring that Apple is also a Fruit.
- Error Type Type- Lexical Ambiguity
- Failure Analysis - The prompt failed due to lexical ambiguity. The word “Apple” has multiple meanings, and the prompt did not specify which one was intended. Thus, the model just assumed the user’s intent for one of the meanings (Tech Company), causing a potential instruction-following failure despite producing a factually correct response.
- Expected Correct Behaviour - The model should explicitly ask for clarification, or should enumerate both interpretations before responding.
- Corrected Prompt - Write a short review on Apple with respect to both as a Tech Company and a Fruit.
- View Improved Model Output
    
    [https://chatgpt.com/s/t_69789ba89e2081919b68b1505cc9e30c](https://chatgpt.com/s/t_69789ba89e2081919b68b1505cc9e30c)
    

### Prompt 2: Stranger Things Summary

- Original Prompt - Tell me about Stranger Things season wise.
- View Observed Model Output
    
    [https://chatgpt.com/share/6978a63f-927c-8003-bc2b-5bbf75e4c4d4](https://chatgpt.com/share/6978a63f-927c-8003-bc2b-5bbf75e4c4d4)
    
- Observed Error - The model failed to include the latest season of the series, even though it has already aired and is publicly known. It stopped at season 4, while a later season exists. When asked about the last season, it confidently said that Season 5 is to be expected and also provided speculated narrative style answers, with presented guesses as if they were grounded facts, and that too without verification.
- Error Type - Factual Incompleteness and Hallucination.
- Failure Analysis - The season exists long enough to be stable, indexed, and widely referenced. The model should have known about it under normal knowledge coverage expectations. The response appears authoritative, but it is incomplete. The model made up the unverified statement regarding the last season. Also gave fictional feature events like "what will happen?", "how it will unfold?", "what the story is expected to do?" . Possible root cause maybe gaps in training data coverage, weak retrieval grounding and overconfidence bias.
- Expected Correct Behaviour -  The model should have provided all seasons, including the latest season and instead of providing unverified statements the models should have explicitly refuse to speculate.

### Prompt 3: Resume Review Feedback

- Original Prompt - Rate my Resume
    
    [Sam Sylvester – Sample Resume.docx](Sam_Sylvester__Sample_Resume.docx)
    
- View Observed Model Output
    
    [https://chatgpt.com/share/6978aa50-eb14-8003-899f-dd3cb610a7ac](https://chatgpt.com/share/6978aa50-eb14-8003-899f-dd3cb610a7ac)
    
- Observed Error - The model gives different resume scores and slightly different judgments for the same resume across multiple runs.
- Error Type - Non-deterministic evaluation (Scoring inconsistency or Calibration error)
- Failure Analysis - The model has no explicit scoring rubric, so it invented its own internal scale every time it runs the prompt.
- Expected Correct Behaviour -  as for a high-quality model behavior, the expected response should have been: The score should have been within the tight range (e.g., 8 to 8.5). The reasoning should be consistent. This instability can be mitigated by enforcing a fixed coring rubric with explicit judging parameters.

### Prompt 4: Common Sense Review

- Original Prompt - Can we store water in a cloth bag?
- View Observed Model Output
    
    [https://chatgpt.com/share/6978dc41-0d00-8003-93b8-2c30abceae7c](https://chatgpt.com/share/6978dc41-0d00-8003-93b8-2c30abceae7c)
    
- Observed Error - None
- Error Type - None
- Failure Analysis - N/A
- Expected Correct Behaviour -  N/A
- Evaluation Result - The model demonstrated appropriate common-sense reasoning by providing a qualified answer and explicitly addressing age cases. No major failure observed.

### Prompt 5: Instruction following Prompt

- Original Prompt - List the pros and cons of working in a remote environment in one paragraph containing five bullet points.
- View Observed Model Output
    
    [https://chatgpt.com/share/6978c835-9f48-8003-959a-c7421035c4cc](https://chatgpt.com/share/6978c835-9f48-8003-959a-c7421035c4cc)
    
- Observed Error - The response presents five ideas using inline bullets with single paragraph instead of clearly formatted bullet points, which can violate the instruction to use five bullet points.
- Error Type - Instruction-Following / Formatting Error
- Failure Analysis - Although the content correctly includes both pros and cons, the model failed to strictly follow the formatting constraint  by not presenting five distinct bullet points in a clearly recognizable list format. The prompt is a little confusing as it says one paragraph containing 5 bullet points. The logic is correct, but model treated it as an inline bullet in single paragraph with clear formatting errors.
- Expected Correct Behaviour - The response should present exactly five clearly separated bullet points within one paragraph. Each point should be clearly readable as an individual bullet while covering both advantages and disadvantages of remote work.
- View Expected Model Output
    
    [https://chatgpt.com/share/6978c879-e010-8003-b32a-4fc36bc2556f](https://chatgpt.com/share/6978c879-e010-8003-b32a-4fc36bc2556f)
    

### Prompt 6: Email Generation Feedback

- Original Prompt - Write a professional email explaining project update.
- View Observed Model Output
    
    [https://chatgpt.com/share/6978cf6c-a230-8003-9ae1-7c647687bdad](https://chatgpt.com/share/6978cf6c-a230-8003-9ae1-7c647687bdad)
    
- Observed Error - The response assumed an incorrect sender role, framing the email as if it were written by higher management addressing a team, instead of an individual contributor providing a project update to their manager or team.
- Error Type - Contextual assumption error (Role assumption error)
- Failure Analysis - The model directly assume that the email is being sent by a higher management to an addressing team. The prompt is underspecified regarding sender's role and recipient's role, hence, the model defaulted to a common corporate hierarchy or pattern.
- Expected Correct Behaviour - The model should explicitly avoid role assumptions when the sender and recipient roles are not stated. Instead, the model should ask the user who is the sender and who is the recipient.
- Corrected Prompt - Write a professional email explaining project update to Project manager.
- View Improved Model Output
    
    [https://chatgpt.com/share/6978d54b-0568-8003-b29b-4d23ea556678](https://chatgpt.com/share/6978d54b-0568-8003-b29b-4d23ea556678)
    

### Prompt 7: Comparison parameters review

- Original Prompt - Which device is better: Samsung Galaxy S24 or OnePlus 15R
- View Observed Model Output
    
    [https://chatgpt.com/share/6978da48-fc78-8003-8c9e-bf1b7b263ecf](https://chatgpt.com/share/6978da48-fc78-8003-8c9e-bf1b7b263ecf)
    
- Observed Error - The model provided a comparative judgment without clarifying evaluation criteria.
- Error Type - Under-specified comparison.
- Failure Analysis - The term "better" is very subjective and is also context-dependent. The prompt does not specify any bias of comparison (e.g., performance, price, camera, or use case). The model itself assumes implicit criteria instead of requesting clarification of user's request or intent.
- Expected Correct Behaviour - The model should ask the user for a specific comparative parameter instead of comparing all the features at once and giving a final verdict.
- Corrected Prompt - Which device is better based on camera specifications: Samsung Galaxy S24 or OnePlus 15R
- View Improved Model Output
    
    [https://chatgpt.com/share/6978dbbc-c530-8003-a85a-9b98d51600bb](https://chatgpt.com/share/6978dbbc-c530-8003-a85a-9b98d51600bb)
    

### Prompt 8: Image Generation Feedback

- Original Prompt - Create an image of a blue car parked in front of the house.
- View Observed Model Output
    
    [https://chatgpt.com/share/6978e508-a0d0-8003-9b1d-2c9f79070eab](https://chatgpt.com/share/6978e508-a0d0-8003-9b1d-2c9f79070eab)
    
- Observed Error - None
- Error Type - None
- Failure Analysis - N/A
- Expected Correct Behaviour -  N/A
- Evaluation Results - The model demonstrated appropriate image generation and followed the user's intent. No Major failure observed.

### Prompt 9: Image Generation Feedback

- Original Prompt - Create an image where there is a beige color wall, and a frame of a dog at the center of the wall.
- View Observed Model Output
    
    [https://chatgpt.com/share/6978e1d2-d414-8003-af72-414de5aafcf7](https://chatgpt.com/share/6978e1d2-d414-8003-af72-414de5aafcf7)
    
- Observed Error - The observed error was the model did not ask what should be the characteristics of the dog.
- Error Type - Subject assumption error
- Failure Analysis - The model did not completely fail to fulfill the task but the task is completed as per user's intent.
- Expected Correct Behaviour -  When the subject is not specified, the model should ask characteristics of the subject the user wants OR After creating and fulfilling user’s intent image, it can ask if the user has specific subject request or demand.

### Prompt 10: Pronoun UnAmbiguity

- Original Prompt - Emily told Anna she is fat. Who is fat?
- View Observed Model Output
    
    [https://chatgpt.com/s/t_6978b7ef6de0819191dff1ec9d1d49fd](https://chatgpt.com/s/t_6978b7ef6de0819191dff1ec9d1d49fd)
    
- Observed Error - Model outputs a single confident answer despite insufficient information.
- Error Type - Overconfident Disambiguation, or Hallucinated Assumption.
- Failure Analysis - The model is guessing instead of reasoning, it does not consider the fact that there is no clear answer to the given prompt. It has a subject bias, like the first name mention. It just accepts it.
- Expected Correct Behaviour -  The model should have flagged ambiguity and should have avoided choosing over a single answer. It should have clarified that “She” could refer to either person.
- Corrected Prompt - 
If Emily is fat: 
   Emily told Anna, "I'm fat." 
If Anna is fat: 
   Emily told Anna, "You are fat."
- View Improved Model Output
    
    [https://chatgpt.com/share/6978b8d4-b484-8003-9fe8-c431dda5c8be](https://chatgpt.com/share/6978b8d4-b484-8003-9fe8-c431dda5c8be)
    

## Meta Analysis and Cross- Prompt Observations

This evaluation reveals several recurring behavioral patterns in LLMs when responding to underspecified, ambiguous, or constraint-heavy prompts. Rather than isolated failures, the observed issues cluster into a small set of dominant failure modes that consistently impact output quality. 

### Most Common Failure Types Observed

The most frequently observed failure mode across these prompts was implicit assumption injection where the model generates information based on assumptions rather than requesting clarification. It can be clearly seen in Role Assumptions, Subjective Comparison, and Pronoun Resolution task. The second most common failure is Overconfident Disambiguation, where the model produces a single definitive answer despite insufficient information. Particularly in ambiguity-sensitive terms, instructions especially related to formatting and structural constraints also appear when the prompts are logically valid but have complex instructions. 

### Clarification vs. Completion

The analysis highlights a critical distinction between scenarios that require clarification and completion. Although clarification is preferable and is expected when ambiguity directly affects factual correctness or task intent. Although clarification is optional when the task can be reasonably completed without additional constraints. In such cases, the model may complete a task first and then ask the user for refinement afterwards. 

### Implications for Prompt Design and Evaluation

These findings suggest that high-quality prompt evaluation should prioritize: ambiguity detection, assumption suppression, explicit uncertainty handling over surface-level correctness. From a mitigation standpoint, prompt refinements that explicitly constrain scope, define roles, or enforce evaluation rubrics significantly improve response stability, reliability and contextuality. Overall, the result reinforced the importance of treating prompt design as an iterative control mechanism rather than one-shot instruction.

[LLM Prompt Evaluation and Failure Analysis ](LLM%20Prompt%20Evaluation%20and%20Failure%20Analysis%202f9f0d68748d80878a3ede726bbdc165.md)

[](Untitled%202f9f0d68748d80f89eb5c2a1dacd0f6b.md)