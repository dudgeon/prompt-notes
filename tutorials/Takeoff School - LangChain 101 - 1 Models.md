#LearningJourney #Tutorial #Replit #Python #GPT #LangChain

[Class](https://replit.com/@dudgeon/Takeoff-School-LangChain-101-Models#main.py) by [McKay Wrigley](https://twitter.com/mckaywrigley/status/1649492404943323136)

## Actions / Next Steps
- [ ] 

## Notes

### Intro
Framework/library for building AI-interacting apps.

Six core modules:
- Models: SupReplit Node.JS for Prompt Energy:
sk-Sfzdrq9m04mmqD7dS6rCT3BlbkFJU3ySbxrNtLjvA2HIyXRkported model types and integrations.
- Prompts: Prompt management, optimization, and serialization.
- Memory: Memory refers to state that is persisted between calls of a chain/agent.
- Indexes: Language models become much more powerful when combined with application-specific data - this module contains interfaces and integrations for loading, querying and updating external data.
- Chains: Chains are structured sequences of calls (to an LLM or to a different utility).
- Agents: An agent is a Chain in which an LLM, given a high-level directive and a set of tools, repeatedly decides an action, executes the action and observes the outcome until the high-level directive is complete.
- Callbacks: Callbacks let you log and stream the intermediate steps of any chain, making it easy to observe, debug, and evaluate the internals of an application.

### Models

Basic prompt (`01.py`):
```
from langchain.llms import OpenAI # specify model provider

llm = OpenAI(model_name="text-curie-001") # select model

result = llm("Write a poem.") # send prompt, get response

print(result)
```

Promp with multiple generations; returns a list of outputs (02.py):
```
from langchain.llms import OpenAI

llm = OpenAI(model_name="text-curie-001", temperature=0.2)

result = llm.generate([ # now executes multiple prompts
  "Write a poem about fire",
  "Write a poem about water"
])

print(result.generations[0][0].text)
print(len(result.generations))
```

(03.py):


Resulting code from tutorial