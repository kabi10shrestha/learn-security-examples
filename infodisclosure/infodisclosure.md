# Tampering

This example demonstrates information disclosure by injecting malicious query objects to a NoSQL database.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Insert test data in the MongoDB database. Make sure the mongod is up and running by typing the `mongosh` command in the termainal. If mongod process is up then you will see that the connection was successful. Command to insert test data:

    `$ npx ts-node insert-test-users.ts`

This will create a database in MongoDB called __infodisclosure__. Verify its presence by connecting with mongosh and running the command `show dbs;`.

2. Start the **insecure.ts** server

    `$ npx ts-node insecure.ts`

3. In the browser, pretend to be a hacker and type a malicious request

    ```
        http://localhost:3000/userinfo?username[$ne]=
    ```

4. Do you see user information being displayed despite the malicious request not having a valid username in the request?

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**
insecure.ts is vulnerable to NoSQL injection because it directly uses the username query parameter in the MongoDB query without validation or sanitization. This allows an attacker to craft malicious input that could manipulate the database query.
2. Briefly explain how a malicious attacker can exploit them.
An attacker can exploit this vulnerability by injecting special characters or query operators (e.g., $ne, $gt) into the username parameter, potentially bypassing authentication and gaining unauthorized access. This could allow the attacker to retrieve sensitive user data or manipulate the database.
3. Briefly explain the defensive techniques used in **secure.ts** to prevent the information disclosure vulnerability?
In secure.ts, the username input is validated to ensure it is a string, and any non-alphanumeric characters are sanitized by removing them. This prevents NoSQL injection by ensuring the input used in the database query is safe and free of malicious characters.