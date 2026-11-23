- What information can HTTP response headers reveal about a web server and its underlying technologies?
```
> curl -I https://vu.lt
HTTP/1.1 301 Moved Permanently
Date: Mon, 23 Nov 2026 17:14:06 GMT
Server: Apache
Location: https://www.vu.lt/
Content-Type: text/html; charset=iso-8859-1
```

It reveals fields such as `Server`, `Content-Type`, `Set-Cookie`. This can suggest frameworks, content format and session handling, but it doesn't reveal anything substantial.

- How can you determine whether a website redirects HTTP requests to HTTPS?
```
> curl -I http://vu.lt
HTTP/1.1 301 Moved Permanently
Date: Mon, 23 Nov 2026 17:16:55 GMT
Server: Apache
Location: https://vu.lt/
Content-Type: text/html; charset=iso-8859-1
```

Response returned `301 Moved Permanently` with `Location: https://vu.lt/` which suggests that HTTP redirects to HTTPS

- Can different HTTP request methods produce different responses for the same resource?
```
> curl -I https://vu.lt
HTTP/1.1 301 Moved Permanently
Date: Mon, 23 Nov 2026 17:26:00 GMT
Server: Apache
Location: https://www.vu.lt/
Content-Type: text/html; charset=iso-8859-1

> curl -i -X OPTIONS https://vu.lt
HTTP/1.1 301 Moved Permanently
Date: Mon, 23 Nov 2026 17:26:23 GMT
Server: Apache
Location: https://www.vu.lt/
Content-Length: 226
Content-Type: text/html; charset=iso-8859-1

<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>301 Moved Permanently</title>
</head><body>
<h1>Moved Permanently</h1>
<p>The document has moved <a href="https://www.vu.lt/">here</a>.</p>
</body></html>
```

Yes, first request sends HEAD, second sends OPTIONS. In this case server accepts both, but a server might accept one, but reject the other.

- What can redirect chains reveal about a website's structure and configuration?
```
> curl -I https://vu.lt
HTTP/1.1 301 Moved Permanently
Date: Mon, 23 Nov 2026 17:28:22 GMT
Server: Apache
Location: https://www.vu.lt/
Content-Type: text/html; charset=iso-8859-1

> curl -I https://www.vu.lt/
HTTP/1.1 200 OK
Date: Mon, 23 Nov 2026 17:28:38 GMT
Server: Apache
Cache-Control: private, no-cache, no-store, max-age=0, must-revalidate
Content-Security-Policy: default-src 'self'; base-uri 'self'; object-src 'none'; frame-ancestors 'self'; form-action 'self' https://www.facebook.com https://static.mailerlite.com; script-src 'self' 'unsafe-inline' 'unsafe-eval' https://www.googletagmanager.com https://www.google.com https://www.gstatic.com https://cse.google.com https://www.youtube.com https://code.jquery.com https://cdn.cookielaw.org https://consent.cookiebot.com https://consentcdn.cookiebot.com https://static.hotjar.com https://script.hotjar.com https://connect.facebook.net https://track.adform.net https://s2.adform.net https://static.mailerlite.com https://app.mailerlite.com https://assets.mlcdn.com https://sc-static.net https://tr.snapchat.com https://googleads.g.doubleclick.net https://partner.googleadservices.com https://ep2.adtrafficquality.google; script-src-attr 'none'; style-src 'self' 'unsafe-inline' https://www.google.com https://fonts.googleapis.com https://cdn.cookielaw.org https://static.mailerlite.com https://assets.mlcdn.com https://fonts.mailerlite.com; img-src 'self' data: blob: https:; font-src 'self' data: https://fonts.gstatic.com https://fonts.mailerlite.com https://assets.mlcdn.com; connect-src 'self' https://www.googletagmanager.com https://www.google.com https://www.gstatic.com https://syndicatedsearch.goog https://n8n.itpc.vu.lt https://sentry.dc.vu.lt https://cdn.cookielaw.org https://geolocation.onetrust.com https://cookies-data.onetrust.io https://consent.cookiebot.com https://consentcdn.cookiebot.com https://*.hotjar.com https://*.hotjar.io wss://*.hotjar.com https://connect.facebook.net https://www.facebook.com https://*.on.aws https://*.run.app https://*.adform.net https://static.mailerlite.com https://*.snapchat.com https://*.google-analytics.com https://*.analytics.google.com https://*.doubleclick.net https://pagead2.googlesyndication.com https://*.adtrafficquality.google https://www.googleadservices.com; frame-src 'self' https://www.youtube.com https://forms.office.com https://forms.cloud.microsoft https://login.microsoftonline.com https://app.powerbi.com https://www.instagram.com https://*.issuu.com https://www.google.com https://www.googletagmanager.com https://syndicatedsearch.goog https://consentcdn.cookiebot.com https://www.facebook.com https://*.snapchat.com https://*.adtrafficquality.google; media-src 'self' data:; worker-src 'self' blob:; manifest-src 'self'; upgrade-insecure-requests
Content-Type: text/html; charset=utf-8
Cross-Origin-Opener-Policy: same-origin
Link: </_next/static/media/4b825e536f0add60-s.p.15vlspr5uap8d.woff2>; rel=preload; as="font"; crossorigin=""; type="font/woff2", </_next/static/chunks/2zt7i03rte-ja.css>; rel=preload; as="style", </_next/static/chunks/0z_yao-k8wanr.css>; rel=preload; as="style", </_next/static/chunks/3qq6pvwsw--ki.css>; rel=preload; as="style"
Permissions-Policy: camera=(), microphone=(), geolocation=(), payment=(), usb=()
Referrer-Policy: strict-origin-when-cross-origin
Strict-Transport-Security: max-age=31536000
Vary: rsc,next-router-state-tree,next-router-prefetch,next-router-segment-prefetch,Accept-Encoding
X-Content-Type-Options: nosniff
X-Current-Path: /
X-Frame-Options: SAMEORIGIN
X-Locale: lt
X-Middleware-Rewrite: /lt
X-Request-Path: /
Set-Cookie: language=lt; Path=/; Expires=Tue, 23 Nov 2027 17:28:38 GMT; Max-Age=31536000; Secure; SameSite=lax
Set-Cookie: ROUTEID=.route1; path=/
```

