# LAB 02 - Exploration of Browser Security Mechanisms using Windows

# Browser Security Mechanisms

Exploration of Browser Security Mechanisms using Windows (TLS, WebAssembly, and OAuth 2.1)

---

# AIM

To explore modern browser security mechanisms on Windows by analyzing HTTPS/TLS connections, understanding WebAssembly (WASM) sandboxing, and demonstrating OAuth 2.1 authentication using a local Keycloak server.

---

# DESIGN STEPS

### Step 1

Install the required software on Windows.

- Google Chrome or Microsoft Edge
- Docker Desktop
- Python 3
- Keycloak (Docker Image)

### Step 2

Verify that Docker is running successfully.

### Step 3

Inspect HTTPS security using the browser Security panel.

### Step 4

Study WebAssembly (WASM) sandboxing concepts.

### Step 5

Deploy a local OAuth 2.1 authentication server using Keycloak.

### Step 6

Generate and decode a JWT access token.

---

# Architecture Diagram

```mermaid
graph LR

subgraph Windows_System

Browser["Chrome / Edge"]
Docker["Docker Desktop"]
Python["Python"]

end

subgraph Authentication_Server

Keycloak["Keycloak OAuth Server"]

end

subgraph Protected_Application

Client["OAuth Client"]
JWT["JWT Token"]

end

Browser --> Keycloak

Docker --> Keycloak

Keycloak --> JWT

JWT --> Client

Client --> Browser
```

---

# Browser Security Architecture

```mermaid
graph TD

User

-->

Browser

Browser

-->

TLS["TLS Certificate"]

Browser

-->

WASM["WebAssembly Sandbox"]

Browser

-->

OAuth["OAuth 2.1"]

OAuth

-->

Keycloak

Keycloak

-->

JWT

JWT

-->

Protected_Application
```

---

# OAuth 2.1 Authentication Flow

```mermaid
sequenceDiagram

participant User
participant Browser
participant Keycloak
participant Client

User->>Browser: Open Application

Browser->>Keycloak: Authentication Request

Keycloak-->>Browser: Login Page

User->>Keycloak: Username & Password

Keycloak-->>Browser: Access Token (JWT)

Browser->>Client: Send JWT

Client-->>Browser: Access Granted
```

---

# Browser Security Workflow

```mermaid
flowchart LR

Start

-->

Open_Browser

-->

Inspect_TLS

-->

Study_WASM

-->

Start_Keycloak

-->

Create_Client

-->

Generate_JWT

-->

Decode_JWT

-->

Finish
```

---

# SOFTWARE REQUIRED

- Windows 10 / Windows 11
- Google Chrome or Microsoft Edge
- Docker Desktop
- Python 3
- Internet Connection
- Keycloak Docker Image

---

# EXECUTION STEPS

## Step 1

Install Docker Desktop and verify Docker is running.

---

## Step 2

Open Command Prompt or PowerShell.

Start the Keycloak server.

```bash
docker run -d --name keycloak -p 8080:8080 ^
-e KEYCLOAK_ADMIN=admin ^
-e KEYCLOAK_ADMIN_PASSWORD=admin ^
quay.io/keycloak/keycloak:latest start-dev
```

---

## Step 3

Open the browser and navigate to

```text
http://localhost:8080
```

Login using

```text
Username : admin

Password : admin
```

---

## Step 4

Create a new Realm.

```text
EnterpriseLab
```

---

## Step 5

Create a Client.

```text
Client ID

lab-client
```

Client Type

```text
OpenID Connect
```

Enable

```text
Standard Flow
```

Redirect URI

```text
http://localhost:8080/*
```

---

## Step 6

Create a Test User.

```text
Username

student1
```

Set a password and disable the Temporary Password option.

---

## Step 7

Login using the newly created user.

Generate an OAuth Access Token (JWT).

---

## Step 8

Copy the generated JWT.

Decode the payload using Python.

```python
import base64
import json

token=input("Paste JWT: ")

payload=token.split('.')[1]+'=='

print(json.dumps(json.loads(base64.urlsafe_b64decode(payload)),indent=2))
```

---

## Step 9

Inspect the decoded JWT.

Observe the following fields.

- iss
- aud
- exp
- preferred_username
- roles
- claims

---

## Step 10

Open a secure website.

Example

```text
https://www.google.com
```

Open

```text
Developer Tools (F12)

Security
```

Verify

- Secure HTTPS connection
- TLS Certificate
- Certificate Authority
- Encryption Protocol

---

## Step 11

Study WebAssembly (WASM).

Observe that:

- WASM executes inside a browser sandbox.
- Direct operating system access is restricted.
- Memory is isolated from the operating system.
- Browser permissions control resource access.

---

# OBSERVATIONS

Students should observe the following.

- Browser establishes secure HTTPS connections using TLS.
- TLS certificates verify server identity.
- OAuth 2.1 issues JWT access tokens after successful authentication.
- JWT tokens contain user identity and authorization claims.
- WebAssembly executes inside an isolated browser sandbox.
- Browser security mechanisms prevent unauthorized operating system access.

---

# SCREENSHOTS 
<img width="1140" height="581" alt="image" src="https://github.com/user-attachments/assets/92e73787-c71d-4dae-a291-ab5cb9b27440" />

<img width="1143" height="580" alt="image" src="https://github.com/user-attachments/assets/f257d99b-ce9c-48cc-83f9-dd0ef648b6e9" />

<img width="1144" height="581" alt="image" src="https://github.com/user-attachments/assets/ceb29703-2f9e-4c33-94ed-8090f155384c" />

<img width="1141" height="641" alt="image" src="https://github.com/user-attachments/assets/ac829667-f8c1-423a-bba9-c37b7e62ab16" />

<img width="1141" height="581" alt="image" src="https://github.com/user-attachments/assets/c6863f97-2772-4462-9720-a540734a3ee2" />

<img width="734" height="558" alt="image" src="https://github.com/user-attachments/assets/80602375-632b-4ef8-8c1c-b135ee9130b1" />

<img width="934" height="519" alt="image" src="https://github.com/user-attachments/assets/8fd93612-14d3-4855-8f94-95f94c166391" />

<img width="746" height="295" alt="image" src="https://github.com/user-attachments/assets/f84049ec-087b-45f1-a470-b79b1456d816" />

# RESULT

Thus, browser security mechanisms were successfully explored on Windows. HTTPS/TLS communication was verified, OAuth 2.1 authentication was demonstrated using Keycloak, JWT tokens were generated and decoded, and WebAssembly sandboxing concepts were studied to understand modern browser security architecture.
```
