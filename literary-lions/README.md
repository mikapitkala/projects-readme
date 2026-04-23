# fancyforum

A web forum that allows users to communicate, associate categories with posts, like/dislike posts & comments, and filter posts.

## ✨ Features

### Core Forum Functionality
- **User Authentication**: Secure registration and login with email/username/password
- **Posts & Comments**: Create and engage in literary discussions
- **Categories**: Organize discussions by books, genres, character studies, etc.
- **Like/Dislike System**: React to posts and comments with engagement metrics
- **Post Filtering**: Filter by category, your own posts, or liked posts
- **Guest Access**: Non-registered users can read all discussions

### Enhanced User Experience
- **Search Functionality**: Find past discussions and insights easily
- **Recent Posts**: Stay updated with latest literary conversations
- **Responsive Design**: Beautiful glassmorphism UI that works on all devices
- **Comprehensive Seed Functions:** Seed some quality content on your brand new forum to get conversation started
- **Automatically Fetches Book Covers:** Makes an attempt to look up all the book covers from Open Library API. There is a fallback for covers it can't quite figure out.

### Technical Excellence
- **SQLite Database**: Lightweight, efficient data storage
- **Session Management**: Secure UUID-based sessions with cookies
- **Password Encryption**: Secure password storage using bcrypt
- **Docker Support**: Containerized deployment for easy hosting
- **Database Migrations**: Automated schema updates and patches

## 🚀 Quick Start

### Prerequisites
- Go 1.21 or higher
- Docker (for containerized deployment)
- SQLite 3 CLI

### Setup

1. **Clone and setup**

```
   git clone <repository-url>
   cd literary-lions-forum
   go mod download
```

Run the application

```
go run cmd/forum/main.go
```

Access the forum
    Open http://localhost:8080
    First time will take a little longer, because it's seeding some categories, posts and comments and looking up book covers. Subsequent runs will be faster once the data is cached in the db
    Register your first account
    Start reading and creating literary discussions!

    You have access to an admin account. Follow the instructions in the terminal.


Docker Deployment

    Build the container

``` bash
docker build -t literary-lions-forum .
```

Run with persistent data

```bash
docker run -p 8080:8080 -v $(pwd)/data:/app/data literary-lions-forum
```

Database Design

The forum uses SQLite with a carefully designed schema optimized for literary discussions:
Core Entities

```
    Users: Authentication and member profiles
    Categories: Book clubs, genres, reading groups
    Posts: Discussion topics and literary analyses
    Comments: Threaded replies and insights
    Reactions: Like/dislike engagement system
```

Key Relationships

    Users create posts in categories
    Posts contain multiple threaded comments
    Users can like/dislike posts and comments
    Categories organize discussions by books and themes

See documentation/fancyForum_ERD.svg for detailed entity relationship diagrams.

## 🏗️ Project Structure

```
literary-lions-forum/
├── cmd/forum/main.go              # Application entry point & routing
├── internal/                      # Internal application logic
│   ├── auth/                      # Authentication & session management
│   ├── database/                  # SQLite interface & models
│   ├── handlers/                  # HTTP request handlers
│   └── middleware/               # Security middleware
├── web/                          # Frontend assets
│   ├── static/css/               # Glassmorphism styling
│   ├── static/img/               # Background images
│   └── templates/                # HTML templates
├── data/                         # Database & migrations
│   ├── forum.db                 # SQLite database file
│   ├── schema.sql               # Initial database schema
│   └── patch/                   # Database migration files
└── documentation/               # Technical documentation
```

