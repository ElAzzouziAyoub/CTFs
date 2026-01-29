# LFI — Local File Inclusion

## What it is
**Local File Inclusion (LFI)** is a web vulnerability where an application lets the user control which **local server file** gets loaded or included.

This exists because the developer trusted user input. That’s the whole bug.

---

## Root cause (why this happens)
Typical vulnerable logic (PHP example, conceptually):

include($_GET['page']);

The app expects something like:
index.php?page=home.php

But the attacker controls `page`.

---

## How exploitation works
Instead of a normal file, the attacker supplies a filesystem path:

index.php?page=../../../../etc/passwd

If the response contains file contents → **LFI confirmed**.

You’re now reading files from the server.

---

## Why LFI is dangerous
With LFI, an attacker can:

- Read sensitive system files  
  - /etc/passwd  
  - /etc/hosts  
  - /proc/self/environ
- Leak credentials  
  - .env  
  - config.php  
  - database passwords
- Read application source code
- Escalate to **RCE (Remote Code Execution)** in many cases

LFI alone is bad.  
LFI chained with another bug = full compromise.

---

## Common LFI parameters (red flags)
Any parameter that looks like it loads a file is suspicious:

?page=  
?file=  
?path=  
?template=  
?view=  
?lang=  
?include=

If it smells like a filename, test it.

---

## Classic LFI payloads
../../../../etc/passwd  
../../../../etc/hosts  
../../../proc/self/environ  
../../../../var/log/apache2/access.log

If these return content instead of errors, the app is broken.

---

## LFI → RCE (the real danger)
LFI can become **Remote Code Execution** by abusing:

- Log file poisoning
- /proc/self/environ
- Uploaded files
- PHP wrappers like:  
  php://filter/convert.base64-encode/resource=index.php

At this point, you’re no longer reading files — you’re running code.

---

## Why this vulnerability exists
Because developers:
- Trust user input
- Don’t whitelist files
- Don’t sanitize paths
- Assume attackers won’t try ../ (they’re wrong)

---

## TL;DR
- LFI = user-controlled file inclusion
- Allows reading local server files
- Leaks secrets and source code
- Often escalates to RCE
- Exists because of bad input validation

If you see include($_GET[...]) in real code, that’s not a bug — it’s an invitation.
