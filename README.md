# 🏠 Home Harbor – Real Estate Website

Home Harbor is a PHP-based real estate website that allows users to browse property listings, view property details, and contact sellers.  
It is designed for ease of use with a clean, responsive interface that works on all devices.

---

## ✨ Features

- Browse properties with images and descriptions
- Search and filter properties
- View detailed property information
- Contact property sellers
- Responsive and user-friendly design

---

## 🛠 Tech Stack

- **Frontend:** HTML, CSS, JavaScript
- **Backend:** PHP
- **Database:** MySQL (phpMyAdmin)

---

## 🚀 Installation & Setup

### 1. Clone the Repository

```bash
git clone https://github.com/Ritika5703/home-harbor-real-estate.git
cd home-harbor-real-estate
```

### 2. Move to Server Directory

- Place the project folder inside your XAMPP `htdocs` or WAMP `www` directory.

---

## 🗄️ Database Setup (phpMyAdmin — step by step, no SQL file)

### 0) Prerequisites

- Install **XAMPP/WAMP/MAMP** and start **Apache** + **MySQL**.
- Open **phpMyAdmin** at `http://localhost/phpmyadmin`.

---

### 1) Create the database

1. In phpMyAdmin left sidebar, click **New**.
2. **Database name:** `home_harbor` (or any other name).
3. **Collation:** `utf8mb4_general_ci`.
4. Click **Create**.

---

### 2) Create tables (UI only)

> Tip: In phpMyAdmin, click your DB (`home_harbor`) → **Structure** → **Create table**.
> Set **Primary** keys and **A_I** (Auto Increment) where stated.

#### 2.1 `about`

- `id` – INT(10), Primary, A_I
- `title` – VARCHAR(100), NOT NULL
- `content` – LONGTEXT, NOT NULL
- `image` – VARCHAR(300), NOT NULL

#### 2.2 `admin`

- `aid` – INT(10), Primary, A_I
- `auser` – VARCHAR(50), NOT NULL
- `aemail` – VARCHAR(50), NOT NULL
- `apass` – VARCHAR(255), NOT NULL
- `adob` – DATE, NOT NULL
- `aphone` – VARCHAR(15), NOT NULL

#### 2.3 `state`

- `sid` – INT(50), Primary, A_I
- `sname` – VARCHAR(100), NOT NULL

#### 2.4 `city`

- `cid` – INT(50), Primary, A_I
- `cname` – VARCHAR(100), NOT NULL
- `sid` – INT(50), NOT NULL

#### 2.5 `user`

- `uid` – INT(50), Primary, A_I
- `uname` – VARCHAR(100), NOT NULL
- `uemail` – VARCHAR(100), NOT NULL
- `uphone` – VARCHAR(20), NOT NULL
- `upass` – VARCHAR(255), NOT NULL
- `utype` – VARCHAR(50), NOT NULL
- `uimage` – VARCHAR(300), NULL

#### 2.6 `property`

| Field Name  | Type          | Description                                  |
| ----------- | ------------- | -------------------------------------------- |
| id          | INT (PK)      | Unique property ID (auto-increment)          |
| title       | VARCHAR(255)  | Property title                               |
| description | TEXT          | Detailed description of the property         |
| price       | DECIMAL(10,2) | Property price                               |
| location    | VARCHAR(255)  | City/area where the property is located      |
| type        | VARCHAR(50)   | Property type (e.g., Apartment, House, Land) |
| bedrooms    | INT           | Number of bedrooms                           |
| bathrooms   | INT           | Number of bathrooms                          |
| size        | INT           | Area in square feet or meters                |
| image       | VARCHAR(255)  | Path or URL to the property’s main image     |
| created\_at | DATETIME      | Record creation timestamp                    |
| updated\_at | DATETIME      | Last update timestamp                        |


#### 2.7 `contact`

- `cid` – INT(50), Primary, A_I
- `name` – VARCHAR(100), NOT NULL
- `email` – VARCHAR(100), NOT NULL
- `phone` – VARCHAR(20), NOT NULL
- `subject` – VARCHAR(100), NOT NULL
- `message` – VARCHAR(250), NOT NULL

#### 2.8 `feedback`

- `fid` – INT(50), Primary, A_I
- `uid` – INT(50), NOT NULL
- `fdescription` – VARCHAR(300), NOT NULL
- `status` – TINYINT(1), NOT NULL DEFAULT 0
- `date` – DATE, DEFAULT CURRENT_TIMESTAMP

---

### 3) Add foreign keys (optional but recommended)

- `city.sid` → `state.sid`
- `property.uid` → `user.uid`
- `feedback.uid` → `user.uid`

---

### 4) Create a dedicated MySQL user

1. phpMyAdmin → **User accounts** → **Add user account**.
2. Username: `home_harbor_user`
3. Host: `localhost`
4. Password: strong password
5. Grant all privileges on `home_harbor` database.

---

### 5) Create your local `config.php` (do NOT commit)

```php
<?php

$con = mysqli_connect("localhost","root","","home_harbor");
	if (mysqli_connect_errno())
	{
		echo "Failed to connect to MySQL: " . mysqli_connect_error();
	}
?>
```

**.gitignore**

```
config.php
.env
*.sql
```

---

### 6) Add your first admin/user safely

- Go to `user` table → **Insert**.
- Hash your password using:

```php
<?php echo password_hash('YourPassword123', PASSWORD_DEFAULT);
```

- Use that hash in `upass`.

---

### 7) Seed basic data (optional)

- Add states, cities, and at least one property linked to a user.

---

## 💻 Running the Project in Browser

1. Start **Apache** and **MySQL** from XAMPP/WAMP.
2. Place this project folder in `htdocs` (XAMPP) or `www` (WAMP).
3. In your browser, open:

```
http://localhost/home-harbor-real-estate
```

4. You should see the homepage.
5. If you encounter a blank page or errors, check `config.php` database settings.

---

## 🔑 Accessing the Admin Dashboard

- Open:

```
http://localhost/home-harbor-real-estate/admin
```

- Log in with your **admin** credentials from the `admin` table in the database.
- If no admin exists:
  1. Insert a record into the `admin` table via phpMyAdmin or register.
  2. Use those credentials on the login page.

---
