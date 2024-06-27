Q1. 42f05b9372a9a4a470db3b52817899b99a76ee73

Q2. index

Q3. 84.25, the closest one is 84.05

Using 
```
search_query = {
    "size": 5,
    "query": {
        "bool": {
            "must": {
                "multi_match": {
                    "query": "How do I execute a command in a running docker container?",
                    "fields": ["question^4", "text"],
                    "type": "best_fields"
                }
            }
        }
    }
}
```

Q4. * How do I debug a docker container?
Using

```
search_query = {
    "size": 3,
    "query": {
        "bool": {
            "must": {
                "multi_match": {
                    "query": "How do I execute a command in a running docker container?",
                    "fields": ["question^4", "text"],
                    "type": "best_fields"
                }
            },
            "filter": {
                "term": {
                    "course": "machine-learning-zoomcamp"
                }
            }
        }
    }
}
```

Q5. 1324, closest one is 1462
Using

```
context_template = """
Q: {question}
A: {text}
""".strip()

built_context = ""

for qa_set in search_resp['hits']['hits']:
    built_context = built_context + context_template.format(question = qa_set['_source']['question'], text = qa_set['_source']['text']) + "\n\n"

prompt_template = """
You're a course teaching assistant. Answer the QUESTION based on the CONTEXT from the FAQ database.
Use only the facts from the CONTEXT when answering the QUESTION.

QUESTION: {question}

CONTEXT:
{context}
""".strip()

built_prompt = prompt_template.format(question = "How do I execute a command in a running docker container?", context = built_context)

len(built_prompt)
```

Q6. 322 is the closest from the value in notebook, which is 298