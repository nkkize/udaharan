## HSTS
HSTS stands for HTTP strict transport porotcol.
1. its a web security policy mechanism
2. it helps to protect websites against the protocol downgrade attacks and cookies hijacking.
3. It allows web servers to declare that web browsers should interact with it using only secure HTTPS connection only.
4. This policy is communicated by the server to the user agent via an HTTPS response header field - `Strict-Transport-Security`.

### 'Strict-Transport-Security' HTTPS resposne Header:
1. this header specifies a period of time during which the user agent should only accesss the server in a secure fashion. It specifies the max-age in seconds.
`Strict-Transport-Security: max-age=31536000`
2. once a site uses this HEADER:
   1. it doesn't connect over HTTP or redirect users to HTTPS.
   2. it never accept the clear text HTTP.
   3. A user-agent not capable of doing TLS will not be able to connnect to the site anymore.
   4. The user-agent modifies the HTTP link into HTTPS links.
   5. If the server's TLS certificate can not be trusted. The user-agent terminates the connection.
   6. Limitation: The initial request to the server, and the request after the expiry of the max-age specified by the `Strict-transport-Security` header remain unprotected.
   7. With HSTS, we can tag the visiting browsers which has privacy concerns.

### Best Practices:
1. HSTS hosts should declare HSTS policy at their top-level domain name. The header should specify the includeSubDomains directive.

### How to enable HTTP Strict Transport Security (HSTS) for your site
#### In Linux:
   1. Go to your project root folder.
   2. create/update the following file `.htacess`.
   3. Add following content in the file and save it.
   ```sh Header set Strict-Transport-Security "max-age=31536000" env=HTTPS```
