# Emails

Email addresses are broken into the two parts the "local-part" and "domain" separated by an "@" symbol:[^1]

```
# Syntax
<local-part>@<domain>

# Example
dkulak@dataseers.ai
```

The case-sensitivity of the local-part depends entirely on the host that the domain of the email specifies.[^2] This means emails can be case-sensitive for the username. That being said, most mail systems do not distinguish email addresses based on casing.

The "domain" portion of the address is case-insensitive.[^3]

>*For all parts of the DNS that are part of the official protocol, all comparisons between character strings (e.g., labels, domain names, etc.) are done in a case-insensitive manner.  At present, this rule is in force throughout the domain system without exception.*

If we were to do any type of normalization to email addresses, it would have to occur after the "@" symbol.

[^1]: https://datatracker.ietf.org/doc/html/rfc2822#section-3.4.1
[^2]: https://www.rfc-editor.org/rfc/rfc5321#section-2.3.11
[^3]: https://www.rfc-editor.org/rfc/rfc1035#section-2.3.3
