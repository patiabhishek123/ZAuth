# 🛡️ ZAuth - Open Source Authentication as a Service

![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=nodedotjs&logoColor=white)
![Express.js](https://img.shields.io/badge/Express.js-000000?style=flat-square&logo=express&logoColor=white)
![JWT](https://img.shields.io/badge/JWT-000000?style=flat-square&logo=jsonwebtokens&logoColor=red)
![Bcrypt](https://img.shields.io/badge/Bcrypt-4C75A1?style=flat-square&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCA1MCA1MCI+PHBhdGggZmlsbD0iIzQwYjYxMiIgZD0iTTEyLjUgNDAuNmg1LjV2LTVuMTE0SDExLjJsNS41LTcuNzE0aDUuMjI4TDE3LjkgMTloNy42NmwyLjEtM3YtMy41aC0xMi42bC01LjkgOS42VjQzLjY1eiIvPjxwYXRoIGZpbGw9IiM2NmM2YjMiIGQ9Ik0yNSA0MC42VjcuOTExbDEwLjMgMTQuMTI5LTMuNCAzLjVIMjEuNVY0MC42eiIvPjwvc3ZnPg==&logoColor=white)
![License](https://img.shields.io/github/license/YourUsername/ZAuth?style=flat-square)
![GitHub issues](https://img.shields.io/github/issues/YourUsername/ZAuth?style=flat-square)

## 🌟 Overview

**ZAuth** is an open-source, self-hosted Authentication as a Service (AaaS) platform designed for developers who need robust, secure, and easily integrated authentication for their applications.

The project is built as a **Monorepo** using **Turborepo** to separate the core **API** from the **Website/Documentation**.

### Key Features (v1.0)

* **Secure Password Hashing:** Uses **bcrypt** with a configurable salt factor for maximum password security.
* **Stateless Authentication:** Implements **JSON Web Tokens (JWT)** for efficient, stateless API authentication and authorization.
* **Core Endpoints:** Provides simple, powerful REST endpoints for `Register`, `Login`, and `Token Refresh`.
* **Scalable Architecture:** Modular structure (`modules/auth`, `modules/user`) to support future growth (e.g., MFA, OAuth, WebAuthn).

## 🚀 Getting Started

Follow these steps to set up the ZAuth Monorepo for local development.

### Prerequisites

* Node.js (LTS version recommended, e.g., 18.x or 20.x)
* npm or pnpm (recommended for monorepos)
* A database (e.g., PostgreSQL, MongoDB, etc. - Update based on your actual choice)

### Installation

1.  **Clone the Repository:**

    ```bash
    git clone [https://github.com/YourUsername/ZAuth.git](https://github.com/YourUsername/ZAuth.git)
    cd ZAuth
    ```

2.  **Install Dependencies:**
    This command runs from the root of the monorepo and installs dependencies for both `zauth-api` and `zauth-web`.

    ```bash
    npm install
    # OR
    pnpm install
    ```

3.  **Setup Environment Variables:**
    Create a `.env` file in the `packages/zauth-api` directory. Copy the contents from `.env.example`.

    ```bash
    # packages/zauth-api/.env

    # Server Configuration
    PORT=3000

    # Database Configuration (Example: PostgreSQL)
    DB_HOST=localhost
    DB_USER=zauth_user
    DB_PASS=secret_password
    DB_NAME=zauth_db

    # JWT Secrets (CRITICAL: Change this to a long, complex string!)
    JWT_SECRET="YourVerySecureAndLongSecretKeyHere"
    JWT_EXPIRY="1h" # Token expiration time
    ```

### Running the Project

Use the central `npm` or `pnpm` scripts from the root directory to manage services:

| Command | Action | Location |
| :--- | :--- | :--- |
| `npm run dev` | Runs both the API and the Web services in development mode. | `zauth-api` & `zauth-web` |
| `npm run dev:api` | Runs only the Authentication API. | `zauth-api` |
| `npm run dev:web` | Runs only the Website/Docs. | `zauth-web` |
| `npm run build` | Builds both the API and the Web services for production. | `zauth-api` & `zauth-web` |

## ⚙️ Core API Endpoints (`/api/v1`)

The ZAuth API runs on the configured port (default: `http://localhost:3000`).

| Method | Endpoint | Description | Authentication |
| :--- | :--- | :--- | :--- |
| **`POST`** | `/api/v1/auth/register` | Creates a new user account. | Public |
| **`POST`** | `/api/v1/auth/login` | Authenticates user and returns a new JWT. | Public |
| **`POST`** | `/api/v1/auth/refresh` | Generates a new access token using a refresh token. | Refresh Token |
| **`GET`** | `/api/v1/user/profile` | Retrieves the authenticated user's profile data. | Access Token |

### Example Usage (Login)

**Request** (`POST` to `http://localhost:3000/api/v1/auth/login`):

```json
{
    "email": "testuser@example.com",
    "password": "mySecurePassword123"
}