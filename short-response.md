Short Response: Databases Checkpoint
====================================

Answer each question below in complete sentences. Aim for 3–5 sentences per answer — enough to show that you understand the concept, not just that you memorized a definition. Use the exact terms and concepts from the lessons, but write in your own words. Specific examples and analogies are encouraged.

* * *

Question 1
----------

What is the difference between **authentication** and **authorization**? Give a concrete example of how a user would encounter each in the context of a fullstack web application.

**Your answer:**

Authentication is verifying that you are who you are, requires your login, and happens before authentication. An example of it would be when you're unlocking your phone or computer. Authorization is what you're allowed to do when you're connected to an account as a certain user. After authentication your session and permissions are checked. An example of this would be being able to edit a Google doc on your account but not being able to edit a document that someone else sent to you.

* * *

Question 2
----------

Why should passwords **never** be stored as plaintext in a database? Explain what hashing is and its key properties that allow a server to verify a password without ever storing the original?

**Your answer:**

Passwords should never be stored as plaintext in a database because it makes it easy for attackers to grab data because it is readable. Password hashes should be stored instead so that the original passwords cannot be accessed. Hashing functions turn plaintext into hashes which are computationally generated strings. They are one-way, so they are irreversible and they are pure, always returning the same hash with the same input. A server never needs to store the original password because it can compare the password hash stored in the database to the hash of the user submitted password to authenticate them.

* * *

Question 3
----------

Explain what it means when we say that "HTTP is stateless"? Explain why cookies are necessary in order to keep users logged-in across multiple sessions and how a server and a client work together to achieve this functionality.

**Your answer:**

To say "HTTP is stateless" means that the server does not remember previous HTTP requests sent by the client. This problem is solved by cookies which store the user's login credentials. The browser automatically sends the cookies to the server with every request to the same domain. This keeps the user logged in.

* * *

Question 4
----------

A frontend can hide a "Delete Account" button from users who aren't logged in. Why isn't that enough to protect the `DELETE /api/users/:id` route on the server? What are the two layers of protection that the backend implements to protect against this?

**Your answer:**

That isn't enough to protect the `DELETE /api/users/:id` route on the server because it only protects against an accidental click by the user. An attacker would directly access the API. To protect against this you use session cookies for authentication and `checkAuthentication` middleware.

* * *

Question 5
----------

What is **SQL injection**? Explain what makes the code below unsafe, then describe how parameterized queries fix the problem.

    // Unsafe — never do this!
    pool.query(`SELECT * FROM users WHERE username = '${username}'`);

**Your answer:**

A SQL injection is an attack from a malicious user that targets queries that include user input values. The code below is unsafe because an attacker could input `DROP TABLE users;` into the query and destroy the users table of your database. This can be avoided by using parameterized queries ($NUM placeholders) which separate the SQL structure from the values, which means that postgres handles the values as data instead of SQL commands.

* * *

Question 6
----------

What problem does the `/api/auth/me` endpoint pattern solve? When does the frontend call it and what does it return?

**Your answer:**

The `/api/auth/me` endpoint pattern solves the issue of having to log in again after leaving an app. The endpoint uses `userModel.find(user_id)` to find a user by their id. The frontend calls it on load and it either returns a user and their login view or a 401 error and guest view.

* * *