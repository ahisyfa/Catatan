# The Evolution of LLM Applications
```
 ┌────────────────┐     ┌──────────┐    ┌──────────┐  
 │    Promt       ├────►│  Chains  ├───►│ AI Agent │  
 │  Engineering   │     └──────────┘    └──────────┘  
 └────────────────┘                                                                  
                                                      
```

## Prompt Engineering
Prompt Engineering is a process of crafting prompts to guide LLM outputs for a specific task, usually with a singular input.
- Simple prompts  
   - are straightforward requests for single tasks. 
   - This could be something like, summarize this article.
- Complex prompts 
   - add layers of detail and structure with multiple criteria and constraints. 
   - For example, summarize this article focusing on its impact on global markets highlighting geopolitical risks in no more than 200 words.

*) There are many Prompt Engineering techniques out there, and one such technique is Chain of Thought Prompting.

## Chains of Thought Prompting
Prompt engineering technique that induces step-by-step reasoning from the model   
It is known to :
   - improve accuracy on complex problems. 
   - You've probably seen examples of prompts that end with a phrase like, ***"let's solve this step-by-step."***
   - Note: this technique is now baked into modern LLMs with thinking mode or extended thinking.

## Chain / Prompt Chaining
- A fix sequence of LLM invocations and operations
- Output from one step become input to the next step 
- Can include data processing and formatting
- Usefull for predictable, structured tasks
- Example : A RAG (Retrieval Augmented Generation Chain)

```
                                                                                    
                  ┌─────────┐      ┌────────┐     ┌─────────────────┐               
 User Query──────►│Retrieve ├─────►│Format  ├────►│Generate Response├───────►Answer 
                  │Documents│      │Context │     │(LLM Call)       │               
                  └─────────┘      └────────┘     └─────────────────┘               
```


## What Make AI Agent Different?  
- Dynamic decision making
   - LLM controls the workflow execution and decides what to do next based on the current state
- Cycle and loops
   - Can revisit tasks and retry actions to refine results, 
   - Continue until completion criteria is met
- Tool Use and Actions
   - actively interact with external systems for both read and write operations.
- Refelection and Improvement
   - Can evaluate their own outputs and self-correct when needed.


## Comparing the Approches

|Feature          |  Prompt Engineering   |    Chain     |  AI Agent     |
|:----------------|:----------------------|:-------------|:--------------|                     
|Interaction      | Single                | Sequential   | Dynamic       |
|Decision Making  | Predefined            | Predefined   | LLM-Driven    |
|Tool Use         | No                    | Limited      | Extensive     |
|Iteration        | No                    | No           | Adaptive loops|
|Complexity       | Low                   | Medium       | High          |




## Quiz
1. What key capability distinguishes chain-of-thought prompting within prompt engineering from prompt chaining?

2. Chain-of-thought prompting is best described as:
