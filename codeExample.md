# 🧪 Code Examples: GitLab Webhook Listener

## ✅ Spring Boot Controller to Receive GitLab Webhook

```java
@RestController
public class GitlabWebhookController {

    @Value("${webhook.secret-token}")
    private String secretToken;

    @PostMapping("/gitlab/webhook")
    public ResponseEntity<String> handleWebhook(
            @RequestHeader("X-Gitlab-Token") String token,
            @RequestBody String payload) {

        if (!secretToken.equals(token)) {
            return ResponseEntity.status(HttpStatus.FORBIDDEN).body("Invalid token");
        }

        // Process the webhook payload (you can parse JSON if needed)
        System.out.println("Received webhook payload: " + payload);

        return ResponseEntity.ok("Webhook received");
    }
}
```

---

## ⚙️ Example `application.properties`

```properties
server.port=8080
webhook.secret-token=mySecretToken123
```

---

## 🧪 Sample CURL Request for Testing

```bash
curl -X POST http://localhost:8080/gitlab/webhook \
  -H "Content-Type: application/json" \
  -H "X-Gitlab-Token: mySecretToken123" \
  -d '{"object_kind": "push", "user_name": "John", "event_name": "push"}'
```

---

## 📦 Maven Dependencies (pom.xml)

```xml
<dependencies>
  <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
  </dependency>
  <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-configuration-processor</artifactId>
    <optional>true</optional>
  </dependency>
  <dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <optional>true</optional>
  </dependency>
</dependencies>
```
