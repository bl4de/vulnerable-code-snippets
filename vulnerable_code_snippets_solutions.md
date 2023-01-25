## Vulnerable Code Snippets Solutions
https://github.com/yeswehack/vulnerable-code-snippets


### XSS/1

Payload:

```
http://127.0.0.1:5000/profile?name=bl4de%3C/script%3E%3Cscript%3Ealert`boom!`%3C/script%3E%3Cscript%3E
```

`name = name.replace('\'', '', -1)` sanitizes `'` character to prevent from escaping
the string `name = '%s';`. However, it does not prevent from using `</script>` tags, which means we can close opening `<script>` tag in the template and inject our own, like in the payload.

### LFI/1

Payload:

```
http://localhost/vulnerable-code-snippets/LFI/1/18-LFI.php?file=/etc/passwd
```

`PathFilter()` function does not sanitize absolute paths, only looks for
Path Traversal payloads (`../`)
