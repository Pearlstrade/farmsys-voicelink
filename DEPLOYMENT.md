# FarmSys VoiceLink Deployment Runbook

## 1. Local smoke test

```bash
python -m venv .venv
# Windows: .venv\\Scripts\\activate
# macOS/Linux: source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env
uvicorn app.main:app --reload
```

Open `http://127.0.0.1:8000` and click **Load demo farmer & buyer**.

Demo mode is safe and does not place real calls.

## 2. Production environment

Required variables:

- `APP_ENV=production`
- `DATABASE_URL=<managed PostgreSQL URL>`
- `SECRET_KEY=<long random secret>`
- `ADMIN_KEY=<long random secret>`
- `CALLE_API_KEY=<CALL-E secret>`
- `CALLE_BASE_URL=https://api.heycall-e.com`
- `DEMO_MODE=false` only after staging validation

Never commit `.env`, API keys, phone lists, transcripts containing personal data, or database files.

## 3. Safe promotion path

1. Deploy with `DEMO_MODE=true`.
2. Verify `/health` and `/ready`.
3. Seed and exercise the demo workflow.
4. Configure CALL-E credentials as platform secrets.
5. Authorize exactly one test number.
6. Set `DEMO_MODE=false`.
7. Keep `ADMIN_KEY` enabled for live-call endpoints.
8. Place one supervised call.
9. Verify structured result, evidence, audit record and match creation.
10. Only then add additional authorised contacts.

## 4. Render

The included `render.yaml` provisions a Docker web service. Add the PostgreSQL connection string and CALL-E key as secrets in Render. Keep demo mode enabled until the public deployment has passed smoke tests.

## 5. Production checklist

- [ ] HTTPS enabled
- [ ] PostgreSQL configured
- [ ] Secrets stored only in deployment secret manager
- [ ] CALL-E key tested
- [ ] One authorised test number
- [ ] AI disclosure verified
- [ ] Human confirmation required for matches
- [ ] Live call endpoint protected by `X-Admin-Key`
- [ ] Call failures visible in dashboard
- [ ] No sensitive credentials collected by call prompts
- [ ] GitHub repository contains no secrets
