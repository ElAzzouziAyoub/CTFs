
This is the **bare‑minimum mental model** you need to stop randomly poking servers and actually control them.

---

## 1️⃣ What HTTP actually is

HTTP is just:

```
CLIENT  ──request──▶  SERVER
CLIENT  ◀─response── SERVER
```

Nothing more. No magic. No mystery.

A **request** has:

1. Method
    
2. URL
    
3. Headers
    
4. Body (optional)
    

A **response** has:

1. Status code
    
2. Headers
    
3. Body
    

---

## 2️⃣ HTTP Methods (memorize this)

|Method|Meaning|Body?|
|---|---|---|
|GET|Read data|❌|
|POST|Send data / login|✅|
|PUT|Replace data|✅|
|PATCH|Modify data|✅|
|DELETE|Delete data|Sometimes|

If you send a body with GET, you’re already wrong.

---

## 3️⃣ Headers (control everything)

Headers are **metadata** about the request.  
They tell the server **how to interpret** what you send.

Format:

```http
Header-Name: value
```

### Common headers you MUST know

|Header|Purpose|
|---|---|
|Content-Type|Format of the body|
|Authorization|Auth tokens|
|Cookie|Session data|
|User-Agent|Client identity|
|X-*|Custom / dev headers|

If headers are wrong → server ignores you.

---

## 4️⃣ Body (the actual data)

The body is the **payload**.

⚠️ The body ONLY works if the **Content-Type matches**.

### JSON body

```json
{
  "email": "user@test.com",
  "password": "123"
}
```

Requires:

```http
Content-Type: application/json
```

### Form body

```
email=user@test.com&password=123
```

Requires:

```http
Content-Type: application/x-www-form-urlencoded
```

Mismatch = server sees nothing.

---

## 5️⃣ `curl` basics (STOP guessing)

### Simple GET

```bash
curl http://example.com
```

### Show headers + body

```bash
curl -i http://example.com
```

### Only headers

```bash
curl -I http://example.com
```

---

## 6️⃣ POST request with JSON (correct way)

```bash
curl -X POST http://example.com/login \
  -H "Content-Type: application/json" \
  -d '{"email":"user@test.com","password":"123"}'
```

Breakdown:

- `-X POST` → method
    
- `-H` → header
    
- `-d` → body
    

No header = broken request.

---

## 7️⃣ curl flags you must know

|Flag|Meaning|
|---|---|
|-X|HTTP method|
|-H|Add header|
|-d|Send body|
|-i|Show response headers|
|-v|Verbose (debug)|
|-L|Follow redirects|

If you’re not using `-i` or `-v`, you’re blind.

---

## 8️⃣ Status codes (read them)

|Code|Meaning|
|---|---|
|200|OK|
|201|Created|
|400|Bad request (you messed up)|
|401|Unauthorized|
|403|Forbidden|
|404|Not found|
|500|Server error|

400‑level = **your fault**  
500‑level = server fault

---

## 9️⃣ Why your earlier request failed (example)

You sent JSON **without** telling the server:

```http
Content-Type: application/json
```

Express ignored your body.  
`req.body` was empty.  
Server looked for `email = undefined`.

That’s not hacking — that’s user error.

---

## 🔟 CTF mindset (important)

Most web challenges exploit:

- Missing headers
    
- Trust in client input
    
- Dev-only headers
    
- Poor method validation
    

If you understand HTTP, **tools barely matter**.

---

## Final rule

If a request fails:

- Don’t retry randomly
    
- Inspect headers
    
- Inspect body
    
- Inspect status code
    

HTTP is strict. Learn the rules, and it obeys you.