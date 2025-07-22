# Scalability Considerations

* **PartyKit Scalability:** PartyKit is specifically designed for high concurrency and real-time messaging, supporting horizontal scaling for simultaneous players and game instances. Its built-in storage scales with the application.
* **Stateless Frontend Clients:** All frontend clients (GB, PMI, ADM) remain stateless, relying on the PartyKit server for real-time state updates, ensuring they are easily scalable.
* **External AI Service Scalability:** Ensure chosen LLM and voice services can handle anticipated request volumes initiated by PartyKit Endpoints.
* **CDN for Assets:** Utilize Content Delivery Networks for serving frontend assets to minimize latency and improve global accessibility. 