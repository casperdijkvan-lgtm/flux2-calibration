# Flux 2 Calibration

A one-page web app that runs a spin-down calibration on a **Tacx Flux 2** smart trainer over Bluetooth, the same way the Tacx app does.

## Use it

Web Bluetooth only works in **Google Chrome or Microsoft Edge** (not Safari), and only on `https://` or `localhost`.

```bash
python3 -m http.server 8000
```

Then open http://localhost:8000 in Chrome.

1. Close Zwift / the Tacx app (the trainer accepts only one Bluetooth connection).
2. Click **Connect trainer** and pick your Flux 2.
3. Click **Start calibration**, pedal up to the target speed shown, then stop pedalling completely.
4. The trainer measures the coast-down and reports success or failure.

Click **Demo** to see the whole flow with a simulated trainer.

## How it works

- **Tacx FE-C over Bluetooth** (preferred): service `6e40fec1-b5a3-f393-e0a9-e50e24dcca9e`. The app sends ANT+ FE-C data page `0x01` with the spin-down bit set, then reads page `0x02` (calibration in progress / target speed), page `0x10` (speed) and the page `0x01` result (spin-down time, temperature).
- **FTMS** (fallback): Fitness Machine Control Point opcode `0x13` (spin down), status via Fitness Machine Status `0x14`.

Open **Bluetooth log** on the page to see the raw messages if something doesn't work.

> Not yet tested against a real Flux 2.
