# OwnFMS.works installer

**Own your system. Own your data. Own your future.**

This is the web page behind <https://ownfms-works.github.io/installer/>. It sets up the open-source
[OwnFMS.works](https://ownfms.works) base configuration (nine grant-management modules) on a Corteza server that
**you** control. You paste your server address and a setup key, press **Install**, and the page builds everything.

The whole installer is one readable file, `index.html`. There are no outside scripts, no analytics and no tracking.

## How it works, and what it does with your key

- The page talks **only to your own Corteza server**. It makes no other network requests.
- Your client ID and client secret stay in the page's memory. They are not stored (no cookies, no local storage, no
  address bar) and they are never sent to us or to anyone but your server.
- When the install finishes the page can **revoke the setup key for you**: it disables the key, deletes it, and then
  proves the server now refuses it. This is on by default.
- Use a server just for this. The setup changes a few server-wide settings; the page lists them before you start.

## Before you trust a page that asks for an admin key

Please check it. Two simple ways:

1. **Read the code.** It is one file, `index.html`, in this repository.
2. **Compare the checksum.** The SHA-256 of `index.html` is in `SHA256SUMS`:

   ```
   4403e5bec37ec0e80fb70809656167bfb8ce25d66b541844279904789e25fe70  index.html
   ```

   To check what the live site serves, run this and compare the result with `SHA256SUMS`:

   ```
   curl -s https://ownfms-works.github.io/installer/ | sha256sum
   ```

You can also read the network panel in your browser's developer tools while you use it: the only requests go to your own server.

## What you need

- A Corteza server, **version 2024.9.1**, reachable over https. A managed one such as Elestio works.
- A setup client created in the Corteza admin area (Auth Clients): grant type `client_credentials`, acting as your administrator.
- About 15 minutes.

Prefer not to use a web page? The same setup is available as Python scripts and a Colab notebook in the starter package.

## Revoking the setup key by hand

Deleting a client alone does **not** stop its secret from working on this Corteza version, and expiry dates are not enforced.
To be sure: in the admin area open Auth Clients, open your setup client, **untick Enabled**, save, then delete it.

## Licence

Apache License 2.0. See [LICENSE](LICENSE). Corteza is also Apache 2.0.
