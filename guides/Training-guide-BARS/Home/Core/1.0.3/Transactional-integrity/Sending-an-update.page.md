---
topic: Core-TransactionalIntegrity-Update-1.0.3
---

## Sending an update

For an update or subsequent message, a new X-Request-ID is generated, therefore allowing the receiver to accept the new message. The X-Correlation-ID remains unchanged to indicate it is part of the same conversation.

![BaRS FHIR API end-to-end process](https://raw.githubusercontent.com/NHSDigital/booking-and-referral-media/master/src/images/TransactionIntegrity/Sending-An-Update-1.0.0.svg)

<br>
<hr>