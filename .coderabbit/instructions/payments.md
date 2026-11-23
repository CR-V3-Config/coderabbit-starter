---
# AGENT: example domain document. Replace it with one document per high-stakes area of your product, three
# or four at most, or delete it. One file per area; `id` matches the file name; `paths` is always set.
# List five to eight concrete defects a senior engineer on this team checks for by hand, in the team's
# words. Under 1,200 characters.
id: payments
name: Payments and billing
paths:
  - "**/{payment,payments,billing,checkout,subscription,subscriptions}*/**"
---

Flag: a charge, refund or cancellation that is not idempotent on retry or webhook replay; amounts handled as floating point; a webhook handler that does not verify the signature; account state derived from a local flag when the payment provider is the source of truth; a failed payment path that leaves the customer with full access or with no access and no way back.
