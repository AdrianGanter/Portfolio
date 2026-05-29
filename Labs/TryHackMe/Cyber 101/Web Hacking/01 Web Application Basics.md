## Web Application Basics

### **Front End (What the user sees)**
- **HTML** – Page structure (the “planet surface”).
- **CSS** – Visual design: colours, layout, style (makes the planet vibrant).
- **JavaScript** – Logic + interactivity (the “brain” reacting to user actions).

### **Back End (What the user doesn’t see)**
- **Database** – Stores and retrieves data (like maps, libraries, resources).
- **Infrastructure** – Servers, networks, storage (roads, cars, fuel running the system).
- **WAF** – Security layer protecting the app (like an atmosphere blocking harmful rays).

---

### **Anatomy of a URL (Short Summary)**
- **Scheme** – Protocol used (HTTP/HTTPS). HTTPS encrypts and is the secure default.
- **User** – Optional login info in the URL (rare today due to security risks).
- **Host/Domain** – Identifies the website. Watch for fake look‑alike domains (typosquatting).
- **Port** – Directs traffic to the correct service (80 = HTTP, 443 = HTTPS).
- **Path** – Points to a specific page or file on the server.
- **Query String** – Starts with `?`; used for searches or form data. Must be validated to prevent injection attacks.
- **Fragment** – Starts with `#`; jumps to a section on the page. Also needs sanitising to avoid injection issues.


<img width="1140" height="270" alt="image" src="https://github.com/user-attachments/assets/bc310b4d-52de-47ab-b152-3bdf50776cbe" />


### TryHackMe Quiz

**Which protocol provides encrypted communication between a browser and a web server?**  
- **HTTPS**

**What term describes registering misspelled versions of popular domains for malicious use?**  
- **Typosquatting**

**What part of a URL passes extra info like search terms or form inputs to the server?**  
- **Query String**

---

### **HTTP Messages**

- **HTTP Messages** = Data exchanged between client and server (requests + responses).
- **Two Types:**
  - **HTTP Request** – Sent by the client to perform an action.
  - **HTTP Response** – Sent by the server with the result.

### **Message Structure**
- **Start Line** – Identifies the message type and how it should be handled.
- **Headers** – Key–value pairs with extra info (security, content type, instructions).
- **Empty Line** – Separates headers from the body.
- **Body** – Actual data (form inputs in requests, webpage/API data in responses).

### **Why It Matters**
- Core of how web apps communicate.
- Helps diagnose web issues and improve reliability.
- Critical for security: understanding structure helps protect data in transit.

