# JSON

Here's an example of how you could import and use json array form json file.

let's take this file.json for example:

```json
[
    {
        "sn": "1",
        "source": "Science",
        "question": "What is the chemical symbol for water?",
        "answer": "a",
        "a": "H2O",
        "b": "CO2",
        "c": "O2",
        "d": "N2",
    },
    {
        "sn": "2",
        "source": "History",
        "question": "Who was the first president of the United States?",
        "answer": "a",
        "a": "George Washington",
        "b": "Abraham Lincoln",
        "d": "John Adams",
    }
]
```

now you can import this file.json and use it in typst as follow.

```typ
json_data = json("file.json")

for mcq in json_data { 
[== #mcq.sn. #mcq.question: ] 
    for opt in ("a", "b", "c", "d", "e", "f", "g") { 
    if opt in mcq and mcq.at(opt) != "" { 
        [== #opt) #mcq.at(opt)] 
    } 
    } 
} 
```
