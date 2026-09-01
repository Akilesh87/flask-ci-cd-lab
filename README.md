# Flask CI/CD Lab (EX24)

## What's included
- `app.py` – minimal Flask app with `/` and `/health` routes
- `test_app.py` – pytest tests
- `requirements.txt` – dependencies
- `Dockerfile` – containerizes the app
- `.github/workflows/ci-cd.yml` – GitHub Actions pipeline (test → build/push Docker image → deploy to Heroku)

## Setup steps

1. **Create a new GitHub repo** and push this whole folder to it:
   ```
   git init
   git add .
   git commit -m "Initial commit: Flask app + CI/CD pipeline"
   git branch -M main
   git remote add origin <your-repo-url>
   git push -u origin main
   ```

2. **Add GitHub repo secrets** (Settings → Secrets and variables → Actions → New repository secret):
   - `DOCKER_USERNAME` – your Docker Hub username
   - `DOCKER_PASSWORD` – a Docker Hub access token (create one under Docker Hub → Account Settings → Security)
   - `HEROKU_API_KEY` – from Heroku account settings
   - `HEROKU_APP_NAME` – name of an existing Heroku app (create one first with `heroku create your-app-name`)
   - `HEROKU_EMAIL` – the email tied to your Heroku account

3. **Push to `main`** — this triggers the pipeline automatically. Check the "Actions" tab on GitHub to watch it run.

4. **Verify**
   - Tests pass (green check on `build-and-test` job)
   - Image appears on Docker Hub under `<DOCKER_USERNAME>/flask-app:latest`
   - App is live at `https://<HEROKU_APP_NAME>.herokuapp.com`

5. **For submission**: screenshot the green Actions run, include the workflow YAML, and the live deployment link.

## Local testing (optional, before pushing)
```
pip install -r requirements.txt
pytest
docker build -t flask-app .
docker run -p 5000:5000 flask-app
```