Redirects help us see website preferences. For example:
`http://vu.lt/` --switch to HTTPS--> `https://vu.lt` --switch to preferred hostname--> `https://www.vu.lt/`

- How might changing request headers affect the server's response?
```
> curl -I -H "Accept-Language: en" https://www.vu.lt
HTTP/1.1 307 Temporary Redirect
Date: Mon, 23 Nov 2026 17:33:48 GMT
Server: Apache
Cache-Control: private, no-store
Content-Security-Policy: default-src 'self'; base-uri 'self'; object-src 'none'; frame-ancestors 'self'; form-action 'self' https://www.facebook.com https://static.mailerlite.com; script-src 'self' 'unsafe-inline' 'unsafe-eval' https://www.googletagmanager.com https://www.google.com https://www.gstatic.com https://cse.google.com https://www.youtube.com https://code.jquery.com https://cdn.cookielaw.org https://consent.cookiebot.com https://consentcdn.cookiebot.com https://static.hotjar.com https://script.hotjar.com https://connect.facebook.net https://track.adform.net https://s2.adform.net https://static.mailerlite.com https://app.mailerlite.com https://assets.mlcdn.com https://sc-static.net https://tr.snapchat.com https://googleads.g.doubleclick.net https://partner.googleadservices.com https://ep2.adtrafficquality.google; script-src-attr 'none'; style-src 'self' 'unsafe-inline' https://www.google.com https://fonts.googleapis.com https://cdn.cookielaw.org https://static.mailerlite.com https://assets.mlcdn.com https://fonts.mailerlite.com; img-src 'self' data: blob: https:; font-src 'self' data: https://fonts.gstatic.com https://fonts.mailerlite.com https://assets.mlcdn.com; connect-src 'self' https://www.googletagmanager.com https://www.google.com https://www.gstatic.com https://syndicatedsearch.goog https://n8n.itpc.vu.lt https://sentry.dc.vu.lt https://cdn.cookielaw.org https://geolocation.onetrust.com https://cookies-data.onetrust.io https://consent.cookiebot.com https://consentcdn.cookiebot.com https://*.hotjar.com https://*.hotjar.io wss://*.hotjar.com https://connect.facebook.net https://www.facebook.com https://*.on.aws https://*.run.app https://*.adform.net https://static.mailerlite.com https://*.snapchat.com https://*.google-analytics.com https://*.analytics.google.com https://*.doubleclick.net https://pagead2.googlesyndication.com https://*.adtrafficquality.google https://www.googleadservices.com; frame-src 'self' https://www.youtube.com https://forms.office.com https://forms.cloud.microsoft https://login.microsoftonline.com https://app.powerbi.com https://www.instagram.com https://*.issuu.com https://www.google.com https://www.googletagmanager.com https://syndicatedsearch.goog https://consentcdn.cookiebot.com https://www.facebook.com https://*.snapchat.com https://*.adtrafficquality.google; media-src 'self' data:; worker-src 'self' blob:; manifest-src 'self'; upgrade-insecure-requests
Cross-Origin-Opener-Policy: same-origin
Location: /en
Permissions-Policy: camera=(), microphone=(), geolocation=(), payment=(), usb=()
Referrer-Policy: strict-origin-when-cross-origin
Strict-Transport-Security: max-age=31536000
X-Content-Type-Options: nosniff
X-Frame-Options: SAMEORIGIN
Set-Cookie: language=en; Path=/; Expires=Tue, 23 Nov 2027 17:33:48 GMT; Max-Age=31536000; Secure; SameSite=lax
Set-Cookie: ROUTEID=.route1; path=/

> curl -I -H "Accept-Language: lt" https://www.vu.lt.lt
HTTP/1.1 200 OK
Date: Mon, 23 Nov 2026 17:36:37 GMT
Server: Apache
Cache-Control: private, no-cache, no-store, max-age=0, must-revalidate
Content-Security-Policy: default-src 'self'; base-uri 'self'; object-src 'none'; frame-ancestors 'self'; form-action 'self' https://www.facebook.com https://static.mailerlite.com; script-src 'self' 'unsafe-inline' 'unsafe-eval' https://www.googletagmanager.com https://www.google.com https://www.gstatic.com https://cse.google.com https://www.youtube.com https://code.jquery.com https://cdn.cookielaw.org https://consent.cookiebot.com https://consentcdn.cookiebot.com https://static.hotjar.com https://script.hotjar.com https://connect.facebook.net https://track.adform.net https://s2.adform.net https://static.mailerlite.com https://app.mailerlite.com https://assets.mlcdn.com https://sc-static.net https://tr.snapchat.com https://googleads.g.doubleclick.net https://partner.googleadservices.com https://ep2.adtrafficquality.google; script-src-attr 'none'; style-src 'self' 'unsafe-inline' https://www.google.com https://fonts.googleapis.com https://cdn.cookielaw.org https://static.mailerlite.com https://assets.mlcdn.com https://fonts.mailerlite.com; img-src 'self' data: blob: https:; font-src 'self' data: https://fonts.gstatic.com https://fonts.mailerlite.com https://assets.mlcdn.com; connect-src 'self' https://www.googletagmanager.com https://www.google.com https://www.gstatic.com https://syndicatedsearch.goog https://n8n.itpc.vu.lt https://sentry.dc.vu.lt https://cdn.cookielaw.org https://geolocation.onetrust.com https://cookies-data.onetrust.io https://consent.cookiebot.com https://consentcdn.cookiebot.com https://*.hotjar.com https://*.hotjar.io wss://*.hotjar.com https://connect.facebook.net https://www.facebook.com https://*.on.aws https://*.run.app https://*.adform.net https://static.mailerlite.com https://*.snapchat.com https://*.google-analytics.com https://*.analytics.google.com https://*.doubleclick.net https://pagead2.googlesyndication.com https://*.adtrafficquality.google https://www.googleadservices.com; frame-src 'self' https://www.youtube.com https://forms.office.com https://forms.cloud.microsoft https://login.microsoftonline.com https://app.powerbi.com https://www.instagram.com https://*.issuu.com https://www.google.com https://www.googletagmanager.com https://syndicatedsearch.goog https://consentcdn.cookiebot.com https://www.facebook.com https://*.snapchat.com https://*.adtrafficquality.google; media-src 'self' data:; worker-src 'self' blob:; manifest-src 'self'; upgrade-insecure-requests
Content-Type: text/html; charset=utf-8
Cross-Origin-Opener-Policy: same-origin
Link: </_next/static/media/4b825e536f0add60-s.p.15vlspr5uap8d.woff2>; rel=preload; as="font"; crossorigin=""; type="font/woff2", </_next/static/chunks/2zt7i03rte-ja.css>; rel=preload; as="style", </_next/static/chunks/0z_yao-k8wanr.css>; rel=preload; as="style", </_next/static/chunks/3qq6pvwsw--ki.css>; rel=preload; as="style"
Permissions-Policy: camera=(), microphone=(), geolocation=(), payment=(), usb=()
Referrer-Policy: strict-origin-when-cross-origin
Strict-Transport-Security: max-age=31536000
Vary: rsc,next-router-state-tree,next-router-prefetch,next-router-segment-prefetch,Accept-Encoding
X-Content-Type-Options: nosniff
X-Current-Path: /
X-Frame-Options: SAMEORIGIN
X-Locale: lt
X-Middleware-Rewrite: /lt
X-Request-Path: /
Set-Cookie: language=lt; Path=/; Expires=Tue, 23 Nov 2027 17:36:37 GMT; Max-Age=31536000; Secure; SameSite=lax
Set-Cookie: ROUTEID=.route1; path=/
```

