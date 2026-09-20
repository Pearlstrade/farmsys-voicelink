# FarmSys VoiceLink v0.7.0

**From farm to market — by phone.**

FarmSys VoiceLink is a CALL-E-powered agricultural market-linkage application. It calls authorised farmers and verified buyers, extracts structured information from natural phone conversations, and turns the results into potential market matches.

## Modes

- **Demo mode:** no real calls. Safe for development, screenshots and rehearsals.
- **Live mode:** uses the CALL-E backend and requires `CALLE_API_KEY`, an `ADMIN_KEY`, and explicitly authorised contacts.

## Local run

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env
uvicorn app.main:app --reload
```

Open `http://localhost:8000`.

## Production

See `DEPLOYMENT.md`. The Render configuration starts in `DEMO_MODE=true`; switch to live only after the public deployment is verified.

## Safety

VoiceLink identifies itself as AI on live calls, requires farmer authorization, restricts buyer calls to verified buyers, stores call evidence/results, and keeps market matches subject to human confirmation. Never commit API keys or real phone numbers to source control.


## Deployment note

The Render Blueprint provisions both the web service and a Render Postgres database. It starts in `DEMO_MODE=true`; promote to live calling only after the public staging checks pass. Render free Postgres is intended for testing and expires after 30 days, so upgrade or move the database before long-term production use.
