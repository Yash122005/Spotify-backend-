# 🎵 Spotify Clone Backend API
**Postman Documentation: https://documenter.getpostman.com/view/46428929/2sBXwqqVsv**

A **Spotify Clone Backend** built using **Node.js, Express.js, MongoDB, and ImageKit.io** that provides authentication, music upload, album management, and protected routes for users and artists.

This backend powers a music streaming application where:

* Users can browse songs and albums
* Artists can upload music and create albums
* Music files are stored and delivered using **ImageKit CDN**
* Authentication is handled securely using cookies and middleware

---

# 🚀 Features

### 🔐 Authentication System

* User registration
* User login
* Logout functionality
* Cookie-based authentication
* Protected routes using middleware

### 🎧 Music Management

* Upload music files
* Create albums
* Fetch all songs
* Fetch albums
* Get album details

### ☁️ Media Storage

* Music files uploaded using **Multer**
* Files stored and served via **ImageKit.io CDN**
* Faster media delivery and optimized storage

### 👨‍🎤 Role Based Access

Two types of users:

**Artist**

* Upload music
* Create albums

**User**

* Browse music
* View albums

---

# 🏗️ Project Structure

```
backend
│
├── controllers
│   ├── auth.controller.js
│   └── music.controller.js
│
├── middlewares
│   └── auth.middleware.js
│
├── routes
│   ├── auth.routes.js
│   └── music.routes.js
│
├── config
│   └── imagekit.js
│
├── app.js
├── server.js
├── package.json
└── README.md
```

---

# 🛠️ Tech Stack

* Node.js
* Express.js
* MongoDB
* Mongoose
* JWT Authentication
* Cookie Parser
* Multer (File Upload)
* ImageKit.io (Media Storage & CDN)

---

# ☁️ ImageKit Integration

This project uses **ImageKit.io** to store and deliver music files efficiently.

### Why ImageKit?

* Fast **CDN delivery**
* Secure **file uploads**
* Optimized **media storage**
* Scalable cloud media management

### Example Upload Flow

1. Artist uploads a music file
2. Multer stores file temporarily in memory
3. File is uploaded to **ImageKit**
4. ImageKit returns a **public URL**
5. The URL is stored in the database
6. Users stream music using the ImageKit URL

Example configuration:

```javascript
const ImageKit = require("imagekit");

const imagekit = new ImageKit({
  publicKey: process.env.IMAGEKIT_PUBLIC_KEY,
  privateKey: process.env.IMAGEKIT_PRIVATE_KEY,
  urlEndpoint: process.env.IMAGEKIT_URL_ENDPOINT
});
```

---

# ⚙️ Installation

### 1️⃣ Clone the repository

```bash
git clone https://github.com/yourusername/spotify-backend.git
```

### 2️⃣ Go to project directory

```bash
cd spotify-backend
```

### 3️⃣ Install dependencies

```bash
npm install
```

---

# 🔐 Environment Variables

Create a `.env` file in the root directory.

Example:

```
PORT=5000
MONGO_URI=your_mongodb_connection
JWT_SECRET=your_secret_key

IMAGEKIT_PUBLIC_KEY=your_public_key
IMAGEKIT_PRIVATE_KEY=your_private_key
IMAGEKIT_URL_ENDPOINT=https://ik.imagekit.io/your_id
```

---

# ▶️ Running the Server

```
npm run dev
```

or

```
node server.js
```

Server will start on:

```
http://localhost:5000
```

---

# 🔐 Authentication Routes

Base URL

```
/api/auth
```

### Register User

```
POST /api/auth/register
```

Body

```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "123456"
}
```

---

### Login User

```
POST /api/auth/login
```

Body

```json
{
  "email": "john@example.com",
  "password": "123456"
}
```

---

### Logout User

```
POST /api/auth/logout
```

---

# 🎵 Music Routes

Base URL

```
/api/music
```

---

### Upload Music (Artist Only)

```
POST /api/music/upload
```

Middleware

```
authArtist
```

Form Data

```
music : file
```

Uses **Multer Memory Storage** before uploading to **ImageKit**.

---

### Create Album (Artist Only)

```
POST /api/music/album
```

Middleware

```
authArtist
```

---

### Get All Music

```
GET /api/music
```

Middleware

```
authUser
```

---

### Get All Albums

```
GET /api/music/albums
```

Middleware

```
authUser
```

---

### Get Album By ID

```
GET /api/music/albums/:albumId
```

Middleware

```
authUser
```

Example

```
/api/music/albums/64ab123c9a
```

---

# 🔑 Middleware

### authUser

* Verifies logged-in user
* Protects user routes

### authArtist

* Ensures the user is an **artist**
* Allows uploading music and creating albums

---

# 📦 File Upload (Multer)

Music files are uploaded using **Multer** with memory storage.

```javascript
const multer = require("multer");

const upload = multer({
  storage: multer.memoryStorage()
});
```

---

# 🍪 Cookie Authentication

Authentication uses **cookies** for session management.

```javascript
const cookieParser = require('cookie-parser');
app.use(cookieParser());
```

---

# 📡 API Prefix

Defined inside `app.js`

```javascript
app.use('/api/auth', authRoutes);
app.use('/api/music', musicRoutes);
```

---

# 🧪 Example API Flow

### Step 1

Register user

```
POST /api/auth/register
```

### Step 2

Login

```
POST /api/auth/login
```

### Step 3

Artist uploads music

```
POST /api/music/upload
```

### Step 4

Users fetch music

```
GET /api/music
```

---

# 📈 Future Improvements

* Music streaming support
* Playlists
* Likes and favorites
* Search functionality
* Music recommendation system
* Pagination
* Rate limiting

---

# 🤝 Contributing

Contributions are welcome!

Steps:

```
Fork the repo
Create a new branch
Commit your changes
Submit a pull request
```

---

# 📜 License

This project is licensed under the **MIT License**.

---

# 👨‍💻 Author

Developed by **Yash Gupta**
