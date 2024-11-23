# Privilege Escalation

The example demonstrates a privilege escalation vulnerability and how to exploit it.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Start the **insecure.ts** server

    `$ npx ts-node insecure.ts`

3. In the browser, send a GET request

    ```
        http://localhost:3000/send-form
    ```

4. Try different UserIds and see which one gives you authorized access to change the role of that user.

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**
insecure.ts is vulnerable to privilege escalation because it uses insecure authorization logic. Specifically, it checks the user's role directly from the database without validating that the user making the request is actually authorized to perform the action.
2. Briefly explain how a malicious attacker can exploit them.
An attacker could exploit this vulnerability by sending a request with a valid userId and a new role, bypassing the authorization check. Since the role is updated based on the user's data without proper session management or authentication, an attacker could escalate their privileges to 'admin'.
3. Briefly explain the defensive techniques used in **secure.ts** to prevent the privilege escalation vulnerability?
secure.ts uses session-based authentication to ensure the user making the request is logged in and has the correct permissions. Only users with the 'admin' role in the session can update roles, preventing unauthorized users from escalating privileges.