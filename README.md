

---

# 🎬 BookMyShow Backend – API Server

A production-ready backend for a movie ticket booking platform similar to **BookMyShow**.
This project implements core features like movies, theatres, showtimes, seat layout, bookings, payments, and authentication.

---

## 🚀 Tech Stack

### **Backend**

* **Java / Spring Boot**
* **Spring MVC**
* **Spring Data JPA**
* **MySQL / PostgreSQL**
* **JWT Authentication**
* **Lombok**

### **Tools**

* Maven / Gradle
* Postman
* Docker (optional)

---

## ✨ Features

### 🧾 **User & Auth**

* User signup + login
* JWT-based authentication
* Role-based access (Admin / User)

### 🎞️ **Movies & Theatres**

* CRUD for Movies
* CRUD for Theatres
* Search movies by city, date, genre
* Manage screens in each theatre

### ⏱️ **Showtimes**

* Add shows for a movie in a screen
* Show includes:

  * movie
  * start time
  * end time
  * screen
  * base ticket price
  * seat layout map

### 🎟️ **Seats & Bookings**

* Real-time seat selection
* Seat locking (avoid double booking)
* Confirmed booking returned with:

  * Transaction ID
  * Show details
  * Seat numbers
  * Total price

### 💰 **Payments**

* Dummy Payment Simulation
  (easily replaceable with Razorpay/Stripe)

---

## 📂 Project Structure

```
src/main/java/com/bookmyshow
│── controller/
│── service/
│── repository/
│── model/
│── dto/
│── exceptions/
│── security/
```

---

## 🛠️ Setup Instructions

### **1. Clone the repo**

```bash
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>
```

### **2. Configure DB (MySQL example)**

Update `application.properties`:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/bookmyshow
spring.datasource.username=root
spring.datasource.password=yourpassword

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
```

### **3. Install dependencies**

```bash
mvn clean install
```

### **4. Run the server**

```bash
mvn spring-boot:run
```

---

## 📌 API Endpoints (Important)

### **Auth**

| Method | Endpoint         | Description       |
| ------ | ---------------- | ----------------- |
| POST   | `/auth/register` | Register new user |
| POST   | `/auth/login`    | Login + get JWT   |

### **Movies**

| Method | Endpoint        | Description     |
| ------ | --------------- | --------------- |
| POST   | `/admin/movies` | Add movie       |
| GET    | `/movies`       | List all movies |
| GET    | `/movies/{id}`  | Movie details   |

### **Theatres & Screens**

| Method | Endpoint                |
| ------ | ----------------------- |
| POST   | `/admin/theatres`       |
| GET    | `/theatres?city=Nashik` |

### **Shows**

| POST | `/admin/shows` |
| GET | `/shows/movie/{movieId}` |

### **Seat Map**

| GET | `/shows/{showId}/seats` |

### **Bookings**

| POST | `/book` |
| GET | `/bookings/user/{id}` |

---

## 🪄 How Booking Works (Flow)

1. User selects movie + show + seats
2. Backend temporarily **locks seats**
3. Payment → success
4. Ticket confirmed + seats marked booked
5. Booking receipt returned

⚠️ Prevents duplicate booking even under high load.

---

## 🔐 Authentication & Roles

* Every request must include:

```
Authorization: Bearer <JWT_TOKEN>
```

* Admin APIs (add movie/show/theatre) require **ADMIN** role.

---

## 🧪 Postman Collection

Include your exported postman collection here:

```
/postman/BookMyShowAPI.postman_collection.json
```

---

## 🐳 Docker Support (Optional)

```bash
docker build -t bookmyshow-backend .
docker run -p 8080:8080 bookmyshow-backend
```

---

## 🚧 Future Improvements

* Payment Gateway Integration
* Seat Price Variations (Gold/Silver/Platinum)
* Notifications (Email/SMS)
* Load balancing + Redis seat lock
* Admin UI panel

---

## 🤝 Contributing

Pull requests welcome! For major changes, open an issue first to discuss.

---

## 📜 License

MIT License.


