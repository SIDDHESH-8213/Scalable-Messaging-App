# Scalable Real-Time Chat Application
![image](https://github.com/user-attachments/assets/6540dc0b-fc1c-4efc-9e1b-02b545c3a297)


This project is a backend implementation of a real-time chat application, similar to WhatsApp, built with Node.js, Express.js, WebSockets, Redis, Kafka, and MongoDB. It focuses on providing a scalable and robust backend for one-on-one messaging.

## Features

*   Real-time one-on-one messaging using WebSockets (Socket.IO).
*   Offline message delivery using MongoDB.
*   Message read receipts.
*   Message updates and deletes.
*   User presence tracking using Redis.
*   Message persistence and distribution using Kafka.
*   REST API for message management.

## Tech Stack

*   Backend: Node.js, Express.js
*   Real-time Communication: WebSockets (Socket.IO)
*   Message Broker: Kafka
*   Data Store: MongoDB
*   Caching/Pub/Sub: Redis

## Message Flow

| Scenario              | Message Flow                                                                                                                                                                                                                                                               |
| --------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Same Server, Both Online | u1 -> WebSocket Server -> Redis Pub/Sub -> WebSocket Server -> u2; Concurrently: WebSocket Server -> Kafka -> MongoDB                                                                                                                                                           |
| Same Server, u2 Offline | u1 -> WebSocket Server -> Redis Pub/Sub (transient) -> Kafka -> MongoDB; u2 retrieves messages from MongoDB upon reconnecting.                                                                                                                                               |
| Diff. Servers, Both Online | u1 -> WS1 -> Redis Pub/Sub -> WS2 -> u2; Concurrently: WS1 -> Kafka -> MongoDB                                                                                                                                                                                                    |
| Diff. Servers, u2 Offline | u1 -> WS1 -> Redis Pub/Sub (transient) -> Kafka -> MongoDB; u2 retrieves messages from MongoDB upon reconnecting. |

## Getting Started

1.  Clone the repository: `git clone [repository URL]`
2.  Install dependencies: `npm install`
3.  Set up your `.env` file (see `.env.example` for the required variables).
4.  Start MongoDB, Redis, and Kafka.
5.  Run the backend: `npm run dev`

## Future Improvements

*   To implement proper end-to-end encryption.
*   To improve Kafka consumer error handling and implement a dead-letter queue.
*   To deploy to a cloud platform like AWS.
*   To add more features like group chats, file sharing, etc.

## Contributing

Contributions are welcome! Please open an issue or submit a pull request.

