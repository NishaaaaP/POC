# POC
Axigen Mail Server RXSS

# Vulnerability Report: Persistent Cross-Site Scripting (XSS) in Axigen Mail Server WebAdmin Branding

**Reporter:** Nisha Thakur | Cyber Security Associate | Green Tick Nepal Pvt. Ltd.

---

## Affected Product

- **Product:** Axigen Mail Server  
- **Component:** WebAdmin Branding  
- **Version:** 10.6.15  

---

## Vulnerability Summary

A persistent Cross-Site Scripting (XSS) vulnerability exists in the WebAdmin branding feature of Axigen Mail Server version 10.6.15. An authenticated administrator can inject arbitrary JavaScript code through the brand name field in the global settings. This malicious script executes whenever the dashboard page is loaded, potentially compromising the administrator’s session.

---

## Vulnerability Details

- **Vulnerability Type:** Cross-Site Scripting (Stored/Persistent)
- **CWE:** CWE-79 (Improper Neutralization of Input During Web Page Generation)
- **Impact:**
  - Execution of arbitrary JavaScript code in the administrator’s session context.
  - Theft of session cookies.
  - Potential full compromise of administrative sessions.
  - Elevated risk of further server or application compromise through hijacked sessions.

---

## Preconditions for Exploitation

- Attacker must have valid administrator login credentials.
- Attacker must access Global Settings to modify branding.
- The administrator’s browser must visit the affected dashboard page after the malicious branding is saved.

---

## Technical Details and Steps to Reproduce

1. Log in to the application with valid administrator credentials.
2. Visit the below crafted URL, injecting a JavaScript payload via the domain name parameter:

```
https://172.16.15.13:9443/?_h=e3c4309339633cabffa7981595d9e9a4&page=uc&domain_name=asdasdss"><script>alert(1)</script>
```

3. Observe an alert dialog displaying the number "1," demonstrating arbitrary JavaScript execution.

---

## Proof of Concept

The injected script executes an alert showing a JavaScript dialog, confirming the XSS vulnerability. Malicious scripts run in the administrator context upon visiting the dashboard page, potentially enabling cookie theft and session hijacking.

---

## Suggested Mitigations

- Sanitize inputs in branding fields before storing data to prevent malicious script injection.
- Implement robust HTML and JavaScript escaping in all user-controllable input fields.
- Enforce secure coding practices to neutralize user input used in web page generation, thus preventing CWE-79 related vulnerabilities.

---

## References

- CWE-79: Improper Neutralization of Input During Web Page Generation  
- Cross-Site Scripting (XSS) attack techniques and prevention best practices


[9] https://www.martellosecurity.com/kb/mitre/cwe/79/
[10] https://owasp.org/www-community/attacks/xss/
[11] https://www.codecademy.com/forum_questions/51fcfadd80ff33a93f003698
