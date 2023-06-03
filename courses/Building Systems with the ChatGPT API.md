Andrew NG and Isa [Course on DeepLearning.ai](https://learn.deeplearning.ai/chatgpt-building-system/lesson/1/introduction)

## Language  Models, the Chat Format, and Tokens

### Text generation process
- Supervised learning:
	- Input / output mapping; e.g. food: "bagel", enjoy: true
	- Good building block for training large language models
		- Whole statement divided and turned into input/output, e.g. "my favorite food is a bagel" >> "my favorite food is a": "bagel"
		- Create massive training set via masking
- Two major typse of LLMs:
	- Base
		- Repeatedly predicts next word based on training data
		- May repeat/iterate vs answer questions
	- Instruction-tuned
		- Tried to follow instructions
	- Process to go base >> instruction tuned
		- First, train base model
		- Fine-tune on smaller set of examples where an output follows an input example (Q/A)
		- Obtain human ratings on, eg, helpful, honest, harmless; fine-tune on these outputs
- Refresher on basic completion process

```
def get_completion(prompt, model="gpt-3.5-turbo"):
    messages = [{"role": "user", "content": prompt}]
    response = openai.ChatCompletion.create(
        model=model,
        messages=messages,
        temperature=0,
    )
    return response.choices[0].message["content"]

response = get_completion("What is the capital of France?")
print(response)
>> Paris
```

Tokenization
- Prompts are understood at the token level, not as letters, e.g.
```
response = get_completion("Take the letters in lollipop \
and reverse them")
print(response)
>> polilol  # close but not quite
```

- Lollipop is not a common enough word to fit within a token, and tokenizes to approximately l-oll-ipop
- A token is ~0.75 words
- You can address by feeding in the letters one at a time
- Given windows have given token context windows (limits for input + output)

### System, User, Assistant messages

- Messages completion format, used in chat contexts:
```
def get_completion_from_messages(messages, 
                                 model="gpt-3.5-turbo", 
                                 temperature=0, 
                                 max_tokens=500):
    response = openai.ChatCompletion.create(
        model=model,
        messages=messages,
        temperature=temperature, # this is the degree of randomness of the model's output
        max_tokens=max_tokens, # the maximum number of tokens the model can ouptut 
    )
    return response.choices[0].message["content"]

# e.g.
messages =  [  
{'role':'system', 
 'content':"""You are an assistant who responds in the style of Dr Seuss."""},    
{'role':'user', 'content':"""write me a very short poem about a happy carrot"""},  
] 
response = get_completion_from_messages(messages, temperature=1)
print(response)
```

- Basics
	- `System`: sets tone/behavior of assistant
	- `Assistant`: LLM response
	- `User`: prompts
- Array of messages lets you remind (on subsequent prompts) the model of previous interactions, to be 'considered' in next response
- 