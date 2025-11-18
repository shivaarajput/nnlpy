# NNL Specification v1.0  
Near Natural Language — A Human-Readable, JSON-Compatible Data Format

---

## 1. Overview

NNL (Near Natural Language) is a human-friendly, indentation-based data format designed to be fully compatible with JSON.  
It allows humans to write structured data using simple English-like statements while retaining strict machine-readable structure.

NNL maps **1:1 to JSON**:
- `object` → NNL `contains:` block  
- `array` → NNL `are:` list  
- `string` → plain text or quotes  
- `number` → numeric literal  
- `boolean` → `true` or `false`  
- `null` → `null`  

NNL is designed so humans can write:

```
user contains:
  name is Alice.
  age is 30.
  roles are admin, editor.
```

And machines can treat it exactly like:

```json
{
  "user": {
    "name": "Alice",
    "age": 30,
    "roles": ["admin", "editor"]
  }
}
```

---

## 2. Syntax Summary

### 2.1 Statements End With a Period `.`  
Every field assignment ends with a `.`  
Anything before the final `.` is considered part of the value.

### 2.2 Assignments

#### **Scalar values**
```
key is value.
```

Examples:
```
name is Alice.
age is 25.
active is true.
rating is 4.5.
note is "Hello world.".
```

#### **Inline list**
```
key are value1, value2, value3.
```

Example:
```
tags are alpha, beta, gamma.
```

#### **Object blocks**
```
key contains:
  inner_key is value.
  something are x, y.
```

Example:
```
user contains:
  name is Bob.
  age is 20.
```

#### **Block lists**
```
key are:
  - value.
  - contains:
      id is 1.
      name is John.
```

Example:
```
items are:
  - 1.
  - 2.
  - 3.
```

Array of objects:
```
items are:
  - contains:
      id is 1.
      tags are a, b.
  - contains:
      id is 2.
      tags are c.
```

### 2.3 Indentation

NNL uses **indentation to indicate nesting**.  
Any line inside a block must be more indented than the block header.

Rules:
- Tabs = allowed (count as 4 spaces)
- Spaces = allowed
- Mixed indentation = allowed but not recommended

---

## 3. Data Types

### 3.1 Strings
Unquoted if simple:

```
name is Alice.
city is London.
```

Use quotes when:
- value contains spaces  
- value contains punctuation `, : { } [ ]`  
- value ends with a period that is part of the value

Examples:
```
note is "Hello world.".
url is "https://example.com/page?id=1".
```

### 3.2 Numbers  
Standard int & float formats:

```
count is 42.
pi is 3.141.
temperature is -4.1.
```

### 3.3 Booleans  
```
active is true.
enabled is false.
```

### 3.4 Null  
```
deleted_at is null.
```

---

## 4. Grammar (EBNF)

```
document       = statement* ;

statement      = scalar_stmt | list_inline_stmt | object_block | list_block ;

scalar_stmt    = key "is" value "." ;
list_inline_stmt = key "are" list_values "." ;

object_block   = key "contains:" newline indent statement* dedent ;

list_block     = key "are:" newline indent list_items dedent ;
list_items     = ( "-" list_item "." newline )+ ;

list_item      = value 
                | object_block_item 
                | list_inline ;

object_block_item = "contains:" newline indent statement* dedent ;

list_values    = value ("," value)* ;

value          = string | number | boolean | null ;

key            = 1*WORD ;
```

---

## 5. Whitespace Rules

- trailing spaces ignored  
- blank lines ignored  
- indentation > base indentation indicates block  

---

## 6. JSON Mapping Rules

| NNL Feature         | JSON Equivalent |
|---------------------|-----------------|
| `key is x.`         | `"key": x` |
| `key contains:`     | `"key": {...}` |
| `key are a, b.`     | `"key": [a, b]` |
| `key are:` block    | `"key": [...]` |
| `- contains:`       | `{...}` |
| `- a, b, c.`        | `[a, b, c]` |
| `null`              | `null` |

All values map cleanly to JSON types.

---

## 7. Examples

### Object
```
config contains:
  host is localhost.
  port is 8000.
```

### List
```
tags are a, b, c.
```

### List of objects
```
users are:
  - contains:
      id is 1.
      name is Alice.
  - contains:
      id is 2.
      name is Bob.
```

---

## 8. Error Handling (Optional)
Recommended parser errors:
- unexpected indentation  
- missing period  
- unclosed block  
- invalid scalar  

NNL parsers should give **helpful, human-readable** errors.

---

## 9. Design Goals
- Human-readable  
- Minimal punctuation  
- Easy to type  
- Machine-parseable  
- JSON-compatible  
- Good for configuration, APIs, documents, scripts  

---

# End of NNL Specification v1.0
