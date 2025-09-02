# Finance App

This project orchestrates multiple microservices for personal finance tracking using Docker Compose.  
It includes a frontend (`finance_tracking`), a backend (`finance_tracking_api`), and a PostgreSQL database.

---

## Quick Start

### Run All Services

**Production:**
```sh
sudo docker image prune -f -a && sudo docker compose up --build
```

**Development:**
```sh
sudo docker image prune -f -a && sudo BUILD_TARGET=development NODE_ENV=development APP_COMMAND="npm run dev" docker-compose up --build
```

**Stop Containers:**
```sh
sudo docker-compose down
# Or use Ctrl-C in the terminal
```

---

## Local Development

- **Flask backend:**  
  ```sh
  python -m app.main  # Run in finance_tracking_api directory
  ```
- **Frontend:**  
  ```sh
  sudo npm run dev    # Run in finance_tracking directory
  ```

---

## Repository Structure

- `finance_tracking` (frontend): Git submodule linked to its own repo
- `finance_tracking_api` (backend): Git submodule linked to its own repo
- `docker-compose.yml`: Orchestrates all services
- `README.md`: Documentation

---

## Git Submodules

**Clone with submodules:**
```sh
git clone --recurse-submodules <repo-url>
```

**Initialize/update submodules:**
```sh
git submodule update --init --recursive
```

**Add submodules:**
```sh
git submodule add <tracking_repo_url> finance_tracking
git submodule add <tracking_api_repo_url> finance_tracking_api
```

---

## Docker Compose Details

- Docker Compose uses the Dockerfiles in each service folder to build images.
- You can switch between development and production using environment variables:
  - `BUILD_TARGET`
  - `NODE_ENV`
  - `APP_COMMAND`

**Note:**  
Always use `--build` when dependencies change.

---

## System Setup

### Custom Local Hostname

```sh
sudo systemctl enable avahi-daemon
hostnamectl set-hostname ourhome
sudo systemctl restart avahi-daemon
```

---

## Flask Backend

- Accepts only connections from localhost by default.
- Frontend proxies requests to backend using Next.js shared functions.

---

## Database

- Program using docker postgres instance

Run backup in ../finance_app_db_backup folder using this command:
sudo docker exec -t finance_app-postgres-1 pg_dumpall -U postgres > backup_YYYY-MM-DD.sql

---

## Docker Cleanup

Free up system storage with these commands:

```sh
sudo docker system df           # View docker storage usage
sudo docker image prune -a      # Remove unused images
sudo docker container prune     # Remove unused containers
sudo docker volume prune        # Remove unused volumes
sudo docker builder prune       # Remove dangling build cache
```

---

## Prevent System Sleep

**To enable:**
```sh
sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target
```
**To disable:**
```sh
sudo systemctl unmask sleep.target suspend.target hibernate.target hybrid-sleep.target
```

---

## Notes

- Use `sudo` for Docker commands if required.
- For custom local hostname, see "System Setup" above.
- For persistent data, see volume mounts in `docker-compose.yml`.

---