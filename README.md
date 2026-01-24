# Meilisearch Docker Setup

This repository contains a Docker Compose configuration for running [Meilisearch](https://www.meilisearch.com/), a powerful, fast, and easy-to-use search engine.

## Prerequisites

- Docker
- Docker Compose

## Setup Instructions

1. **Copy the environment file**
   ```bash
   cp .env.example .env
   ```

2. **Configure your environment variables**

   Edit the `.env` file and replace the placeholder master key with a secure random string:
   ```bash
   # Generate a secure master key (Linux/macOS)
   openssl rand -base64 32

   # Or use any secure random string generator
   ```

   Update `MEILI_MASTER_KEY` in your `.env` file with the generated key.

3. **Start Meilisearch**
   ```bash
   docker-compose up -d
   ```

4. **Verify it's running**

   Visit http://localhost:7700 in your browser or use curl:
   ```bash
   curl http://localhost:7700/health
   ```

## Configuration

### Environment Variables

- `MEILI_ENV`: Set to `development` or `production`
  - **development**: More permissive, suitable for local testing
  - **production**: Stricter security requirements, master key required

- `MEILI_MASTER_KEY`: Master key for authentication
  - Used to create API keys and authenticate requests
  - Should be a secure random string
  - **Never commit this to version control**

### Data Persistence

Meilisearch data is persisted in the `./meili_data` directory, which is mounted as a Docker volume. This ensures your data survives container restarts.

## Usage

### Start the service
```bash
docker-compose up -d
```

### Stop the service
```bash
docker-compose down
```

### View logs
```bash
docker-compose logs -f meilisearch
```

### Restart the service
```bash
docker-compose restart
```

## Accessing Meilisearch

- **URL**: http://localhost:7700
- **API Documentation**: https://www.meilisearch.com/docs/reference/api/overview

## Data Management

### Database Location
The database file is stored at `./meili_data/data.ms`

### Backups
Refer to the [Meilisearch documentation](https://www.meilisearch.com/docs/guides/docker) for information on:
- Exporting dumps via the API
- Importing dumps using `--import-dump`
- Creating snapshots with `--schedule-snapshot`

## Security Notes

- Always use a strong master key in production
- Keep your `.env` file secure and never commit it to version control
- The `.gitignore` file is configured to exclude sensitive files

## Official Documentation

- [Meilisearch Docker Guide](https://www.meilisearch.com/docs/guides/docker)
- [Meilisearch Documentation](https://www.meilisearch.com/docs)
