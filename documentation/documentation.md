# 📘 GitLab Webhook Listener API

## 🧾 Description

This service listens to GitLab webhook events (such as `push`, `merge_request`, etc.) and handles them securely using a token verification mechanism.

---

## 🛠️ Technologies Used

- Java 17+
- Spring Boot 3.x
- Maven
- OpenAPI 3.0 (Swagger)
- GitLab Webhook Integration

---

## 🚀 How to Run

### Prerequisites:

- Java 17+
- Maven installed
- GitLab project with webhook configured

### Steps:

```bash
git clone https://github.com/your-org/gitlab-webhook-listener.git
cd gitlab-webhook-listener
mvn spring-boot:run
```

Application will start on:  
`http://localhost:8080`

---

## 🌐 API Endpoints

### 🔸 POST `/gitlab/webhook`

Receives and processes GitLab webhook events.

| Header | Type   | Required | Description                  |
|--------|--------|----------|------------------------------|
| `X-Gitlab-Token` | string | ✅ Yes     | Secret token for validation |

#### Example Payload (Push Event):

```json
{
  "object_kind": "push",
  "event_name": "push",
  "user_name": "John Doe",
  "project": {
    "name": "example-repo",
    "git_http_url": "https://gitlab.com/example-repo"
  }
}
```

#### Responses:

- `200 OK`: Webhook processed
- `403 Forbidden`: Invalid token
- `400 Bad Request`: Malformed payload

---

## 🔐 Security

To secure the endpoint:

1. Set a secret token in GitLab → **Settings → Webhooks**
2. Use the same token in your application (`application.properties`):

```properties
webhook.secret-token=mySecretToken123
```

---

## 🧪 Testing the Webhook Locally

You can use `curl` or Postman:

```bash
curl -X POST http://localhost:8080/gitlab/webhook \
  -H "Content-Type: application/json" \
  -H "X-Gitlab-Token: mySecretToken123" \
  -d @sample-payload.json
```

---

## 📄 License

MIT License
