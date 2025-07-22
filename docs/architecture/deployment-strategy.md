# Deployment Strategy

* **PartyKit Deployment:** Deploy the PartyKit server-side logic and storage to the PartyKit platform/CDN.
* **Frontend Clients (GB, PMI, ADM):**
    * Serve as static assets (pure React application) deployed to a modern CDN or static hosting provider (e.g., Vercel, Netlify, AWS S3/CloudFront, Google Cloud Storage/CDN).
    * Each client (Game Board, Player Interface, Admin Dashboard) will likely have its own dedicated URL. 