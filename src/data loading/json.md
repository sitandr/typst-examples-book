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
        "e": "H2SO4",
        "f": "NaCl",
        "g": ""
    },
    {
        "sn": "2",
        "source": "History",
        "question": "Who was the first president of the United States?",
        "answer": "a",
        "a": "George Washington",
        "b": "Abraham Lincoln",
        "c": "Thomas Jefferson",
        "d": "John Adams",
        "e": "James Madison",
        "f": "Benjamin Franklin",
        "g": ""
    },
    {
        "sn": "3",
        "source": "Geography",
        "question": "What is the capital city of France?",
        "answer": "b",
        "a": "Berlin",
        "b": "Paris",
        "c": "London",
        "d": "Madrid",
        "e": "Rome",
        "f": "Amsterdam",
        "g": ""
    },
    {
        "sn": "4",
        "source": "Mathematics",
        "question": "What is the value of Pi (\u03c0) to two decimal places?",
        "answer": "c",
        "a": "2.14",
        "b": "2.71",
        "c": "3.14",
        "d": "3.72",
        "e": "4.00",
        "f": "2.00",
        "g": ""
    },
    {
        "sn": "5",
        "source": "Literature",
        "question": "Who wrote the play \"Romeo and Juliet\"?",
        "answer": "a",
        "a": "William Shakespeare",
        "b": "Charles Dickens",
        "c": "Mark Twain",
        "d": "Jane Austen",
        "e": "Ernest Hemingway",
        "f": "F. Scott Fitzgerald",
        "g": ""
    },
    {
        "sn": "6",
        "source": "Technology",
        "question": "Which company developed the Windows operating system?",
        "answer": "d",
        "a": "Apple Inc.",
        "b": "Google",
        "c": "IBM",
        "d": "Microsoft",
        "e": "Amazon",
        "f": "Facebook",
        "g": ""
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
