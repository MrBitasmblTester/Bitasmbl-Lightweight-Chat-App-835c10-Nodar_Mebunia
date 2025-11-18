# Bitasmbl-Lightweight-Chat-App-835c10-Nodar_Mebunia

## Description
Build a web application that allows users to join anonymous chatrooms and exchange messages in real-time using WebSockets. The focus is on fast communication, simple interface, and responsive updates without requiring user registration.

## Tech Stack
- Express.js
- React
- Socket.IO

## Requirements
- Allow users to join chatrooms without authentication
- Gracefully handle disconnected users and reconnections
- Handle multiple chatrooms simultaneously
- Display messages with timestamps and user identifiers (anonymous)
- Send and receive messages in real-time using WebSockets

## Installation
Follow these steps to set up the project locally. This guide assumes the repository is hosted under the provided GitHub username.

1. Clone the repository:

   git clone https://github.com/MrBitasmblTester/Bitasmbl-Lightweight-Chat-App-835c10-Nodar_Mebunia.git
   cd Bitasmbl-Lightweight-Chat-App-835c10-Nodar_Mebunia

2. Install backend dependencies (Express.js + Socket.IO):

   cd server
   npm install

3. Install frontend dependencies (React + socket.io-client):

   cd ../client
   npm install

Note: The project is expected to have separate server and client directories. If your repository layout differs, run the install commands in the appropriate directories containing package.json for each part.

## Usage
Run the backend and frontend in separate terminals.

1. Start the backend (Express + Socket.IO):

   cd server
   npm start

2. Start the frontend (React):

   cd client
   npm start

3. Open the frontend in your browser (typically http://localhost:3000). Ensure the backend server is running and reachable by the frontend.

Messages are exchanged in real-time via WebSockets (Socket.IO). Use multiple browser windows/tabs to test anonymous users joining the same or different chatrooms.

## Implementation Steps
1. Initialize the backend with Express.js and Socket.IO. Create an HTTP server and attach a Socket.IO server to it.
2. Implement a minimal Express route for server health (e.g., GET /health) to verify the backend is running.
3. Define Socket.IO events on the server:
   - Handle a "join" event where a socket requests to join a specific chatroom (use socket.join(room)).
   - Handle a "message" event where the server timestamps the message, attaches an anonymous identifier (e.g., socket.id or a generated short id), and broadcasts it to the room with io.to(room).emit(...).
   - Handle "disconnect" and reconnection-related events to notify room members or update presence as needed.
4. Support multiple chatrooms by using Socket.IO rooms; messages and presence updates should be scoped to the room the socket has joined.
5. Ensure messages include a timestamp (e.g., new Date().toISOString()) and an anonymous user identifier before emitting to clients.
6. On the client (React):
   - Install socket.io-client and connect to the backend Socket.IO endpoint.
   - Provide a simple UI to enter or select a chatroom name and join without authentication.
   - After joining, display incoming messages in real-time with timestamp and anonymous identifier, and provide an input to send messages.
   - Store the current room locally (in component state) so the client can rejoin the same room automatically after reconnection.
   - Handle Socket.IO connection lifecycle events (connect, disconnect, reconnect, connect_error) to present connection state to the user and attempt automatic reconnection.
7. Gracefully handle disconnected users: when a socket disconnects, emit a room-scoped notification (optional) and let clients update UI accordingly. On reconnection, rejoin the stored room and reconcile state on the client.
8. Test functionality by opening multiple clients (browser tabs/windows) and verifying:
   - Users can join rooms without authentication.
   - Real-time messages are delivered to clients in the same room only.
   - Messages show timestamps and anonymous identifiers.
   - Disconnects and reconnections are handled gracefully and clients can rejoin rooms automatically.

## API Endpoints (Optional)
- GET /health
  - Method: GET
  - Description: Basic health check endpoint to verify the backend server is running and responding.