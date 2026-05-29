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

### **HTTP Requests**

- **HTTP Request** – Sent by the client to interact with a web app (first point of contact).
- **Request Line** – Contains: **METHOD /path HTTP/version**.
- **URL Path** – Identifies the specific resource or endpoint.
- **HTTP Version** – Defines protocol features (1.1 is still the most widely used).

### **Common HTTP Methods**
- **GET** – Retrieve data. Avoid exposing sensitive info.
- **POST** – Send data. Validate inputs to prevent SQLi/XSS.
- **PUT** – Replace/update resources. Requires strict authorisation.
- **DELETE** – Remove resources. Must be restricted to authorised users.
- **PATCH** – Partial updates. Validate to avoid inconsistent data.
- **HEAD** – Same as GET but returns headers only.
- **OPTIONS** – Shows allowed methods for a resource.
- **TRACE** – Debugging; often disabled for security.
- **CONNECT** – Creates secure tunnels (e.g., HTTPS).

### **Security Notes**
- Validate and sanitise URL paths.
- Prevent unauthorised access to sensitive endpoints.
- Avoid exposing sensitive data in GET requests.
- Disable unnecessary methods (TRACE/OPTIONS) when not needed.

## TryHackMe Quiz

**Which HTTP protocol version became widely adopted and remains the most commonly used?**  
- **HTTP/1.1**

**Which HTTP method shows communication options for a resource?**  
- **OPTIONS**

**Which component specifies the resource/endpoint after the domain?**  
- **URL Path**

---
### **Request Headers & Request Body**

### **Common Request Headers**
- **Host** – Specifies the domain the request is sent to.
- **User-Agent** – Identifies the browser or client making the request.
- **Referer** – Shows the page the request originated from.
- **Cookie** – Stores server‑assigned data (sessions, preferences, etc.).
- **Content-Type** – Describes the format of data in the request body.

---

### **Request Body Formats**
Used in methods like **POST** and **PUT** when sending data to the server.

- **URL Encoded** – `key=value` pairs separated by `&`. Default for HTML forms.
- **Form Data (multipart/form-data)** – Supports multiple data blocks; used for file uploads.
- **JSON (application/json)** – Name/value pairs in JSON structure.
- **XML (application/xml)** – Data wrapped in nested tags.

---

### TryHackMe Quiz

**Which header specifies the domain name of the web server?**  
- **Host**

**Default content type for key=value form submissions?**  
- **application/x-www-form-urlencoded**

**Which part of an HTTP request contains info like host, user agent, and content type?**  
- **Request Headers**

