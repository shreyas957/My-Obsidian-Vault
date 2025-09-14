2025-09-10 20:43

Status: [[Spring Boot]]

Tags: [[complete]]


Spring Boot's **conditional annotations** are a powerful mechanism for controlling the creation of beans and configurations based on specific conditions. They are the foundation of auto-configuration, allowing for modular and configurable applications.

---

### 📑 Quick Summary

|Annotation|Condition Checked|Example Use Case|
|---|---|---|
|`@Conditional`|Custom logic in `Condition.matches()`|Complex, custom conditions|
|`@ConditionalOnProperty`|Property value match|Feature toggles|
|`@ConditionalOnClass`|Class present in classpath|Auto-configure DB beans|
|`@ConditionalOnMissingClass`|Class NOT present|Fallback configs|
|`@ConditionalOnBean`|Another bean exists|Load dependent bean|
|`@ConditionalOnMissingBean`|Bean missing|Provide default implementation|
|`@ConditionalOnExpression`|SpEL evaluates to true|Combine multiple property checks|
|`@Profile`|Active Spring profile|Environment-specific configs|

---

### 1️⃣ `@Conditional`

**Usage:**

Java

```
@Conditional(MyCustomCondition.class)
```

This annotation takes a `Class<? extends Condition>`, which must implement the `matches(ConditionContext, AnnotatedTypeMetadata)` method. It runs **custom logic** to decide whether a bean or configuration should load. Use this for advanced conditions that can't be covered by the other annotations, such as checking for file existence or a specific system state.

### 2️⃣ `@ConditionalOnProperty`

**Usage:**

Java

```
@ConditionalOnProperty(
    prefix = "feature", 
    name = "new-ui", 
    havingValue = "true", 
    matchIfMissing = false
)
```

This annotation loads a bean only if a specified **property exists and its value matches** the criteria. Key attributes include `prefix` (optional property prefix), `name` (the property name), `havingValue` (the expected value), and `matchIfMissing` (if `true`, the bean loads even if the property is absent). This is ideal for **feature toggles**, enabling or disabling modules via configuration.
in example we have prop as `feature.new-ui`

### 3️⃣ `@ConditionalOnClass`

**Usage:**

Java

```
@ConditionalOnClass(name = "com.mysql.cj.jdbc.Driver")
```

This annotation loads a bean or configuration only if the specified **class exists on the classpath**. It's commonly used to auto-configure beans based on the presence of a dependency, like a JDBC driver or a Kafka library.

### 4️⃣ `@ConditionalOnMissingClass`

**Usage:**

Java

```
@ConditionalOnMissingClass("com.mysql.cj.jdbc.Driver")
```

The inverse of `@ConditionalOnClass`, this annotation loads a bean only if a specified **class is NOT present on the classpath**. It's useful for providing a **fallback implementation** when a primary dependency is absent.

### 5️⃣ `@ConditionalOnBean`

**Usage:**

Java

```
@ConditionalOnBean(name = "parentBean")
```

This loads a bean or configuration only if **another bean already exists** in the Spring application context. You can specify the required beans by `value` (type), `name`, or even by a specific `annotation` they must have. Use this to load **dependent beans** only if their parent beans are available.

### 6️⃣ `@ConditionalOnMissingBean`

**Usage:**

Java

```
@ConditionalOnMissingBean(MyService.class)
```

This annotation loads a bean only if **no other bean of the given type or name exists** in the context. This is a crucial annotation for creating auto-configurable modules, as it allows a framework to provide a **default implementation** that a user can easily override by simply defining their own bean of the same type.

### 7️⃣ `@ConditionalOnExpression`

**Usage:**

Java

```
@ConditionalOnExpression("'${app.env}'=='dev' or ${feature.beta:false}")
```

This annotation loads a bean if a given **Spring Expression Language (SpEL)** expression evaluates to `true`. This provides a flexible way to combine multiple conditions, such as checking properties with logical operators (`and`, `or`, `not`).

### 8️⃣ `@Profile`

**Usage:**

Java

```java
@Profile({"dev", "test"})

// dev not active
@Profile("!dev")

// combine multiple profiles 
@Profile("a & b & c")

```

This annotation activates beans or configurations only when one of the specified **Spring profiles is active**. It's the standard way to manage **environment-specific configurations** for different stages like `dev`, `test`, or `prod`.

```bash
-Dspring.profiles.active=dev   // to active profile during application startup via JVM sys parameter


// In Unix systems 
export spring_profiles_active=dev
```

In maven we do by following - 
```xml
<profiles>
    <profile>
        <id>dev</id>
        <activation>
            <activeByDefault>true</activeByDefault>
        </activation>
        <properties>
            <spring.profiles.active>dev</spring.profiles.active>
        </properties>
    </profile>
    <profile>
        <id>prod</id>
        <properties>
            <spring.profiles.active>prod</spring.profiles.active>
        </properties>
    </profile>
</profiles>
```

---

### 🧠 Cheat Sheet (Which Annotation to Use?)

- ✅ **Classpath check** → `@ConditionalOnClass` / `@ConditionalOnMissingClass`
    
- ✅ **Property check** → `@ConditionalOnProperty` / `@ConditionalOnExpression`
    
- ✅ **Bean presence check** → `@ConditionalOnBean` / `@ConditionalOnMissingBean`
    
- ✅ **Custom logic** → `@Conditional`
    
- ✅ **Environment/profile** → `@Profile`
    

---

### 🔑 Best Practices

- 🟢 Use `@ConditionalOnMissingBean` for creating **default beans** that users can easily override.
    
- 🟢 `@ConditionalOnProperty` is excellent for **feature toggles** as it allows enabling/disabling features without code changes.
    
- 🟢 Combine multiple conditions (e.g., `@ConditionalOnClass` and `@ConditionalOnProperty`) for more complex configuration scenarios.
    
- 🟢 Prefer `@Profile` for separating configurations based on your development lifecycle (dev/test/prod).