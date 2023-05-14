#LearningJourney #Tutorial #Replit #Python #GPT

[Class](https://replit.com/@dudgeon/Takeoff-School-Your-1st-AI-App) by [McKay Wrigley](https://twitter.com/mckaywrigley/status/1649492404943323136)

## Actions / Next Steps
- [ ] Replit's [100 Days of Code: The complete python course](https://replit.com/learn/100-days-of-python)

## Notes

Links
- Repo
- [Replit Project](https://replit.com/@dudgeon/Takeoff-School-Your-1st-AI-App#main.py)

Resulting code from tutorial

```
import os # imports OS module; used to access secret env variable
import openai

openai.api_key = os.getenv("OPENAI_API_KEY") # imports api key from env variable

while True: # loop for repeated questions

  # get the user question
  question = input("\033[34mWhat is your question?\n\033[0m") # \033[34m...\n\033[0m styles the text; The \033[34m at the start sets the text to green, and the \033[0m at the end resets it back to white.

  # exit handler
  if question.lower() == "exit":
    print("\033[31mGoodbye!\n\033[0m")
    break

  # create 'completion' request response from openai, make API call
  completion = openai.ChatCompletion.create(
    model="gpt-3.5-turbo",
    messages=[
      {"role": "system", "content": "You are a helpful assistant. Answer the given question."},
      {"role": "user", "content": question}
    ]
  )
  
  # print response
  print("\033[32m" + completion.choices[0].message.content + "\n") # response is prepended with styling to make text green
```

