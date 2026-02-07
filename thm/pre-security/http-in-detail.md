# Pre-Security / HTTP in Detail

## HTTP & URLs
**HTTP (HyperText Transfer Protocol)** is a set of rules used to communicate with web servers and transmit web content (HTML, images, video, etc.).

**URL (Uniform Resource Locator)** general form:
`scheme://userinfo@host:port/path?query#fragment`

- **Scheme**: protocol used to access the resource (e.g., HTTP, HTTPS, FTP).
- **Userinfo**: optional `username:password` (rare and generally discouraged today).
- **Host**: domain name or IP address of the server.
- **Port**: where to connect (commonly 80 for HTTP, 443 for HTTPS, but can be 1–65535).
- **Path**: location of the resource on the server (e.g., `/index.html`, `/blog/1`).
- **Query string**: extra parameters sent to the path (e.g., `/blog?id=1`).
- **Fragment**: points to a section on the page (handled by the browser; typically not sent to the server).

---

## HTTP Request (structure)
A request consists of:
1) **Request line**: `METHOD /path HTTP/1.1`
2) **Headers** (key/value pairs)
3) **Blank line** (end of headers)
4) **Optional body** (common with POST/PUT)

Example (high-level):
- Line 1: method + path + HTTP version
- `Host`: which site you want (important when one server hosts multiple sites)
- `User-Agent`: client info (browser/app)
- `Referer`: the previous page (optional)
- blank line: end of headers

---

## HTTP Response (structure)
A response consists of:
1) **Status line**: `HTTP/1.1 STATUS_CODE STATUS_TEXT`
2) **Headers**
3) **Blank line** (end of headers)
4) **Body** (the requested content)

Common response headers:
- `Server`: server software (often present, sometimes hidden)
- `Date`: server time for the response
- `Content-Type`: what kind of data is sent (HTML, JSON, images, etc.)
- `Content-Length`: size of the response body in bytes (not always present)
- `Content-Encoding`: compression used (gzip, br, etc.)

---

## Methods
- **GET**: retrieve data from a web server (usually no body).
- **POST**: submit data (often used to create resources or perform actions).
- **PUT**: create/replace a resource (or update it depending on API design).
- **DELETE**: remove a resource.

---

## Status Codes (overview)
- **1xx**: Informational
- **2xx**: Success (e.g., 200 OK)
- **3xx**: Redirection (e.g., 301/302)
- **4xx**: Client errors (e.g., 400, 401, 403, 404)
- **5xx**: Server errors (e.g., 500)

Key ones:
- **200** OK
- **301/302** Redirect
- **400** Bad Request
- **401** Unauthorized (authentication required/failed)
- **403** Forbidden (authenticated or not, but access denied)
- **404** Not Found
- **500** Internal Server Error

---

## Cookies & Sessions
**Cookies** are small pieces of data stored by the browser.
Servers send cookies using the `Set-Cookie` header, and the browser returns them in the `Cookie` header on subsequent requests.

Because HTTP is stateless, cookies help the server recognize the client (e.g., login state, preferences).

**Sessions** are typically stored server-side. The browser usually holds only a **session identifier** (token) in a cookie.

Important cookie flags:
- **HttpOnly**: reduces access from client-side scripts
- **Secure**: only sent over HTTPS
- **SameSite**: helps mitigate cross-site request abuse

---

## Common Headers
- **Host**: selects the target website on a shared server
- **User-Agent**: identifies the client
- **Content-Type**: type of data being sent (request/response)
- **Content-Length**: size of request/response body (bytes)
- **Authorization**: credentials/token for protected resources
- **Cookie**: data sent from browser to server
- **Set-Cookie**: instructs browser to store cookie data
- **Content-Encoding**: compression used for the body
- **Referer**: previous page (optional; spelling is intentionally "Referer")

---

## What commonly ends up in logs (Blue Team view)
(Depends on server/app, but often includes:)
- source IP (or `X-Forwarded-For` if behind proxies)
- method + path (route)
- status code
- user-agent
- response size / latency (if enabled)
- referrer (sometimes)
