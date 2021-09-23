# YAML File

## Simple Types
```yaml
# str
name: "Mike"
occupation: 'programmer'
# int
age: 23
# float
gpa: 3.5
fav_num: 1e+10
# boolean
male: true
# date and time
birthday: 1993-06-02 14:33:22 # ISO 8601 (standard)
# NULL
flaws: null

# Object
person:
    name: "Again"
    age: 26
```

## List
```yaml
hobbies:
    - hiking
    - fishing
    - programming
# Alternative definition
languages: ["Cpp", "Python", "Vimscript"]
friends:
    - name: "Steph"
      age: 22
    - {name: "Adam", age: 22}
    - 
        name: "Joe"
        age: 23
    # These three ways are identical
```

## MultiLine String
```yaml
# Rendered as single line
description: >
    YAML is a data serialization language designed
    to be human-friendly and work well with modern
    programming languages for common everyday tasks.
# Formatting to be preserved
signature: |
    Mike
    Giraffe Academy
    email - giraffeacademy@gmail.com
```

## Anchoring
Anchors and aliases let you identify an item with an anchor, and then refer to that item with an alias later in
the same document.
* **Anchors** are identified by an `&` character
* **Aliases** by an `*` character
* Anchor names can also be reused, aliases will refer to the most recent instance of an anchor
* In alias, `<<` is a special key that indicates key-values from another mapping should be merged into this mapping

```yaml
person:
    name: &name "Mike"
    id: *name # id: "Mike"

base: &base
    foo: "foo"

derive:
    <<: *base # foo: "foo"
    bar: "bar"
```

## Coercive Types
```yaml
age: !!float 23 # 23.0
gpa: !!str 3.5 # "3.5"
```

## PyYAML
`pip install pyyaml` to install the package

```python
import yaml

def yaml_loader(filepath):
    """ Loads a yaml file """
    with open(filepath, 'r') as file_descriptor:
        data = yaml.load(file_descriptor)
    return data
    
def yaml_dumper(filepath, data):
    """ Dumps a yaml file """
    with open(filepath, 'w') as file_descriptor:
        yaml.dump(data, file_descriptor)
        
if __name__ == "__main__":
    filepath1 = "test1.yaml"
    data1 = yaml_loader(filepath)
    
    items = data1.get("items")
    for item_name, item_value in items.items():
        print(item_name, item_value)
        
    filepath2 = "test2.yaml"
    data2 = {
        "items": {
            "sword": 100,
            "axe": 80,
            "boots": 40
        }
    }
    yaml_dumper(filepath2, data2)
```
