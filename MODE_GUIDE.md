# FarmSys VoiceLink — Dual Mode

FarmSys VoiceLink intentionally supports both safe Demo Mode and authenticated Live Mode.

## Demo Mode

Set:

```env
DEMO_MODE=true
```

- No real phone calls are placed.
- Demo-authorized contacts may be used.
- CALL-E-shaped results are simulated.
- Use this mode for UI development, testing, screenshots and rehearsing the hackathon demo.

## Live Mode

Set:

```env
DEMO_MODE=false
CALLE_API_KEY=your_server_side_key
ADMIN_KEY=your_strong_secret
```

- Only explicitly authorized farmer contacts may be called.
- Only verified buyers may be called.
- Live call endpoints require the `X-Admin-Key` header.
- CALL-E is invoked from the backend; the API key is never exposed to the browser.
- Commercial matches remain subject to human confirmation.

## Recommended workflow

1. Develop and rehearse in Demo Mode.
2. Deploy staging in Demo Mode.
3. Verify `/health`, `/ready`, dashboard and workflows.
4. Configure CALL-E credentials server-side.
5. Switch staging to Live Mode.
6. Test only with an explicitly authorized number.
7. Keep production Live Mode protected by the admin key and contact authorization.
