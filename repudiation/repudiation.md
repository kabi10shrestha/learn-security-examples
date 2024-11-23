# Repudiation

The example demonstrates a vulnerability that can lead to repudiation by malicious users attempting to access the services provided by a server.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Run the server __insecure.ts__.

3. Pretend to be a malicous user and interact with the services by sending requests from the browser.

4. Do you think your actions can be repudiated?

## For you to do

1. Briefly explain the vulnerability.
In insecure.ts, there is no authentication or authorization for accessing the messages or sending them, which makes it vulnerable to unauthorized access and tampering. Anyone can send or retrieve messages, leading to potential misuse.
2. Briefly explain why the vulnerability is addressed in __secure.ts__.
In secure.ts, the application includes user authentication (even if simulated) for accessing and sending messages, ensuring only authorized users can interact with sensitive data. Additionally, request logging and error handling are added, improving traceability and security.
3. Which design pattern is used in the secure version to address the vulnerability? Briefly explain how it works?
The Middleware Pattern is used in secure.ts to address the vulnerability. The middleware is employed to intercept requests for logging, authentication, and error handling, ensuring that only authenticated users can access sensitive routes and that all actions are logged for traceability.