Sending `Accept-Language: en` to `https://www.vu.lt` produced a temporary redirect to `/en` and set a language preference cookie. Doing the same with Lithuanian changes those two parameters to Lithuanian equivalents.

- What is the difference between HTTP `HEAD` and `GET` requests when inspecting a website?
```
> curl -I https://vu.lt
HTTP/1.1 301 Moved Permanently
Date: Mon, 23 Nov 2026 17:39:08 GMT
Server: Apache
Location: https://www.vu.lt/
Content-Type: text/html; charset=iso-8859-1

> curl -i https://vu.lt
HTTP/1.1 301 Moved Permanently
Date: Mon, 23 Nov 2026 17:39:30 GMT
Server: Apache
Location: https://www.vu.lt/
Content-Length: 226
Content-Type: text/html; charset=iso-8859-1

<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>301 Moved Permanently</title>
</head><body>
<h1>Moved Permanently</h1>
<p>The document has moved <a href="https://www.vu.lt/">here</a>.</p>
</body></html>
```

HEAD returns headers without page content. GET returns content too. HEAD usually transfers less data.

- How can you identify which HTTP methods a server supports?
```
> curl -i -X OPTIONS https://www.vu.lt
```

Server does not reveal which HTTP methods it supports.

- What publicly accessible files might reveal information about a website's structure?
```
> curl https://www.vu.lt/robots.txt
User-Agent: *
Allow: /
Disallow: /api/

Host: https://www.vu.lt
Sitemap: https://www.vu.lt/sitemap.xml

> curl https://www.vu.lt/sitemap.xml
...
```

