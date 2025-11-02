# Deployment Guide

## Quick Start with Docker

### Prerequisites
- Docker & Docker Compose installed
- Telegram API credentials (get at [my.telegram.org/apps](https://my.telegram.org/apps))
- Session string (generate with `python session_string_generator.py`)

### Setup (5 minutes)

1. **Clone & prepare:**
   ```bash
   git clone <repo-url>
   cd telegram-mcp
   cp .env.example .env
   ```

2. **Fill `.env` with your credentials:**
   ```bash
   TELEGRAM_API_ID=your_api_id
   TELEGRAM_API_HASH=your_api_hash
   TELEGRAM_SESSION_STRING=your_session_string
   ```

3. **Run with Docker Compose:**
   ```bash
   docker compose up --build
   ```

   Or detached mode:
   ```bash
   docker compose up --build -d
   ```

4. **Check logs:**
   ```bash
   docker compose logs -f
   ```

### Server Details
- **HTTP Endpoint:** `http://localhost:8000`
- **Port mapping:** `8004:8000` (adjust in `docker-compose.yml` if needed)
- **Error logs:** Inside container at `/app/mcp_errors.log`

### Stopping
```bash
docker compose down
```

### Alternative: Direct `docker run`
```bash
docker run -it --rm \
  -e TELEGRAM_API_ID="your_api_id" \
  -e TELEGRAM_API_HASH="your_api_hash" \
  -e TELEGRAM_SESSION_STRING="your_session_string" \
  telegram-mcp:latest
```

## Integration with Claude/Cursor

Add to your client config:
```json
{
  "mcpServers": {
    "telegram-mcp": {
      "command": "docker",
      "args": ["run", "--rm", "-e", "TELEGRAM_API_ID=...", "-e", "TELEGRAM_API_HASH=...", "-e", "TELEGRAM_SESSION_STRING=...", "telegram-mcp:latest"]
    }
  }
}
```

---

For full documentation, see [README.md](README.md)
