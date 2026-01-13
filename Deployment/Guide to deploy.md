## Deployment

### Prerequisites
- **Windows 10**
- **WSL2** enabled
- **Docker Desktop** installed

### Steps

1. Paste the contents from docker-compose.yml of this folder and save it with the same name.
2. Navigate to the `docker/` directory and open cmd.
3. 3. Start Redmine container: **docker compose up -d**
4. Verify container is running: **docker ps**
5. Open Redmine in browser: **http://localhost:3000**
   Default credentials: Username: admin, Password: admin
