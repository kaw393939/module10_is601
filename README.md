# **Module 10: Secure User Accounts, Pydantic Validation, and CI/CD**

## **Module Overview**

In **Module 10**, you will leverage your foundational knowledge of **databases** (from Module 9) and extend it to build a **secure user model** with **SQLAlchemy**, **Pydantic** validation, and an end-to-end **CI/CD pipeline** that pushes your Docker image to **Docker Hub**. Specifically, you will:

1. Create a **User** model that stores **hashed passwords** (no plain text!), enforcing best security practices.  
2. Validate user data using **Pydantic**, ensuring fields (e.g., email) meet required formats and preventing malformed data from reaching the database.  
3. Write and run **unit** and **integration tests** in GitHub Actions, where a **PostgreSQL** container is used for real database interactions.  
4. Finalize a **CI/CD workflow** to build, scan, and deploy your Docker image to Docker Hub, promoting DevOps principles that ensure code quality and security.

By successfully completing Module 10, you will demonstrate mastery of several **Course Learning Outcomes (CLOs)**:

- **CLO 3:** Create Python applications with automated testing.  
- **CLO 4:** Set up GitHub Actions for Continuous Integration (CI), automating tests and Docker builds to demonstrate DevOps principles.  
- **CLO 10:** Apply containerization techniques to containerize applications using Docker.  
- **CLO 12:** Integrate Python programs with SQL databases to create and manipulate data.  
- **CLO 13:** Serialize, deserialize, and validate JSON using Python with Pydantic.  
- **CLO 14:** Utilize best practices for software development security by implementing secure authentication and authorization techniques, including encryption, hashing, and encoding.

---

## **Why Focus on Secure User Models, Validation, and CI/CD?**

1. **Security from the Start:** Handling passwords securely (hashed + salted) and validating inputs (with Pydantic) helps you avoid critical vulnerabilities.  
2. **Seamless Development:** Orchestrating tests (unit, integration) via GitHub Actions ensures code reliability and quickly flags regressions.  
3. **Production Readiness:** By deploying Docker images to Docker Hub, you lay the groundwork for future expansions (Routes in Module 12, UI in Module 13, final project in Module 14).

---

## **Module 10 Videos**

1. **Overview Video (on Canvas)**  
   - Shows how **SQLAlchemy** models and **Pydantic** schemas integrate for secure user data handling.  
   - Explains basic password hashing with a library (e.g., `bcrypt`).  

2. **Hands-On Video (on Canvas)**  
   - Demonstrates writing **unit** and **integration tests** that spin up a **PostgreSQL** service in GitHub Actions.  
   - Explains building a **CI/CD pipeline** that checks for vulnerabilities before pushing to Docker Hub.

---

## **Learning Pathway**

### **Recall**

**Title:** From Raw SQL to an ORM & CI/CD  
**Grading Type:** Points  
**Instructions:**  
1. **Reflect:** How did manually writing SQL in Module 9 inform your approach to database operations? Why might an ORM approach (SQLAlchemy) be more efficient or safer for production?  
2. **Discussion Prompt:**  
   - Why is hashing passwords a mandatory practice in modern web apps?  
   - What benefits do automated tests + Docker deployment offer as your project scales?

**Purpose:** These questions transition you from manual SQL operations to a robust, professionally aligned Python stack with continuous delivery.

---

## **Step-by-Step Guide: Secure User Model & CI/CD**

### **1. Creating a Secure User Model (SQLAlchemy)**

- **Model Fields:** `id`, `username`, `email`, `password_hash`, `created_at`.  
- **Uniqueness Constraints:** Enforce no duplicate usernames or emails.  
- **Hashed Passwords:** Rely on a hashing library (e.g., `bcrypt`) to store a salted hash instead of plain-text passwords.

### **2. Validating Data with Pydantic**

- **UserCreate Schema:**  
  - Includes `username`, `email`, `password` in plain text (for creation only).  
  - Optionally validate minimum password length, email format, etc.  

- **UserRead Schema:**  
  - Exposes only safe fields (e.g., `id`, `username`, `email`, `created_at`), excluding `password_hash`.

### **3. Database Testing in GitHub Actions**

- **Unit Tests:**  
  - Verify password hashing/verification methods (ensure plain text != hashed text).  
  - Check that invalid user data (e.g., duplicate username) is handled gracefully.  
- **Integration Tests:**  
  - Spin up a test **PostgreSQL** container in GitHub Actions.  
  - Insert users, confirm the database rejects invalid inputs, etc.  

### **4. CI/CD Workflow: Build, Scan, Deploy**

- **Test Stage:** Runs all unit/integration tests; fails early on errors.  
- **Security/Scan Stage:** (Optional) uses a scanner to detect high/critical vulnerabilities in your Docker image.  
- **Deploy Stage:** Pushes the final image to **Docker Hub** if prior stages succeed.

---

## **Hands-On Assignment**

**Title:** Secure User Model, Pydantic Validation, Database Testing, and Docker Deployment  
**Grading Type:** Points  

**Instructions:**

1. **Set Up Your SQLAlchemy User Model**  
   - Define columns for `username`, `email`, `password_hash`, ensuring **unique constraints**.  
   - Incorporate a `created_at` timestamp.

