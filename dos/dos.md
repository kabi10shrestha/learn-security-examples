# Denial-of-Service (DoS)

This example demonstrates DoS vulnerabilities and how they can be exploited.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Ignore if you have already done this once. Insert test data in the MongoDB database. Make sure the mongod is up and running by typing the `mongosh` command in the termainal. If mongod process is up then you will see that the connection was successful. Command to insert test data:

    `$ npx ts-node insert-test-users.ts`

This will create a database in MongoDB called __infodisclosure__. Verify its presence by connecting with mongosh and running the command `show dbs;`.

2. Start the **insecure.ts** server

    `$ npx ts-node insecure.ts`

3. In the browser, pretend to be a hacker and type a malicious request

    ```
        http://localhost:3000/userinfo?id[$ne]=
    ```

4. Do you see the server crashing?

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts** that can lead to a DoS attack.
The insecure.ts application lacks rate limiting, allowing attackers to flood the server with requests, potentially overwhelming it. Additionally, the id query parameter is used directly in the database query without validation, which can cause inefficiencies or even crashes.
2. Briefly explain how a malicious attacker can exploit them.
Malicious users can exploit the lack of rate limiting by sending a large number of requests, causing a DoS attack by overloading the server. The unvalidated inputs allow attackers to inject large or malformed data, potentially leading to resource-intensive database queries that degrade performance.
3. Briefly explain the defensive techniques used in **secure.ts** to prevent the DoS vulnerability?
secure.ts mitigates DoS risks by implementing rate limiting, which restricts requests to 1 per IP every 5 seconds, reducing the impact of flooding attacks. It also includes error handling with a try-catch block to prevent crashes and provides proper error responses when something goes wrong.