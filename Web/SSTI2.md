# SSTI (Server-Side Template Injection) — Dot Bypass Explained

## What SSTI Is (no fluff)
SSTI happens when **user input is rendered inside a server-side template** (Jinja2, Twig, Velocity, etc.) **without proper sanitization**.  
If you can inject template syntax, you can execute template logic — and in weak setups, escalate to code execution.

If you don’t control the template context, **you lose**. Period.

---

## Why the Dot (`.`) Matters
In engines like **Jinja2**, the dot is used for:
- Attribute access: `obj.attr`
- Method access: `obj.method()`

Defenders often blacklist `.` thinking they’re clever.  
They’re not. The engine still exposes **attribute access via filters and functions**.

Blacklisting characters is **trash security**.

---

## Core Bypass: `|attr`
Jinja2 allows attribute access using the `attr` filter.

### Normal (blocked)
```jinja
{{ user.__class__ }}
```

#### Without Dots (blocked)
```
`{{ user | attr("__class__") | attr("__mro__") }}`
```
