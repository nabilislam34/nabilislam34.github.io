# Reflection

## 1. The path of an HTTP request to my GitHub Pages site

1. I type `https://nabilislam34.github.io` into the browser. The browser splits the URL into the protocol (`https`), the host (`nabilislam34.github.io`), and the path (`/`).
2. **DNS lookup:** The browser needs an IP address for the host. It checks its own cache, the operating system cache and lastly, it asks a DNS resolver. The resolver asks the root servers, the `.io` servers, GitHub's name servers, and gets back an IP address that belongs to GitHub's CDN.
3. **TCP connection:** The browser opens a TCP connection to that IP on port 443 using the three-way handshake (SYN, SYN-ACK, ACK).
4. **TLS handshake:** Because the site uses HTTPS, the browser and server agree on encryption keys, and the server sends its certificate for `*.github.io`, which the browser verifies before sending anything.
5. **HTTP request:** The browser sends `GET / HTTP/1.1` (or HTTP/2) with a `Host: nabilislam34.github.io` header. The Host header is how GitHub knows which user's site to serve.
6. **Server response:** GitHub Pages finds the `index.html` from the main branch of my `nabilislam34.github.io` repository and returns `200 OK` with `Content-Type: text/html` and the HTML in the body. If the file is cached at the nearest CDN edge, the edge server answers directly.
7. **Parsing and extra requests:** The browser parses the HTML and finds `<link rel="stylesheet" href="style.css">`, so it makes a second `GET /style.css` request over the same connection.
8. **Rendering:** The browser builds the DOM from the HTML and the CSSOM from the CSS, applies the cascade and specificity rules to decide each element's final styles, then lays out and paints the page.

## 2. AI Attribution

I used Claude Code to help write this site.

**Prompts used:**

> follow the instructions here. first discuss with me ideas for this hw for the website [path to Homework_1_WD_FA26.pdf]

> put my major CSCI. for projects list the automation stuff, the sqlite db, discord/tele bots, dashboard


**Logic error the AI made:**

For the specificity challenge, the AI added a plain `p { color: #333; }` rule. It set the footer's color to a light gray on a dark background.It thought the footer paragraphs would inherit it. This was incorrect as inherited value always loses to any rule that targets the element directly. The footer text "GitHub:" and the copyright line came out dark gray on dark navy and was invisible. I fixed this by setting the color on `footer p` directly. `footer p` has specificity (0,0,2), which is better than `p` at (0,0,1).
