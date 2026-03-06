# Avila's Blog

A full-stack blog web application built with Python and Flask. Users can read posts, register accounts, leave comments, and contact the site owner—while administrators have full CRUD control over blog content.

![Python](https://img.shields.io/badge/Python-3.12-3776AB?style=flat&logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-2.3-000000?style=flat&logo=flask&logoColor=white)
![SQLAlchemy](https://img.shields.io/badge/SQLAlchemy-2.0-333333?style=flat)
![Bootstrap](https://img.shields.io/badge/Bootstrap-5.2-7952B3?style=flat&logo=bootstrap&logoColor=white)

---

## Features

### Public Features
- **Blog Feed** — Browse all published posts on the homepage
- **Individual Post View** — Read full posts with rich HTML content
- **User Registration & Login** — Secure account creation with password hashing & salt rounds
- **Comment System** — Authenticated users can leave comments with Gravatar avatars
- **About Page** — Site information and author bio
- **Contact Form** — Send messages via email (SMTP integration)

### Admin-Only Features (Role-Based Access)
- **Create Posts** — Rich text editor (CKEditor) for writing blog content
- **Edit Posts** — Update existing posts
- **Delete Posts** — Remove posts from the blog

### Technical Highlights
- Responsive, mobile-first design using Bootstrap 5
- Dynamic navigation (Login/Register vs Log Out based on auth state)
- Flash messages for user feedback
- Environment-based configuration for secrets and database URI

---

## Tech Stack

| Layer | Technology |
|-------|------------|
| **Backend** | Python 3.12, Flask 2.3 |
| **Database** | SQLAlchemy 2.0 ORM, SQLite (dev) / PostgreSQL (production) |
| **Authentication** | Flask-Login, Werkzeug password hashing (PBKDF2-SHA256) |
| **Forms** | Flask-WTF, WTForms with validation |
| **Rich Text** | Flask-CKEditor |
| **Frontend** | Jinja2 templating, Bootstrap 5, Font Awesome |
| **Email** | Python `smtplib` (SMTP) |
| **Deployment** | Gunicorn, Heroku-ready (Procfile) |

---

## Skills Demonstrated

This project showcases a range of full-stack development competencies:

### Backend Development
- **Flask** — Routing, blueprints, request/response handling, redirects
- **RESTful design** — Semantic URL structure (`/post/<id>`, `/edit-post/<id>`)
- **Decorators** — Custom `@admin_only` for role-based access control
- **Error handling** — `abort(403)` for unauthorized access, `db.get_or_404()` for missing resources

### Database & ORM
- **SQLAlchemy 2.0** — Declarative models with `Mapped` type hints
- **Relational design** — Foreign keys, one-to-many and many-to-one relationships
- **Models** — `User`, `BlogPost`, `Comment` with proper `relationship()` definitions
- **Migrations** — Schema creation via `db.create_all()`

### Security
- **Password hashing** — Werkzeug `generate_password_hash` / `check_password_hash` (PBKDF2-SHA256)
- **Session management** — Flask-Login for authenticated sessions
- **CSRF protection** — Flask-WTF form tokens
- **Environment variables** — Secrets stored in `.env`, never committed

### Form Handling & Validation
- **WTForms** — `CreatePostForm`, `RegisterForm`, `LoginForm`, `CommentForm`
- **Validators** — `DataRequired`, `URL` for input validation
- **Server-side validation** — `form.validate_on_submit()` before processing

### Frontend & UX
- **Jinja2** — Template inheritance, includes, conditionals, loops
- **Bootstrap 5** — Responsive layout, components, utilities
- **CKEditor** — Rich text input for posts and comments
- **Gravatar** — Automatic user avatars in comments
- **Flash messages** — User feedback for login errors, registration, etc.

### DevOps & Deployment
- **Environment config** — `python-dotenv` for local `.env` loading
- **Production WSGI** — Gunicorn for serving the app
- **Render** — Procfile and `runtime.txt` for cloud deployment
- **Database flexibility** — SQLite for dev, PostgreSQL for production via `DB_URI`

---

## Project Structure

```
blog-website/
├── main.py              # Flask app, routes, models
├── forms.py             # WTForms form definitions
├── requirements.txt     # Python dependencies
├── Procfile             # Render process definition
├── runtime.txt          # Python version for Render
├── static/
│   ├── css/styles.css   # Custom styles
│   └── js/scripts.js    # Navbar scroll behavior
└── templates/
    ├── header.html      # Shared navigation
    ├── footer.html      # Shared footer
    ├── index.html       # Blog feed
    ├── post.html        # Single post + comments
    ├── make-post.html   # Create/Edit post (admin)
    ├── login.html       # Login form
    ├── register.html    # Registration form
    ├── about.html       # About page
    └── contact.html     # Contact form
```

---

## Setup

### Prerequisites
- Python 3.12+
- pip

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd blog-website
   ```

2. **Create a virtual environment** (recommended)
   ```bash
   python -m venv venv
   # Windows
   venv\Scripts\activate
   # macOS/Linux
   source venv/bin/activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Configure environment variables**
   
   Create a `.env` file in the project root:
   ```
   FLASK_SECRET_KEY=your-secret-key
   DB_URI=sqlite:///posts.db
   EMAIL_KEY=your-email@gmail.com
   PASSWORD_KEY=your-app-password
   ```
   
   - `FLASK_SECRET_KEY` — Required for session security (use a strong random value in production)
   - `DB_URI` — Database connection string (defaults to SQLite if omitted)
   - `EMAIL_KEY` / `PASSWORD_KEY` — For contact form SMTP (Gmail app password)

5. **Run the application**
   ```bash
   python main.py
   ```
   
   The app will be available at `http://127.0.0.1:5001` 

### First Admin User
The first registered user (ID 1) is the admin. Register first to gain access to create, edit, and delete posts.

---

## Deployment (Render)

The project includes a `Procfile` and `runtime.txt` for Render deployment:

1. Create a Render app and add a PostgreSQL add-on
2. Set config vars: `FLASK_SECRET_KEY`, `DB_URI` (from Render Postgres), `EMAIL_KEY`, `PASSWORD_KEY`
3. Deploy via Git or Render CLI

---

## License

This project is open source and available for educational and portfolio use.
