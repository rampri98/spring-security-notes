# 02-configure-security-filter-chain – SecurityFilterChain Configuration

---

## ✅ @EnableWebSecurity
- Enables Spring Security’s web security support.
- Used to register and customize `SecurityFilterChain` beans. Also, `AuthenticationManager` and `PasswordEncoder`.
- Replaces `WebSecurityConfigurerAdapter` (deprecated in Spring Security 5.7+).

---

## 🔓 authorizeHttpRequests
- Defines **authorization rules** for HTTP requests.

```java
http.authorizeHttpRequests(auth -> auth
   .requestMatchers("/admin/**").hasRole("ADMIN")
   .requestMatchers("/h2-console/**").permitAll()
   .requestMatchers("/api/auth/**").permitAll()
   .anyRequest().authenticated()
)
```

---

## 🔒 sessionManagement
- Manages session-related security like setting the session creation policy.

```java
http.sessionManagement(session -> 
    session.sessionCreationPolicy(SessionCreationPolicy.STATELESS)
);
```

---

## 🔑 httpBasic() vs formLogin()

| Feature     | httpBasic()           | formLogin()               |
|-------------|-----------------------|---------------------------|
| UI          | Browser alert box     | Custom login form         |
| Use Case    | APIs, simple apps     | Web applications          |
| Credentials | Sent on every request | Stored in session         |
| Example     | `http.httpBasic();`   | `http.formLogin();`       |

---

## 🧾 headers()
- Configures **security-related HTTP headers**.

```java
http.headers(headers -> 
    headers.frameOptions().sameOrigin()
);
```

### Common Headers:
- `X-Frame-Options`
- `Content-Security-Policy`
- `Strict-Transport-Security`

---

## 🛡️ csrf()
- Protects against Cross-Site Request Forgery attacks.
- **Enabled by default** in Spring Security.
- Should be **disabled for stateless APIs** (e.g., JWT):

```java
http.csrf(csrf -> csrf.disable());
```

---

## ➕ addFilterBefore()
- Adds a custom filter **before** another in the filter chain.

```java
http.addFilterBefore(customFilter, UsernamePasswordAuthenticationFilter.class);
```

### Use Cases:
- JWT filters
- Logging filters
- Request validation filters

---

## 👤 userDetailsService
- Loads user-specific data for authentication (username, password, roles).
- You must implement `UserDetailsService`.

```java
http.userDetailsService(customUserDetailsService);
```

---