# gremlin-gpt
A dataset of questions and statements in natural language, and their translation to Gremlin


## Purpose
We want to create a set of datasets that can be used for training a natural language model to translate English sentences into Gremlin statements.
We are targeting to use this to fine-tune a GPT-3 model from [OpenAI](https://openai.com/blog/openai-api/)


## Organisation
The training data is written as a JSONL file, with one line per question, with the following fields:

```
{"data": 
  {"text_list": ["Question in plain English, ending with a question mark?", "g.V().gremlinquery(<parameter>); parameter='value'; <end>"]
  }
}
```
Identation is shown here to make it easy to display, but on the actual dataset a line feed will signify a new question only. That means, no \n character, please.

Example:
```
{"data": {"text_list": ["What is the full name of Alice?", "g.V().hasLabel(<object_1>).has(<identifier_1>, <value_1>).values(<result_1>); object_1='person'; identifier_1='name'; value_1='Alice'; result_1='full name'; <end>"]}}
```

## Ambition
We need A LOT of data points in order to fine tune the GPT-3 model properly, as it currently has had little to none exposure to Gremlin. We also want to show it as many diverse schemas as possible, so that the model can learn to infer what the schema is based on the given input. For example, if we are asing about Alice, the model should learn that this refers to a question about a person. Likewise for a question begining with "Who".

Ideally we would have a way to validate that your contribution is valid Gremlin and would return the expected result if queried on the right database, but that would be very complicated due to the fact that we are allowing any kind of schema. So we will be revieweing manually, via pull request reviews. Help in doing this is very much appreciated.