`robots.txt` and `sitemap.xml`. Reveals the overall website structure.

- What security-related information can be inferred from HTTP response headers?
```
> curl -I https://www.vu.lt
```

`Strict-Transport-Security: max-age=31536000` Instructs browsers to use HTTPS for this hostname for one year.
`Content-Security-Policy` Restricts where scripts, styles, frames, and other resources can come from.
`X-Frame-Options: SAMEORIGIN` Prevents other origins from embedding the page in a frame, helping reduce clickjacking. CSP’s `frame-ancestors 'self'` provides a similar restriction.
`X-Content-Type-Options: nosniff` Tells browsers not to guess certain resource types instead of respecting the declared content type.
`Permissions-Policy` Disables camera, microphone, geolocation, payment, and USB features for the page.
`Referrer-Policy: strict-origin-when-cross-origin` Limits the address information sent when navigating or making requests to another origin.
`Cross-Origin-Opener-Policy: same-origin` Separates the page’s browsing context from cross-origin windows.
`Cache-Control: ... no-store ...` Instructs caches not to store this response.

- How can you distinguish between an origin server and an intermediary such as a reverse proxy or CDN?

The response advertises Apache and sets a `ROUTEID` cookie, which suggests possible backend routing or load balancing. However, no explicit proxy or cache headers such as `Via`, `Age`, or `X-Cache` are present. Therefore, the headers suggest an intermediary may exist, but do not conclusively distinguish the origin server from a reverse proxy or CDN.

