# Dharmovix — Render deployment package

This package is arranged with `package.json` and `server.js` at the repository root and includes a `render.yaml` Blueprint. It is intended for Render Web Service deployment, not static-only Netlify hosting.

## Render setup

1. Put the contents of this folder at the root of a GitHub repository (do not upload a ZIP as the only repository file). Do not upload `.env`, database files, or secrets.
2. In Render choose **New + → Blueprint** and connect the repository containing `render.yaml`.
3. Render will ask for values marked `sync: false`. Enter:
   - `ADMIN_EMAIL`: your admin email
   - `ADMIN_PASSWORD`: a strong initial admin password
   - `SMTP_USER`: `dmvxtechnologies@gmail.com`
   - `SMTP_PASSWORD`: a Google App Password for that Gmail account
   - `FROM_EMAIL`: `Dharmovix <dmvxtechnologies@gmail.com>`
4. The Blueprint creates a 1 GB persistent disk at `/var/data`; SQLite and uploads are configured to use it.
5. After deployment, check the actual Render service URL. If it differs from `https://dharmovix-web.onrender.com`, update `APP_URL` in Render's Environment settings to the real URL and redeploy.
6. Test admin login, email from Admin → Settings, uploads, and data persistence before relying on the site.

## Important data-preservation note

This ZIP does not contain your previous local SQLite database or uploaded user files. To preserve existing records, copy your existing database and uploads into the persistent disk before using the new deployment, or perform a deliberate migration. Do not overwrite or discard your original database until you verify the migrated records.

## Secrets

Never commit `.env`, Gmail App Passwords, admin passwords, or Supabase service-role keys. The `.gitignore` excludes `.env` and local database files.
