# local_passport_auth_service

A demo of user authentication using **Passport.js** with **Local Strategy** and session-based login.

## Features
- User registration with hashed password (bcrypt)
- Login using username/password
- Session persisted with express-session (stored in memory by default)
- Protected route: profile
- Logout destroys the session

## Requirements
- Node.js >= 18
- MongoDB running on default port (27017)

## Installation
```bash
npm install
```

## Running
```bash
node app.js
# or
npm start
```
Server runs on: http://localhost:3000

## API Endpoints
Base path: `/auth`

### POST /register
Registers a new user.
Request body (JSON):
```json
{ "username": "yourname", "password": "yourpassword" }
```
Response:
```json
{ "message": "User registered successfully" }
```
<img width="1091" height="680" alt="image" src="https://github.com/user-attachments/assets/fa032794-c565-4318-81aa-50d60d41fcb8" />


<img width="1409" height="502" alt="image" src="https://github.com/user-attachments/assets/05eb82cd-d4ec-4ffc-a8fe-71da2f51c8dd" />

### POST /login
Logs in user and starts a session.
Request body (JSON):
```json
{ "username": "yourname", "password": "yourpassword" }
```
Response:
```json
{ "message": "Logged in successfully", "user": { ... } }
```
<img width="1122" height="828" alt="image" src="https://github.com/user-attachments/assets/a1fa77c8-8954-4e60-aceb-69925d3e4ff9" />

if not login:
<img width="1094" height="633" alt="image" src="https://github.com/user-attachments/assets/afe06bee-29bb-4505-b6e5-835f660f5ca0" />

### GET /profile
Protected route. Requires login and valid session cookie `connect.sid`.
Response:
```json
{ "message": "Profile data", "user": { ... } }
```
<img width="1088" height="791" alt="image" src="https://github.com/user-attachments/assets/35ab81ae-b522-4fe3-8884-0673eb4d0af1" />

<img width="1073" height="371" alt="image" src="https://github.com/user-attachments/assets/79e5e0fc-a673-4d42-af95-f12fc847d7dc" />

If not logged in:
```json
{ "message": "Not authenticated" }
```

### GET /logout
Logs out and destroys session.
Response:
```json
{ "message": "Logged out" }
```
<img width="1124" height="734" alt="image" src="https://github.com/user-attachments/assets/d667f2d1-a4d2-4701-8f68-80474afbc73c" />

## Testing with Postman
1. Enable **Retain session cookies** in Postman settings.
2. Send `POST /auth/register` with a JSON body to create a user.
3. Send `POST /auth/login` with valid credentials to create a session.
   - Check the `connect.sid` cookie in the Postman Cookies tab.
4. Send `GET /auth/profile` to retrieve profile information. Requires a valid cookie.
5. Send `GET /auth/logout` to destroy the session and clear the cookie.

## Security Notes
- Change the session `secret` in production. (currently `"mysecretkey"` in `app.js`)
- Ensure MongoDB is running at `mongodb://127.0.0.1:27017/passport_local_demo`.

## License
ISC
