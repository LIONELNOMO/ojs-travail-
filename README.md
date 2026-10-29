# Biolinguistics — OJS journal (Docker)

A custom academic journal built on **OJS 3.3** running in **Docker**, with a custom theme
(`biolingtheme`) that reproduces the PsychOpen "Biolinguistics" look. An older React/Vite mockup
(`ojs-journal/`) is kept as a visual reference only.

> 🤖 If you are an AI assistant, read **[CLAUDE.md](CLAUDE.md)** first — it has the full architecture
> and the non-obvious gotchas.

---

## Quick start (new machine)

Requires **Docker Desktop**, **Node.js 18+**, **git**.

```bash
# 1. Start the stack (downloads images the first time)
cd ojs-docker
docker compose up -d

# 2. Restore the saved journal (settings, contacts, theme, issues)
cd ..
bash scripts/restore.sh

# 3. Open the journal
#    → http://localhost:8080/journal
```

Without step 2 the OJS install is empty. The saved state lives in `ojs-docker/backup/`.

---

## Everyday commands

```bash
# Start / stop
cd ojs-docker && docker compose up -d
cd ojs-docker && docker compose down

# After editing the theme (templates/CSS), clear OJS caches:
docker exec ojs-docker-ojs-1 bash -c "rm -rf /var/www/html/cache/t_compile/* /var/www/html/cache/fc-*.php"

# Save the current journal state back into the repo (then commit):
bash scripts/backup.sh
```

---

## Layout

| Path | What |
|------|------|
| `ojs-docker/docker-compose.yml` | OJS + MariaDB stack |
| `ojs-docker/themes/biolingtheme/` | the custom theme (current design) |
| `ojs-docker/backup/` | DB dump + uploaded files (the saved journal) |
| `ojs-journal/` | old React mockup (reference only) |
| `scripts/` | `restore.sh`, `backup.sh` |
| `CLAUDE.md` | full context for AI assistants |

---

## ⚠️ Keep this repo private

`ojs-docker/config.inc.php` contains `api_key_secret` and the DB dump contains journal data.
Do not make this repository public.
# ojs-travail-
