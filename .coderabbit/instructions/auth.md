---
# AGENT: example domain document. Replace it with one document per high-stakes area of your product, three
# or four at most, or delete it. One file per area; `id` matches the file name; `paths` is always set.
# List five to eight concrete defects a senior engineer on this team checks for by hand, in the team's
# words. Under 1,200 characters.
id: auth
name: Authentication and sessions
paths:
  - "**/{auth,authentication,session,sessions,identity}*/**"
---

Flag: a route or handler reachable without the authentication check its neighbours have; authorization decided from client supplied data; tokens or session ids written to logs; password, token or secret comparison that is not constant time; a session that survives logout or password change; a redirect after login built from an unvalidated parameter.
