# Sakhi – your digital guide (Python / Flask)

Same mobile app as the HTML version, now with a real backend.

## Run (VS Code terminal)
```
python -m venv .venv
.venv\Scripts\activate          # Windows      (Mac/Linux: source .venv/bin/activate)
pip install -r requirements.txt
python app.py
```
Open http://localhost:5000  (on your phone: http://<your-pc-ip>:5000 on the same Wi-Fi;
location and voice need https or localhost, so use a tunnel/host with https for phone tests).

## What the Python side does
| Endpoint | Purpose |
|---|---|
| `POST /api/otp/send` | validates the number, makes a 4-digit OTP (valid 5 min, 1 send / 30 s) |
| `POST /api/otp/verify` | checks it (max 5 tries), starts a 30-day login session |
| `GET/PUT /api/me` | document locker (+ photos) and saved location, stored in SQLite (`sakhi.db`) |
| `POST /api/logout` | ends the session |

## Settings (environment variables)
- `SAKHI_SECRET` – any long random text; keeps logins valid after restart.
- `SAKHI_DEMO` – `1` (default) shows the OTP on screen and in the console. Set `0` once real SMS is connected.
- `SAKHI_DB`, `PORT`, `FLASK_DEBUG=1` – optional.

## Real SMS
Edit `send_sms()` in `app.py` and call your provider (MSG91, Twilio, Fast2SMS...). Then set `SAKHI_DEMO=0`.

## Files
- `app.py` – the server
- `static/index.html` – the app screens (all 6 languages, schemes, emergency numbers, themes)

## Before going live
Use https, run with a production server (`pip install gunicorn` then `gunicorn app:app`), set `SAKHI_SECRET`,
and note that Aadhaar/ration photos are personal data – get consent and secure the database file.
