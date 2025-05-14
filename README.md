### How much data will the publisher program send to the message broker in one run?

The publisher sends 5 messages, each containing a `UserCreatedEventMessage` with a `user_id` and `user_name`. Each message consists of two `String` fields serialized using the Borsh format. Assuming average user_name length is about 20 characters, and each character is 1 byte (UTF-8), the approximate data per message is:

- `user_id`: ~1–2 bytes
- `user_name`: ~20 bytes
- Borsh overhead: ~8–10 bytes

Estimated total per message: ~30–40 bytes  
Total for 5 messages: **approximately 150–200 bytes**

This is a rough estimate and may vary slightly based on string lengths and Borsh encoding.

---

### What does it mean that the URL `amqp://guest:guest@localhost:5672` is the same in the subscriber program?

This means both the **publisher** and **subscriber** are connecting to the **same RabbitMQ message broker**:

- `guest:guest` is the default **username and password** used to authenticate.
- `localhost` refers to the **local machine**, indicating that the RabbitMQ server is running on the same computer.
- `5672` is the **default port** used by RabbitMQ for AMQP protocol.

Since both programs use the same URL, they operate on the same message queue system, enabling successful publishing and receiving of events on the `"user_created"` queue.
