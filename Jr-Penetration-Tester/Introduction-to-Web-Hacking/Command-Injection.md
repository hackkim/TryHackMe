# 🔥 Command Injection

---

## ✅ Task 1: Introduction (What is Command Injection?)

**Command Injection** is a critical security vulnerability that allows attackers to execute arbitrary commands on a server by exploiting improper validation or sanitization of user inputs.

### Impact and Risks:

* Unauthorized command execution
* Potential data breaches
* Privilege escalation

---

## ✅ Task 2: Discovering Command Injection

Applications become vulnerable to command injection when user input directly interacts with system-level commands without validation.

### PHP Example:

```php
<?php
$songs = "/var/www/html/songs";
if (isset($_GET["title"])) {
    $title = $_GET["title"];
    $command = "grep $title /var/www/html/songtitle.txt";
    $search = exec($command);

    if ($search == "") {
        $return = "<p>The requested song $title does not exist!</p>";
    } else {
        $return = "<p>The requested song $title exists!</p>";
    }
    echo $return;
}
?>
```

### Python Example:

```python
import subprocess
from flask import Flask

app = Flask(__name__)

def execute_command(shell):
    return subprocess.Popen(shell, shell=True, stdout=subprocess.PIPE).stdout.read()

@app.route('/<shell>')
def command_server(shell):
    return execute_command(shell)
```

---

## ✅ Task 3: Exploiting Command Injection

### Types of Command Injection:

* **Blind Injection:** No direct feedback.

  * Payload Example: `127.0.0.1 && sleep 10`

* **Verbose Injection:** Direct feedback.

  * Payload Example: `127.0.0.1 && whoami`

### Useful Payloads:

| Linux Commands | Description                       |
| -------------- | --------------------------------- |
| `whoami`       | Identify current user             |
| `ls`           | List directory contents           |
| `ping`         | Induce delays for blind injection |
| `sleep`        | Alternative delay method          |
| `nc`           | Spawn reverse shell               |

| Windows Commands | Description              |
| ---------------- | ------------------------ |
| `whoami`         | Identify current user    |
| `dir`            | List directory contents  |
| `ping`           | Induce delays            |
| `timeout`        | Alternative delay method |

---

## ✅ Task 4: Remediating Command Injection

### Preventive Methods:

1. **Avoid Vulnerable Functions** (`exec()`, `system()`, `passthru()`):

```php
<input type="text" pattern="[0-9]+">
<?php
passthru("/bin/ping -c 4 " . $_GET["ping"]);
?>
```

2. **Sanitize and Validate Inputs:**

```php
if (!filter_input(INPUT_GET, "number", FILTER_VALIDATE_NUMBER)) {
    // Reject input
}
```

3. **Payload Encoding to Bypass Filters:**

```php
$payload = "\x2f\x65\x74\x63\x2f\x70\x61\x73\x73\x77\x64";
```

---

## ✅ Task 5: Practical Command Injection

![127.0.0.1](https://github.com/user-attachments/assets/63c5be14-a303-4e7a-bbac-91e1082c0149)

**Objective:** Retrieve the flag from:

```
/home/tryhackme/flag.txt
```

### Example Payload:

```bash
127.0.0.1 && cat /home/tryhackme/flag.txt
```

Experiment with payloads to exploit vulnerabilities practically.

---

## ✅ Task 6: Conclusion

You've now learned:

* Identifying command injection vulnerabilities
* Exploitation techniques
* Preventive measures
* Practical command injection exercises

Keep practicing and exploring further!

**Happy Hacking! 🚀**
