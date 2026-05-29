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

<img width="1140" height="600" alt="image" src="https://github.com/user-attachments/assets/e4526530-d291-4d88-b168-93c41002725e" />


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

---

## **HTTP Responses**

- **HTTP Response** – Sent by the server to indicate success, failure, or additional action needed.
- **Status Line** – Contains:
  - **HTTP Version**
  - **Status Code** (numeric outcome)
  - **Reason Phrase** (short explanation)

### **Status Code Categories**
- **100–199: Informational** – Request received, continue.
- **200–299: Success** – Request processed correctly.
- **300–399: Redirection** – Resource moved; follow new location.
- **400–499: Client Errors** – Bad request, missing data, unauthorised, etc.
- **500–599: Server Errors** – Server failed to process the request.

### **Common Status Codes**
- **100 – Continue** – Server ready for the rest of the request.
- **200 – OK** – Request succeeded.
- **301 – Moved Permanently** – Resource now lives at a new URL.
- **404 – Not Found** – Resource doesn’t exist at the given path.
- **500 – Internal Server Error** – Server encountered an unexpected issue.

---

## TryHackMe Quiz

**What part of an HTTP response contains version, status code, and reason phrase?**  
- **Status Line**

**Which category indicates the server encountered an internal issue?**  
- **Server Error Responses**

**Which status code means the resource could not be found?**  
- **404**

---

## **HTTP Response Headers & Response Body**

<img width="1140" height="700" alt="image" src="https://github.com/user-attachments/assets/b2cdf935-4d01-4291-93d5-4bfd96eed29d" />

### **Response Headers**
Key–value pairs sent by the server to give the client instructions about how to handle the response.

### **Required Response Headers**
- **Date** – When the server generated the response.
- **Content-Type** – Format of the returned data (HTML, JSON, etc.) + character set.
- **Server** – Server software handling the request (often removed to avoid leaking info).

### **Other Common Response Headers**
- **Set-Cookie** – Sends cookies to the client.  
  - Use **Secure** (HTTPS only)  
  - Use **HttpOnly** (not accessible via JavaScript)
- **Cache-Control** – Controls caching behaviour (e.g., `max-age`, `no-cache`).
- **Location** – Used in redirects (3xx) to tell the client where to go next.

### **Response Body**
- Contains the actual returned data (HTML, JSON, images, etc.).
- Must be sanitised/escaped to prevent XSS and other injection attacks.

---

## TryHackMe Quiz

**Which response header can reveal server software and version?**  
- **Server**

**Which cookie flag ensures cookies are only sent over HTTPS?**  
- **Secure**

**Which cookie flag prevents JavaScript from accessing cookies?**  
- **HttpOnly**

