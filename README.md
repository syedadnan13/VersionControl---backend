# VersionControl---backend
This backend repo is a custom-built Version Control System (VCS) server that combines Git-like file operations with a full REST API for users, repositories, and issue management. It is built using Node.js, Express, MongoDB, and Socket.IO, and includes a custom CLI that mimics essential Git commands such as init, add, commit, push, pull, and revert.

# 1. What this project is

This repo contains the backend for a custom version-control system that works both as:
- a local CLI (mini-git) — init, add, commit, push, pull, revert — that stores state under .Git/ and can sync to AWS S3; and
- an HTTP + realtime server exposing REST endpoints for users, repositories and issues, plus Socket.IO rooms for live updates.
The backend uses Express and MongoDB for persistence. It is designed for learning, prototyping and to be wired to a frontend that provides a GitHub-like UI.

# 2. Key features

 - Filesystem-based versioning (.apnaGit with staging + commits)
- CLI commands: init, add, commit, push, pull, revert (via index.js yargs wrapper)
- REST API for Users, Repositories, Issues (create/read/update/delete)
- JWT-based authentication + hashed passwords (bcrypt)
- Mongoose data models for Repository & Issue, and native Mongo driver used by User controller
- Push/Pull to AWS S3 for remote storage (optional)
- Socket.IO for real-time updates (room-based by userId)

# Required environment variables
Create a .env file in the project root with the following keys:


```env
PORT=3000
MONGODB_URI=<your-mongodb-connection-string>
JWT_SECRET_KEY=<a-strong-secret>
S3_BUCKET=<your-s3-bucket-name>         # required only for push/pull
AWS_ACCESS_KEY_ID=<aws-access-key>
AWS_SECRET_ACCESS_KEY=<aws-secret-key>
AWS_REGION=<aws-region>
NODE_ENV=development
```
# 3. How to run
Start the server (HTTP + Socket.IO)
```
node index.js start
```
Run CLI commands
```
node index.js init
node index.js add path/to/file
node index.js commit "commit message"
node index.js push
node index.js pull
node index.js revert <commitId>
```
# 4. API reference

Base URL (default): ```http://localhost:3000```

**User endpoints**
- ```POST /signup``` — create user
- ```POST /login``` — login
- ```GET /allUsers``` — list users
- ```GET /userProfile/:id``` — get user by id
- ```PUT /updateProfile/:id``` — update user
- ```DELETE /deleteProfile/:id``` — delete user

**Repository endpoints**
- ```POST /repo/create``` - create repo
- ```GET /repo/all``` — list all repos
- ```GET /repo/:id``` — fetch repository by id
- ```GET /repo/name/:name``` — fetch by name
- ```GET /repo/user/:userID``` — fetch repos of a user
- ```PUT /repo/update/:id``` — update a repo
- ```DELETE /repo/delete/:id``` — delete repo
- ```PATCH /repo/toggle/:id``` — toggle visibility

**Issue endpoints**
- ```POST /issue/create/:id``` — create issue for repo :id
- ```PUT /issue/update/:id``` — update issue
- ```DELETE /issue/delete/:id``` — delete issue
- ```GET /issue/all/:id``` — list issues for repo :id
- ```GET /issue/:id``` — fetch issue by id

# Contribution

Feel free to fork the repository and submit pull requests for improvements or additional features!



