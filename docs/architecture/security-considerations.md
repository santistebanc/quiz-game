# Security Considerations

* **Admin Dashboard Access:** As per user's request, no authentication will be implemented for the Admin Dashboard. Access relies on the inherent trust within the social gathering environment.
* **Secure Real-time Communication:** PartyKit inherently uses WebSockets over TLS (WSS) for encrypted communication between clients and the server.
* **API Key Management:** Securely manage API keys for LLM and voice services within PartyKit Endpoints (using environment variables/secrets management provided by PartyKit or the hosting platform) to prevent client-side exposure.
* **Input Validation:** Validate all user inputs (player names, admin commands) on both client and PartyKit server-side to prevent injection attacks or malformed data.
* **Rate Limiting:** Implement rate limiting within PartyKit Endpoints on sensitive operations (e.g., question generation) to prevent abuse of external AI services.
* **Sanitization of LLM Outputs:** Sanitize any LLM-generated content before displaying it on client interfaces to prevent XSS attacks. 