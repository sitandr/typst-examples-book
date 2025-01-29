# JSON

`author: MuhammadAly11`

Here's an example of how you could import and use json array form json file.

Consider the following example of data for the test you want to write:

```json
[
    {
        "sn": "1",
        "source": "Science",
        "question": "What is the chemical symbol for water?",
        "answer": "a",
        "a": "H₂O",
        "b": "CO₂",
        "c": "O₂",
        "d": "N₂",
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

You can import this file and use it in Typst:

```typ
#let json_data = json("../file.json")

#for mcq in json_data {
    [== #mcq.sn. #mcq.question: ]
    for opt in ("a", "b", "c", "d", "e", "f", "g") {
        if opt in mcq and mcq.at(opt) != "" {
            [- #opt) #mcq.at(opt)]
        }
    }
}
```
