# Basic Summarizer Prompt

Goal: create a summarizer prompt that meets the following goals:

* Summarizes text, regardless of input format (paragraph, bullets) into bullets.
* Retains all identifiable ideas/facts from input text.
* Uses vocabulary that is understandable by average readers, regardless of education level or domain expertise.
* Explains terms that may not be understood by a general audience.
* Has a clean output that does not require further parsing (i.e. does not prepend "sure! here is your summary!")
* Conceals internal thought processes

## Current prompt

```
I need your help summarizing text; there will be multiple steps; please review them all before responding.
First, in your own head, summarize the text surrounded by triple backticks into bullets, each no longer than 140 characters,
explaining the distinct, identifiable ideas and datapoints of the input text; think in a manner that is clear and understandable,
regardless of the reader’s educational background in plain language that can be easily understood by the average consumer;
do not share this initial summarization with the user. Once you have completed your initial summarization, please review it,
identify any terms that fail these goals, and the revise your answer to explain these terms; then check your work again;
then share your answer.
```

Example input:
```
The dominant sequence transduction models are based on complex recurrent or convolutional neural networks in an encoder-decoder configuration. The best performing models also connect the encoder and decoder through an attention mechanism. We propose a new simple network architecture, the Transformer, based solely on attention mechanisms, dispensing with recurrence and convolutions entirely. Experiments on two machine translation tasks show these models to be superior in quality while being more parallelizable and requiring significantly less time to train. Our model achieves 28.4 BLEU on the WMT 2014 English-to-German translation task, improving over the existing best results, including ensembles by over 2 BLEU. On the WMT 2014 English-to-French translation task, our model establishes a new single-model state-of-the-art BLEU score of 41.8 after training for 3.5 days on eight GPUs, a small fraction of the training costs of the best models from the literature. We show that the Transformer generalizes well to other tasks by applying it successfully to English constituency parsing both with large and limited training data.
```

Example Output (gpt-4):
```
- Current methods for translating sequences, like language, use complex, repeating, or feature-spotting networks.
- These models often link input and output stages via a tool called an attention mechanism.
- A simpler design, the Transformer, is suggested, using only attention mechanisms and skipping the repetitive and feature-spotting stages.
- In language translation tests, the Transformer was better, could handle more data at once, and was quicker to train.
- The Transformer scored 28.4 in an English-to-German translation test, improving previous best scores by over 2 points.
- It also scored 41.8 in an English-to-French translation test after 3.5 days of training on eight graphics cards, costing less than other models.
- The Transformer can be effectively used in other areas, like analyzing English sentence structure, with varying amounts of training data.
```

### Previous attempts

#### Initial

Prompt:

```
Please summarize the text surrounded by triple backticks into bullets, each no longer than 140 characters, explaining the distinct,
identifiable ideas and datapoints of the input text; write in a manner that is clear and understandable,
regardless of the reader’s educational background in plain language that can be easily understood by the average consumer.
```

Example input: Same as before, `{Abstract from "Attention is all you need"}`

Example output (`gpt-3.5-turbo`):

```
- The dominant models for sequence transduction use complex recurrent or convolutional neural networks in an encoder-decoder setup.
- The best models use an attention mechanism to connect the encoder and decoder.
- The proposed Transformer architecture is a simpler network based solely on attention mechanisms, eliminating recurrence and convolutions.
- The Transformer models outperform others in machine translation tasks, achieving higher quality, parallelizability, and faster training time.
- The Transformer model achieves a BLEU score of 28.4 on the WMT 2014 English-to-German translation task, surpassing existing results by 2 BLEU.
- For the WMT 2014 English-to-French translation task, the Transformer model sets a new state-of-the-art BLEU score of 41.8 after training for 3.5 days on eight GPUs, with significantly lower training costs.
- The Transformer architecture generalizes well to other tasks, such as English constituency parsing, even with limited training data.
```

Conclusion:
* Model + prompt produced inconsistent result
  - Distillation of text to bullets <= 140 characters: success
  - Preservation of distinct, identifiable ideas: success
  - `clear and understandable, regardless of the reader’s educational background in plain language that can be easily understood by the average consumer`: complete failure
* Clearly require additional instructions
* Task may exceed capabilities of `gpt-3.5-turbo`
