# McAuth – Supabase Authentication for Fabric Minecraft Servers

McAuth is a **server-side Fabric mod** that integrates **Supabase authentication** with a Minecraft server.  
Players must authenticate via an external login system before being allowed to play.

This project demonstrates **secure backend-driven authentication**, UUID-based identity enforcement, and clean Fabric mod architecture.

---

## ✨ Features

- 🔐 External authentication using Supabase Auth
- 🌐 Backend-based verification (no secrets in the mod)
- 🧾 UUID-based player identity binding
- ⏳ Login timeout & automatic kick
- ⚙️ Fabric server-side implementation
- 🚫 Prevents unauthenticated server access

---

## 🧠 Architecture Overview

```

[ Web App / Launcher ]
        |
        |  Supabase Auth (JWT)
        |
    [ Backend API ]
        |
        |  Verification Result
        |
[ Fabric Server Mod ]

```

## 📁 Project Structure

```
src/main/java/org/bpl/mcAuth
├── McAuth.java                # Mod entry point
├── auth
│   ├── AuthState.java         # Tracks unauthenticated players
│   ├── AuthEvents.java        # Player join handling
│   └── AuthHttp.java          # Backend verification logic
├── command
│   └── LoginCommand.java      # /login <code> command

```

## 🚀 How It Works

1. Player logs in via a **web app or launcher**
2. Supabase authenticates the user
3. Backend generates a **short-lived login code**
4. Player joins the server and runs:
    ```/login <code>```
5. Fabric mod sends UUID + code to backend
6. Backend verifies the user and responds
7. Player is allowed or kicked

---

## 🛠️ Requirements

- Java 17+
- Fabric Loader
- Fabric API
- Minecraft (Fabric-compatible version)
- External backend (Node.js / Java / Python)
- Supabase project with Auth enabled

---

## 🔧 Configuration

### Backend Endpoint
Update this constant in `AuthHttp.java`:

```java
private static final String VERIFY_URL = "https://your-backend.com/verify";
```
The backend must return:

```json
{ 
  "allowed": true
}
```
or
```json
{ 
  "allowed": false
}
```
## 🔐 Security Considerations


✔ No Supabase keys inside the mod

✔ UUID-based authentication

✔ Short-lived login codes

✔ Async HTTP calls (non-blocking)

✔ Server-side enforcement

❌ Username-based auth

❌ Client-side verification

❌ Long-lived tokens

## 🧪 Example Backend Logic (Conceptual)

- Validate login code

- Verify Supabase JWT

- Match Supabase user ↔ Minecraft UUID

- Return authorization result

## 📌 Use Cases

- Private SMP servers

- Paid / whitelist servers

- College or portfolio projects

- OAuth-based Minecraft authentication

- Secure roleplay communities

## 📄 License

MIT License – feel free to use, modify, and extend.

## 🧑‍💻 Author

Built by BPL (Sujay and Shibasis)
Fabric • Java • Backend Integration • Supabase Auth