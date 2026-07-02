# Express Secrets Web Application

A small password-protected web app built with **Node.js** and **Express**. Visitors enter a password on the home page; if it is correct, the server reveals a hidden page of curated life tips and secrets.

This project demonstrates core Express concepts: routing, middleware, form handling with `body-parser`, and serving static HTML files.

---

## Features

- Simple password gate before accessing protected content
- Custom middleware to validate submitted passwords
- Server-side authorization state
- Clean separation between public login page and private secrets page

---

## Tech Stack

| Technology   | Purpose                          |
| ------------ | -------------------------------- |
| Node.js      | Runtime                          |
| Express 4    | Web server and routing           |
| body-parser  | Parse URL-encoded form data      |
| ES Modules   | Modern `import`/`export` syntax  |

---

## Prerequisites

- [Node.js](https://nodejs.org/) **v18+** recommended (ES modules support)
- npm (included with Node.js)

---

## Installation

1. Clone or download this repository.

2. Install dependencies:

```bash
npm install
```

---

## Usage

Start the server:

```bash
node index.js
```

The app runs at **http://localhost:3000**.

1. Open the home page in your browser.
2. Enter the password in the form and submit.
3. If the password is correct, you are shown the secrets page.
4. If it is wrong, you remain on the login page.

---

## How It Works

```
Browser                    Express Server
   |                              |
   |  GET /                       |
   |----------------------------->|  Serve public/index.html
   |                              |
   |  POST /check (password=...)  |
   |----------------------------->|  passwordCheck middleware
   |                              |    -> sets userIsAuthorised
   |                              |  Route handler
   |                              |    -> secret.html OR index.html
   |<-----------------------------|
```

1. **`GET /`** — Serves the login form from `public/index.html`.
2. **`passwordCheck` middleware** — Runs on every request. On `POST` submissions, it reads `password` from the form body and updates the authorization flag when the value matches the expected password.
3. **`POST /check`** — If the user is authorized, serves `public/secret.html`; otherwise, serves the login page again.

---

## Project Structure

```
Express Secrets Web Application/
├── index.js              # Express server, middleware, and routes
├── package.json          # Dependencies and project metadata
├── package-lock.json
├── public/
│   ├── index.html        # Login page with password form
│   └── secret.html       # Protected secrets content
└── README.md
```

---

## Routes

| Method | Path    | Description                                      |
| ------ | ------- | ------------------------------------------------ |
| `GET`  | `/`     | Login page                                       |
| `POST` | `/check`| Validates password and returns secrets or login  |

---

## Configuration

| Setting  | Default | Location   |
| -------- | ------- | ---------- |
| Port     | `3000`  | `index.js` |
| Password | Set in `passwordCheck` middleware in `index.js` |

To change the port, edit the `port` constant in `index.js`:

```js
const port = 3000;
```

---

## Dependencies

- **express** — HTTP server framework
- **body-parser** — Parses incoming request bodies (used for form submissions)

---

## Learning Goals

This project is useful for practicing:

- Creating Express apps with ES module syntax
- Writing custom middleware functions
- Handling `GET` and `POST` routes
- Serving HTML files with `res.sendFile()`
- Basic request authorization flow

---

## License

ISC
