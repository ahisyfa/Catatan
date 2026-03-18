# AI Agents
Build the skills you’ll need to create autonomous systems, from designing basic agentic workflows to deploying advanced multi-agent architectures for production.


## Level 1 - Exploring
AI Agents and their Core Components
Define an AI agent and identify its core components (e.g., reasoning engine, tools, memory).
```
 ┌───────────────────────────────────────┐
 │      Characteristics of AI Agents     │
 │                                       │
 │ ┌───────────────┐     ┌─────────────┐ │
 │ │Autonomous     │     │Adaptive     │ │
 │ └───────────────┘     └─────────────┘ │
 │ ┌───────────────┐     ┌─────────────┐ │
 │ │Goal Directed  │     │Interactive  │ │
 │ └───────────────┘     └─────────────┘ │
 └───────────────────────────────────────┘
                                          
                                          
      ┌───────────────────────────────┐   
      │ Core Component of an AI Agent │   
      │                               │   
      │    ┌──────────────────────┐   │   
      │    │Reasoning Engine (LLM)│   │   
      │    └──────────────────────┘   │   
      │          ┌─────────┐          │   
      │          │  Tools  │          │   
      │          └─────────┘          │   
      │          ┌─────────┐          │   
      │          │ Memory  │          │   
      │          └─────────┘          │   
      └───────────────────────────────┘   
```

### Characteristics of AI Agents
What Are AI Agent?
AI agent are software system that powered by Large Language Model (LLM) that **can plan, take action, and use feedback to execute goals**, over multiple iterations.
They different from taditional software by their ability to make decisions dynamically and adapt their behaviour based on context.

4 Characterictic of AI Agents
1. Autonomous : They can operate independently without constant human direction.
2. Goal Directed : They can work towards achieving specific objectives rather than just responding to individual commands
3. Adaptive : They can change their approach based on what they learn from their environment.
4. Interactive : They can engage in external systems, tools, and users to accomplish their tasks.

### Core Component of an AI Agent
1. **Reasoning Engine (LLM)**
The brain that make decisions based on context, input and prior knowledge. Example: GPT-5, Cloud Sonic 4.5, Gemini 3 Pro.

2. **Tools**
External functions or services that an AI Agent can call to perform tasks. Tools can also invoke other large language models or even other agents. This is how you start building more and more sophisticated systems.

3. **Memory**
Ability to retain knowledge of past interactions and outputs for informed decision-making. 
Memory comes in two flavors. 
   - Short-term memory, which covers things like current conversation context, working state of the system.
   - Long-term memory, which includes learned patterns and episodic knowledge that persists across sessions.    

Without memory, every conversation is like talking to someone with amnesia. 

### How Component Work Together
**Reasoning Engine (LLM)** analyzes the situation and decides what to do next

**Tools** The tools extend the agent's capabilities by actually performing the actions

**Memory** provides context from previous interactions to inform current decisions

### Agent Architecture
```                                                                                                                              
                                                                                         
                                 AI Agent System                                         
                                                                                         
                                                                                         
                                                                                         
                                                                                         
                   ┌────────────────────┐       Retrieval        ┌─────────────┐         
                   │                    │◄───────────────────────┤             │         
                   │  Reasoning Engine  │                        │   Memory    │         
                   │      (LLM)         │       Update           │             │         
                   │                    ┼───────────────────────►└─────────────┘         
                   └───────▲───────┬────┘                                                
                           │       │                                                     
                           │       │                                                     
                           │       │ Invocation                                          
                           │       │                                                     
                           │       │                                                     
                    Result │       │                                                     
                           │       │       ┌──────────────┐                              
                           │       └──────►│              │                              
                           │               │    Tools     │                              
                           │               │              │                              
                           └───────────────┤              │                              
                                           └──────────────┘                              
                                                                                         
```
### Example of Agentic Behaviour
1. **Routing** 
where the agent decides between different application paths based on the user's request. Should a particular request go to customer support or sales or HR, the agent will figure this out. 

2. **Tool** selection
where multiple tools are available. The agent can choose which ones to call. This means making decisions like, do I need to source the web or should I query the database? 

3. **Quality assessment** 
where the agent evaluates whether its generated answer can actually meet the requirements. Is this good enough or should I try again?

4. **Iterative refinement** 
where the agent works in a loop until a task is completed successfully. This means that the agent can try different approaches if the first one doesn't quite work out. What's interesting is that you have already used certain agentic systems without perhaps not realizing it. Let's look at some familiar examples.

### Agentic Systems You May Have Used
Agent:
- ChatGPT
- Claude
- Perplexity AI
- Github CoPilot
- Cursor


### Common Pitfal: Is this an Agent?
There's a tendency in the industry to label any LLM application as an agent.

Someone wraps an API call with a good prompt, and they start calling it an agent. 
But the truth is that it's not actually an agent. That's just a simple LLM call. 
A true agent requires autonomy, decision-making, tool use, as well as some sort of iterative loop. If your system just takes input, calls an LLM once, and returns the output back to the caller, that's not really an agent.

## Level 2 - Applying

## Level 3 - Building

## Level 4 - Advancing