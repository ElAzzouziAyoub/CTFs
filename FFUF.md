# ffuf — Fast Web Fuzzer (Web Hacking Overview)

ffuf (Fuzz Faster U Fool) is a high-performance web fuzzing tool used in web hacking, bug bounties, and CTFs to discover hidden attack surface in web applications. It is designed to be fast, flexible, and precise, making it a standard tool for serious web attackers.

ffuf works by injecting the keyword `FUZZ` into parts of an HTTP request (URL path, parameters, headers, POST data) and systematically replacing it with values from a wordlist. The server’s responses are then analyzed to identify meaningful differences.

ffuf is commonly used to enumerate hidden directories and files, discover undocumented parameters, brute-force inputs, identify virtual hosts, and map APIs that are not exposed by the frontend.

Installation:
```bash
sudo apt install ffuf
# or
go install github.com/ffuf/ffuf@latest
```

### Basic directory and file fuzzing:
```
ffuf -u http://target.com/FUZZ -w wordlist.txt -mc 200,301,302
```

### Filtering responses by HTTP status code:
```
ffuf -u http://target.com/FUZZ -w wordlist.txt -mc 200,301,302
```

### Filtering noise by response size (critical when everything returns 200):
```
ffuf -u http://target.com/FUZZ -w wordlist.txt -fs 1234
```

### GET parameter fuzzing to discover hidden parameters:
```
ffuf -u "http://target.com/index.php?FUZZ=test" -w params.txt

```

###  POST parameter fuzzing (login forms, APIs):
```
ffuf -u http://target.com/login \
-X POST \
-d "username=admin&password=FUZZ" \
-H "Content-Type: application/x-www-form-urlencoded" \
-w passwords.txt

```

### Header fuzzing to test for auth bypasses and debug behavior:
```
ffuf -u http://target.com/ -w headers.txt -H "FUZZ: test"

```
### Virtual host (vhost) fuzzing on shared IPs:
```
ffuf -u http://target-ip/ -w subdomains.txt -H "Host: FUZZ.target.com"

```
### Recursive fuzzing to automatically scan discovered directories:
```
ffuf -u http://target.com/FUZZ -w dirs.txt -recursion

```
### Saving results for later analysis:
```
ffuf -u http://target.com/FUZZ -w wordlist.txt -o result.json -of json

```