---
title: Ch03 Control Flow
date: 2025-12-27
author: Your Name
cell_count: 80
score: 80
---

# Python Control Flow (if, loops, match)Control flow turns business intent into executable logic using conditionals, loops, and pattern matching.

## 1. Strategic Overview

Primary constructs: if/elif/else, for/while loops, break/continue/else, match/case. They encode rules, decisions, state transitions, and fallbacks.

## 2. Enterprise Significance

Good structure avoids spaghetti logic, hidden edge cases, and duplication; delivers readable, testable, predictable behavior.

## 3. Core Building Blocks of Control Flow

- Conditionals: if / elif / else, ternary expressions- Loops: for over iterables; while over conditions- Loop modifiers: break, continue, else on loops- Pattern matching: match / case for multi-branch logic (3.10+).

## 4. if / elif / else — Conditional Control


```python
if user_is_active:    send_welcome_email()
```


```python
if score >= 90:    grade = 'A'elif score >= 80:    grade = 'B'elif score >= 70:    grade = 'C'else:    grade = 'D'
```

Best practices: keep conditions simple, order specific→general, avoid deep nesting; extract functions or use pattern matching when complex.

## 5. Truthiness and Condition Semantics

Falsy: 0, 0.0, None, '', [], {}, set(), False.


```python
if items:  # non-empty    process(items)else:    handle_empty()
```


```python
if user is None:    raise ValueError('User required')
```

Use truthiness for emptiness checks; use explicit comparisons for clarity when needed.

## 6. Ternary Conditional Expressions

Short inline conditional for simple assignments.


```python
status = 'active' if is_enabled else 'disabled'
```

Guidelines: keep ternaries simple; avoid nesting—use standard if blocks for complex logic.

## 7. for Loops and the Iteration Protocol

for loops iterate over any iterable (lists, generators, dicts, files) using the iterator protocol (iter + next until StopIteration).


```python
for user in users:    send_notification(user)
```

### 7.1 Enumerating with index


```python
for index, user in enumerate(users):    log_index(index, user)
```

### 7.2 Iterating over dictionaries


```python
for key, value in config.items():    print(key, value)
```

Best practices: prefer for over while; use enumerate/.items()/.values()/.keys() instead of manual indexes.

## 8. while Loops — Condition-based Repetition


```python
retries = 0while retries < MAX_RETRIES:    if do_operation():        break    retries += 1
```

Use while when iteration count depends on a condition (polling, retries, state machines); avoid infinite loops by clearly updating conditions.

## 9. break, continue, and pass

### 9.1 break


```python
for user in users:    if user.id == target_id:        found = user        break
```

### 9.2 continue


```python
for user in users:    if not user.is_active:        continue    process_active_user(user)
```

### 9.3 pass


```python
def future_feature():    pass
```

Use break to exit, continue to skip to next iteration, and pass as a placeholder for required but empty blocks.

## 10. Loop else Clauses — Underused but Powerful


```python
for user in users:    if user.id == target_id:        found = user        breakelse:    raise LookupError('User not found')
```

else runs only if the loop completes without break—useful for search/retry loops; document behavior if team is unfamiliar.

## 11. Structural Pattern Matching: match / case (Python 3.10+)

match enables expressive branching based on structure and content of values, replacing long if/elif chains.


```python
def handle_event(event):    match event:        case {"type": "login", "user": user}:            handle_login(user)        case {"type": "logout", "user": user}:            handle_logout(user)        case _:            handle_unknown(event)
```

Key benefits: declarative branching on structure; works with literals, sequences, mappings, classes, and more.

## 12. Pattern Types in match / case

### 12.1 Literal patterns


```python
match status:    case "pending":        ...    case "approved":        ...    case "rejected":        ...
```

### 12.2 OR patterns


```python
match status:    case "pending" | "in_review":        queue_for_approval()
```

### 12.3 Wildcard pattern


```python
case _:    # default / fallback    ...
```

### 12.4 Sequence patterns


```python
match point:    case [x, y]:        handle_2d(x, y)    case [x, y, z]:        handle_3d(x, y, z)
```

### 12.5 Mapping patterns


```python
match msg:    case {"type": "error", "code": code}:        handle_error(code)
```

### 12.6 Class patterns


```python
class Event:    def __init__(self, kind, payload):        self.kind = kind        self.payload = payloadmatch event:    case Event(kind="login", payload=payload):        handle_login(payload)
```

### 12.7 Guard patterns (if within case)


```python
match user:    case {"age": age} if age >= 18:        allow_access()    case _:        deny_access()
```

## 13. When to Use match vs if / elif

Use if/elif for simple, independent checks; use match for many branches on one value/structure. If you have 5–10+ structured branches, consider match.

## 14. Control Flow and Error Handling

Use if/match for expected variation; exceptions for unexpected errors. Avoid using exceptions for normal branching.


```python
# Anti-patterntry:    result = maybe_get_value()except ValueError:    result = default_value# Preferif has_value():    result = get_value()else:    result = default_value
```

## 15. Side-Effect Discipline in Control Flow


```python
# Less idealif user.is_active and send_email(user):    log('Email sent')# Betterif user.is_active:    email_sent = send_email(user)    if email_sent:        log('Email sent')
```

Separate decision logic from side effects for readability and testability.

## 16. Refactoring Nested Control Flow


```python
# Deep nestingif condition_a:    if condition_b:        if condition_c:            do_something()# Guard clausesif not condition_a:    returnif not condition_b:    returnif not condition_c:    returndo_something()# Extract functionif can_process(order):    process(order)
```

Use match for complex structured branching; prefer guard clauses and extraction over deep nesting.

## 17. Performance Considerations

Control flow rarely the bottleneck: prefer clarity. Use for over manual indexing; avoid repeated condition checks in hot loops; optimize algorithm before micro-branches.

## 18. Common Control Flow Anti-Patterns

- Deeply nested if/else- Giant if chain on same variable (prefer match/dispatch)- Using exceptions as normal branches- Unreachable branches- Overuse of break/continue- Hidden mutations in condition checks

## 19. Governance Model for Control Flow

Business Rule → Control Structure Choice (if/loop/match) → Branch Clarity → Side-Effect Isolation → Branch Test Coverage → Observability for critical decisions.

## 20. Summary

Use if/elif for clear branching, for/while for iteration, break/continue/else for explicit loop behavior, match/case for structured branching, and prioritize clarity and testability over micro-optimizations.


---
**Score: 80**