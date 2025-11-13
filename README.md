## 🚀 Mongoose-Crud-ClassWork: Express.js & MongoDB CRUD

This is an **Express.js and Mongoose backend application** that implements full **CRUD** functionality for `User` and `Post` entities using a MongoDB database.

---

### ⚙️ Stack and Structure

| Component | Technology | Description |
| :--- | :--- | :--- |
| **Framework** | Express.js | Handles routing and middleware. |
| **Database** | MongoDB | Primary NoSQL data store. |
| **ORM** | Mongoose | Object Data Modeling (ODM) layer for Node.js and MongoDB. |
| **Architecture** | MVC-like | Separated into `/routes`, `/controllers`, and `/models`. |
| **Configuration** | MongoDB connection | Set up in `/models/index.js`, using settings from `/configs/mongoDb.json`. |

---

### 🗃️ Models and Validation

| Model | Schema and Validation | Relationship (Ref) |
| :--- | :--- | :--- |
| **User** | Built-in Mongoose validators (`required`, `min`/`max`) + **yup** for email validation. | Parent (One side) |
| **Post** | `body` (text), timestamps. | `userId` with `ref: 'User'` (1:n Relationship). |

---

### 🔗 Key Operations and Relationships

| Operation | API Path | Mongoose Method | SQL Equivalent |
| :--- | :--- | :--- | :--- |
| **User CRUD** | `/api/users/:userId` | `create`, `findById`, `findByIdAndUpdate`, `findByIdAndDelete`. | Basic DML (`INSERT`, `SELECT`, `UPDATE`, `DELETE`). |
| **Pagination** | `/api/users?page=...` | `find().sort().skip().limit()`. | `ORDER BY`, `OFFSET`, `LIMIT`. |
| **Create Post** | `/api/users/:userId/posts` | `Post.create()`. | `INSERT` with `FOREIGN KEY`. |
| **Posts with User** | `/api/posts` | `Post.find().**populate('userId')**`. | `LEFT JOIN`. |
| **User's Posts** | `/api/users/:userId/posts` | `User.aggregate().**$lookup**`. | `JOIN` via Aggregation Pipeline. |

---

### 🛑 Error Handling

* **Standardization**: `http-errors` is used to create standardized HTTP errors (e.g., **404 Not Found**, **422 Unprocessable Entity**).
* **Centralized Middleware**: A centralized error handler (`middleware/errorHandlers.js`) intercepts errors and returns standardized JSON responses.