- What information can be collected about TLS connections and certificates?
```
> curl -vI https://vu.lt
* Host vu.lt:443 was resolved.
* IPv6: (none)
* IPv4: 158.129.159.160
*   Trying 158.129.159.160:443...
* ALPN: curl offers h2,http/1.1
* TLSv1.3 (OUT), TLS handshake, Client hello (1):
*  CAfile: /etc/ssl/certs/ca-certificates.crt
*  CApath: /etc/ssl/certs
* TLSv1.3 (IN), TLS handshake, Server hello (2):
* TLSv1.3 (IN), TLS change cipher, Change cipher spec (1):
* TLSv1.3 (IN), TLS handshake, Encrypted Extensions (8):
* TLSv1.3 (IN), TLS handshake, Certificate (11):
* TLSv1.3 (IN), TLS handshake, CERT verify (15):
* TLSv1.3 (IN), TLS handshake, Finished (20):
* TLSv1.3 (OUT), TLS change cipher, Change cipher spec (1):
* TLSv1.3 (OUT), TLS handshake, Finished (20):
* SSL connection using TLSv1.3 / TLS_AES_256_GCM_SHA384 / x25519 / RSASSA-PSS
* ALPN: server accepted http/1.1
* Server certificate:
*  subject: C=LT; L=Vilnius; O=Vilniaus universitetas; CN=vu.lt
*  start date: Jan  9 12:37:17 2026 GMT
*  expire date: Jan  9 12:37:17 2027 GMT
*  subjectAltName: host "vu.lt" matched cert's "vu.lt"
*  issuer: C=GR; O=Hellenic Academic and Research Institutions CA; CN=GEANT TLS RSA 1
*  SSL certificate verify ok.
*   Certificate level 0: Public key type RSA (2048/112 Bits/secBits), signed using sha256WithRSAEncryption
*   Certificate level 1: Public key type RSA (3072/128 Bits/secBits), signed using sha256WithRSAEncryption
*   Certificate level 2: Public key type RSA (4096/152 Bits/secBits), signed using sha256WithRSAEncryption
* Connected to vu.lt (158.129.159.160) port 443
* using HTTP/1.x
> HEAD / HTTP/1.1
> Host: vu.lt
> User-Agent: curl/8.14.1
> Accept: */*
>
* Request completely sent off
* TLSv1.3 (IN), TLS handshake, Newsession Ticket (4):
* TLSv1.3 (IN), TLS handshake, Newsession Ticket (4):
< HTTP/1.1 301 Moved Permanently
HTTP/1.1 301 Moved Permanently
< Date: Mon, 23 Nov 2026 17:49:55 GMT
Date: Mon, 23 Nov 2026 17:49:55 GMT
< Server: Apache
Server: Apache
< Location: https://www.vu.lt/
Location: https://www.vu.lt/
< Content-Type: text/html; charset=iso-8859-1
Content-Type: text/html; charset=iso-8859-1
<
```
-  **Owner:** Vilniaus universitetas, located in Vilnius, Lithuania.
- **Hostname:** The certificate matches `vu.lt`, confirmed by the `subjectAltName` check.
- **Issuer:** `GEANT TLS RSA 1`, operated by the Hellenic Academic and Research Institutions CA.
- **Validity:** From **9 January 2026 to 9 January 2027**, so it was within its validity period when you tested it.
- **Public key:** The server certificate uses a **2048-bit RSA key** and is signed using **SHA-256 with RSA**.
- **Verification:** `SSL certificate verify ok` means curl successfully validated the certificate using the VM’s trusted certificate authorities.

- How can you measure and compare different stages of an HTTP request?
```
> curl -I -w '
DNS: %{time_namelookup}s
TCP connected: %{time_connect}s
TLS completed: %{time_appconnect}s
First byte: %{time_starttransfer}s
Total: %{time_total}s
' https://vu.lt
HTTP/1.1 301 Moved Permanently
Date: Mon, 23 Nov 2026 17:54:47 GMT
Server: Apache
Location: https://www.vu.lt/
Content-Type: text/html; charset=iso-8859-1


DNS: 0.003004s
TCP connected: 0.004825s
TLS completed: 0.046951s
First byte: 0.048862s
Total: 0.050470s
```

- What are the limitations of identifying server technologies through HTTP responses?
`Server` and `X-Powered-By` may be missing, inaccurate, or supplied by a proxy.

- How can automated HTTP requests be performed while minimising unnecessary traffic?
Use HEAD when you only need metadata, save results for reuse, limit requests, and leave pauses between them.