# IsJSONValid

A simple python package for JSON validation

## Installation

```
python -m pip install "git+https://github.com/ivancmonaco/isjsonvalid.git"
```


## Usage

### Example

```
from isjsonvalid import validate

spec = {
  "name": {"type": str, "required": True},
  "age": {"type": int, "min": 0, "fallback": 0, "validator": lambda x: x >= 0},
  "role": {"type": str, "one_of": ["user", "admin"], "fallback": "user"},
  "prefs": {
    "type": dict,
    "keys": {
      "tags": {
        "type": list,
        "min_length": 1,
        "element_validator": lambda s: isinstance(s, str) and len(s) <= 10
      }
    }
  }
}

data = {"name": "Ivan", "age": -5, "role": "superuser", "prefs": {"tags": ["gojira", "metal"]}}

validate(data, spec)
```

```
ValueError: {"age": {"cause": "Incorrect value for age", "hint": ""}, "role": {"cause": "Value for role must be one of ['user', 'admin']", "hint": ""}}
```




