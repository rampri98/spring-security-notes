# 01-default — Spring Security Default Configuration

## 🔐 Default Behavior
- Spring Boot auto-enables **form-based login** when `spring-boot-starter-security` is on the classpath.
- A **built-in login page** is available at `/login`.
- **All endpoints are secured** by default — authentication is required unless explicitly permitted.
- A default user is created with a **random password**, printed in the console.

```properties
spring.security.user.name=admin
spring.security.user.password=admin123
```

## 🔄 Authentication Flow Summary
1. **Filter Chain** intercepts every HTTP request.
2. **Authentication Filter** checks for login attempts and calls `AuthenticationManager`.
3. **AuthenticationManager** delegates to one or more `AuthenticationProvider`s.
4. **DaoAuthenticationProvider**:
    - Calls `UserDetailsService.loadUserByUsername()` to fetch user details.
    - Uses `PasswordEncoder.matches()` to validate the password.
5. On success, authentication info is stored in the **SecurityContext**.
6. The request continues to your **application controller** if authorized.