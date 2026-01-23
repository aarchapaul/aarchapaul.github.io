SameOriginPolicy vs CSP

CSRF vs Same-Origin Policy (SOP)

Same-Origin Policy (SOP):

Prevents JavaScript from reading responses across origins

❌ Does not stop cross-origin requests from being sent

CSRF exploits the fact that:

Requests are allowed

Responses don’t need to be read

CSP (Content Security Policy)

Can reduce attack surface

❌ Not a primary CSRF defense

Should be considered defense-in-depth only