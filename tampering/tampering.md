# Tampering

This example demonstrates tampering through script injection.

## Steps to reproduce

1. Install all dependencies

    `npm install`

2. Start the **insecure.ts** server

    `npx ts-node insecure.ts`

3. In the browser, type a potentially malicious script in the name field of the form

    ```
        <script> document.body.innerHTML = "<a href='https://google.com'> Gotcha </a>"</script>
    ```

4. Do you see the potentially malicious hyperlink being injected into the form?

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**
Insecure.ts has two vulnerabilities: it lacks input sanitization for user-submitted names, which makes it vulnerable to XSS attacks, and while the session cookie is marked as httpOnly, there is no protection against CSRF attacks due to the absence of the sameSite attribute on cookies.
2. Briefly explain how a malicious attacker can exploit them.
An attacker can inject malicious scripts into the input field (via XSS) or trick users into submitting a forged request (via CSRF), leading to unauthorized actions or data theft.
3. Briefly explain why **secure.ts** does not have the same vulnerabilties?
Secure.ts mitigates these vulnerabilities by sanitizing user inputs with escapeHTML to prevent XSS and by setting sameSite: 'strict' on the session cookie to protect against CSRF attacks.