2. **Add Pydantic Schemas**  
   - **UserCreate**: For new user data (`username`, `email`, `password`).  
   - **UserRead**: For returning user details (omitting `password_hash`).

3. **Implement Hashing**  
   - Use a function to hash raw passwords before storing them in `password_hash`.  
   - Provide a verify function to confirm a plain-text password matches the stored hash.

4. **Write Unit and Integration Tests**  
   - Unit tests for hashing, schema validation, etc.  
   - Integration tests requiring a real database (Postgres container in GitHub Actions) to test user uniqueness, invalid emails, etc.

5. **Configure CI/CD**  
   - **Test**: Ensure all tests pass in GitHub Actions.  
   - **Deploy**: Push your Docker image to **Docker Hub** upon successful tests.

6. **Submit**  
   - **GitHub Repository Link**: Must include **your own code** (not a copy of the instructor’s repo).  
   - In your **README**, add:  
     - A brief overview of how to run tests locally.  
     - **Links** to your Docker Hub repository (where your image is pushed).  
   - Remember, this is the same project you’ll build upon in future modules, ultimately forming your final project.
# **Grading Expectations**

Your submissions for the **Hands-On Assignment** will be evaluated based on the following two criteria:

### **1. Submission Completeness (50 Points)**

- **GitHub Repository Link:**
  - Provided and accessible.
  - Contains all necessary files (`SQLAlchemy` models, Pydantic schemas, application code, tests, GitHub Actions workflow).

- **Screenshots:**
  - **GitHub Actions Workflow:** Screenshot showing a successful run of the GitHub Actions workflow.
  - **Docker Hub Deployment:** Screenshot demonstrating the Docker image has been successfully pushed to Docker Hub.

- **Documentation:**
  - Includes a reflection document addressing key experiences and challenges faced during the development and deployment process.
  - README file contains instructions on how to run tests locally and links to the Docker Hub repository.

### **2. Functionality of Secure User Model and CI/CD Pipeline (50 Points)**

- **Secure User Model:**
  - SQLAlchemy `User` model correctly implemented with hashed passwords and uniqueness constraints for `username` and `email`.
  - Pydantic schemas (`UserCreate`, `UserRead`) accurately validate and serialize user data.

- **Testing and CI/CD:**
  - Comprehensive unit and integration tests are written and pass successfully in the GitHub Actions workflow.
  - CI/CD pipeline is properly configured to build, scan, and deploy the Docker image to Docker Hub without errors.
  - Docker image is functional and can be pulled from Docker Hub, running the application as expected.

---

**Total: 100 Points**
---

## **Reflect**

**Title:** Module 10 Reflection  
**Grading Type:** Points  
**Instructions:**  
Write **200-300 words** covering:

1. **CLO 3, 4, 10, 12, 13, 14:** Reflect on how each of these CLOs comes into play (testing, CI/CD, containerization, database integration, data validation, security).  
2. **Security & Validation:** What new insights did you gain about hashing passwords and validating user input with Pydantic?  
3. **Challenges & Solutions:** Note any significant hurdles (e.g., Docker Hub authentication, environment variables for tests) and how you resolved them.  


---

## **Quiz**

**Title:** Secure User Model & CI/CD Quiz  
**Grading Type:** Points  

**Instructions:**  
1. **Complete the Quiz on Canvas**, covering topics like:  
   - SQLAlchemy model basics (unique constraints, hashed passwords).  
   - Pydantic validations and error handling.  
   - GitHub Actions test containers (PostgreSQL).  
   - Docker image scanning + deployment to Docker Hub.  

2. **Question Types:**  
   - **Multiple-Choice:** Identify correct usage of hashing or Pydantic validations.  
   - **Short Answer:** Explain how you’d handle a failing test or a duplicate username scenario.  
   - **Scenario-Based:** Propose a fix if your pipeline fails to push an image to Docker Hub or if the Postgres container won’t spin up in CI.

---

## **Tips for Success**

1. **Never Store Plain Passwords:** Only store salted, hashed passwords.  
2. **Validate with Pydantic:** Catch invalid data (e.g., malformed emails, short passwords) early.  
3. **Test Thoroughly:** Combine unit + integration tests to cover all code paths, ensuring your pipeline is robust.  
4. **Automate CI/CD:** A fully automated workflow frees you to focus on feature development while maintaining quality.  
5. **Documentation:** Keep a clear README—this project is your stepping stone for Modules 11–14, culminating in your final project.

---

## **Submission Deadline**

Please submit the following by **[Insert Deadline Here]**:

1. **GitHub Repository Link** (showing your code, tests, and CI config).  
2. **Module 10 Reflection** (200-300 words).  
3. **In your GitHub repo’s README**:  
   - Links to your Docker Hub repository.  
   - Instructions on how to run tests locally.  

Late submissions may be subject to course policy penalties.

---

**Congratulations!** You have taken a significant step toward mastering secure user management, robust validation, comprehensive testing, and automated deployments. This foundation will prove invaluable as you evolve your application in Modules 11–14, leading to a polished **final project**.
