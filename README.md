# inMemoryUserDetailsManager Notes

---

## What is inMemoryUserDetailsManager?

- A built-in implementation of `UserDetailsService`.
- Stores user details (username, password, roles) **in memory**.
- Useful for:
    - Testing and prototyping
    - Small apps that don’t need a database
---
## 🛠️ How to Configure inMemoryUserDetailsManager
1. SecurityConfig 
   - UserDetailsManager bean creating new InMemoryUserDetailsManager()
   - PasswordEncoder bean
2. AuthController to create an endpoint for registering new users
3. AuthService to use userDetailsManager to createUser
```java
UserDetails user = User.withUsername(authRequest.getUsername())
                .password(authRequest.getPassword())
                .roles("USER")
                .build();
userDetailsManager.createUser(user);
```