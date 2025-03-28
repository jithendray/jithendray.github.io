---
tags:
  - python
layout: post
title: python-json-notes
---
#### Intro
- JSON - JavaScript Object Notation
- lightweight data format

#### JSON to python object
- `json.load()` -> read JSON from file and convert to python object
  
```python
with open('data.json', 'r') as file:
	data = json.load(file)
```

- `json.loads()` -> JSON string to python object
  
```python
json_string = '{"name":"John", "age":"32"}'
data = json.loads(json_string)
```

#### python object to JSON
- `json.dump()` -> convert object to JSON and write to file
  
```python
data = '{"name":"John", "age":"32"}'
with open('data.json', 'w') as f:
	json.dump(data, f, indent=4)
```

- `json.dumps()` -> convert object to JSON string
