# JdbcUserDetailsManager Notes

---

## What is JdbcUserDetailsManager?

- An implementation of `UserDetailsService` that uses a **relational database**.
- Stores user credentials and authorities in **database tables**.
- Suitable for **production** systems.

---

## 🛠️ How to Configure JdbcUserDetailsManager
- Same as inMemory but JdbcUserDetailsManager bean should return JdbcUserDetailsManager(dataSource)
- Also, must have a schema.sql to create the required tables during startup in the same folder as application.properties

```sql
-- schema.sql
CREATE TABLE users (
    username VARCHAR(50) NOT NULL PRIMARY KEY,
    password VARCHAR(100) NOT NULL,
    enabled BOOLEAN NOT NULL
);

CREATE TABLE authorities (
    username VARCHAR(50) NOT NULL,
    authority VARCHAR(50) NOT NULL,
    CONSTRAINT fk_username FOREIGN KEY(username) REFERENCES users(username)
);

CREATE UNIQUE INDEX ix_auth_username ON authorities (username, authority);
```
---

## Required Database Schema

JdbcUserDetailsManager expects **two default tables**:

### 🔹 `users` table

| Column     | Type     |
|------------|----------|
| username   | VARCHAR  |
| password   | VARCHAR  |
| enabled    | BOOLEAN  |

### 🔹 `authorities` table

| Column     | Type     |
|------------|----------|
| username   | VARCHAR  |
| authority  | VARCHAR  |

You can also customize the queries if your schema is different.

---

