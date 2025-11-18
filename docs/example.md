# NNL Examples  
A practical collection of real-world patterns, showing how to use NNL effectively.

---

## 1. Basic Object

```
user contains:
  name is Alice.
  age is 30.
  active is true.
```

JSON:

```json
{
  "user": {
    "name": "Alice",
    "age": 30,
    "active": true
  }
}
```

---

## 2. Nested Objects

```
company contains:
  name is OpenAI.
  address contains:
    street is Market St.
    city is San Francisco.
    zip is 94103.
```

---

## 3. Inline Lists

```
tags are alpha, beta, gamma.
roles are admin, moderator.
```

---

## 4. Block Lists

```
scores are:
  - 10.
  - 15.
  - 22.
```

Nested list:

```
matrix are:
  - 1, 2, 3.
  - 4, 5, 6.
```

Equivalent JSON:

```json
{
  "matrix": [
    [1,2,3],
    [4,5,6]
  ]
}
```

---

## 5. Array of Objects

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

## 6. Object With Mixed Types

```
product contains:
  id is 552.
  name is Keyboard.
  price is 49.99.
  in_stock is true.
  tags are gaming, rgb.
```

---

## 7. Server Configuration Example

```
server contains:
  host is localhost.
  port is 8000.
  features are logging, metrics, caching.
  paths contains:
    home is /.
    login is /login.
```

---

## 8. Blog Post Example

```
post contains:
  title is My First Post.
  author contains:
    name is John.
    email is john@example.com.
  tags are writing, blog.
  published_at is 2025-01-01.
```

---

## 9. API Response Example

```
response contains:
  success is true.
  data contains:
    count is 2.
    items are:
      - contains:
          id is 101.
          name is Widget A.
      - contains:
          id is 102.
          name is Widget B.
```

---

## 10. Settings File Example

```
settings contains:
  theme is dark.
  autosave is true.
  refresh_interval is 30.
  plugins are formatter, linter, ai-helper.
```

---

# End of Examples
