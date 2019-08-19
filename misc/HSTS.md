## HSTS
HSTS stands for HTTP strict transport porotcol.
1. its a web security policy mechanism
2. it helps to protext websites against the protocol downgrade attacks and cookies hijacking.
3. It allows web serviers to declare that web browsers shouls interact with it using only secure HTTPS connecton only.
4. This policy is communicated by the server to the user agent via an HTTPS response header field - 'Strict-Transport-Security'.

### 'Strict-Transport-Security' HTTPS resposne Header:
1. this header specifies a period of time during which the user agent should only accesss the server in a secure fashion. It specifies the max-age in seconds.
`Strict-Transport-Security: max-age=31536000`
2. once a site uses this HEADER:
   1. it doesn't connect over HTTP or redirect users to HTTPS.
   2. it never accept the clear text HTTP.
   3. A user-agent not capable of doing TLS will not be able to connnect to the site anymore.
