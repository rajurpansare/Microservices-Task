# Microservices-Task

## Overview
This document provides details on testing various services after running the `docker-compose` file. These services include User, Product, Order, and Gateway Services. Each service has its own endpoints for testing purposes.

---

## Services and Endpoints

### **User Service**
- **Base URL:** `http://localhost:3000`
- **Endpoints:**
  - **List Users:**  
   
    Output: http://localhost:3000/users
    
<img width="494" height="231" alt="Screenshot 2026-04-25 at 5 02 54 PM" src="https://github.com/user-attachments/assets/46577a40-2e41-4694-9579-b13ed90a3eb6" />


---

### **Product Service**
- **Base URL:** `http://localhost:3001`
- **Endpoints:**
  - **List Products:**
    
    Output: http://localhost:3001/products

<img width="647" height="245" alt="Screenshot 2026-04-25 at 5 09 07 PM" src="https://github.com/user-attachments/assets/cadf327b-4c32-4262-a3b5-2619543eb5ca" />

---

### **Order Service**
- **Base URL:** `http://localhost:3002`
- **Endpoints:**
  - **List Orders:**
    
    Output: http://localhost:3002/orders
<img width="605" height="227" alt="Screenshot 2026-04-25 at 5 14 53 PM" src="https://github.com/user-attachments/assets/b49cfa2f-7843-4ba1-bef8-be7e6dec303e" />


---

### **Gateway Service**
- **Base URL:** `http://localhost:3003/api`
- **Endpoints:**
  - **Users:**  
   
    Output: http://localhost:3003/api/users
    
<img width="604" height="242" alt="Screenshot 2026-04-25 at 5 13 53 PM" src="https://github.com/user-attachments/assets/1b7281ac-56df-4f8a-85be-648036bad1eb" />


  - **Products:**  
   
    Output http://localhost:3003/api/products
   
<img width="639" height="275" alt="Screenshot 2026-04-25 at 5 13 16 PM" src="https://github.com/user-attachments/assets/061813d1-7f1b-4b3b-b7cc-defbfd2877d8" />


  - **Orders:**  
    
    Output: http://localhost:3003/api/orders
  
<img width="595" height="339" alt="Screenshot 2026-04-25 at 5 11 44 PM" src="https://github.com/user-attachments/assets/ee7715e7-dd9a-4d7e-b5fa-bada6be528a5" />

---

## Instructions
1. Start all services using the `docker-compose` file:
   ```
   docker-compose up --build
   ```
<img width="853" height="201" alt="Screenshot 2026-04-25 at 5 19 08 PM" src="https://github.com/user-attachments/assets/eafefc29-86f5-43a8-a3aa-8000dd8d0342" />
   
2. Once the services are running, check the endpoints and the functionality.
    ```
   docker ps
   ```

 <img width="1307" height="89" alt="Screenshot 2026-04-25 at 5 21 29 PM" src="https://github.com/user-attachments/assets/3d80a1f8-5aa9-4884-ab64-3b8b278b9b12" />

 

!! Thank You !!
