[README.md](https://github.com/user-attachments/files/26907010/README.md)
# Laser Cutter Settings Calculator

A free, single-page web tool that gives hobbyist laser cutter users instant starting-point settings for diode and CO₂ machines — no login, no ads, no fluff.

**Live site:** [hobbyistlasercalc.com](https://hobbyistlasercalc.com)

---

## What it does

Select your machine, material, and thickness (in mm or inches) and get:

- Recommended power %
- Speed (mm/min for diode / mm/s for CO₂)
- Number of passes
- Air assist level
- Kerf offset
- Focus point recommendation
- LightBurn-specific tips for each combination

Covers **cut** and **engrave** operations across 30+ materials including wood, acrylic, leather, foam board (including Dollar Tree), EVA foam, cork, fabric, rubber, and paper.

---

## Supported machines

**Diode lasers**
- Longer Ray 5 (5W, 10W, 20W), Longer B1 (30W)
- xTool D1 / D1 Pro (5W, 10W, 20W), xTool S1, F1, M1
- Sculpfun S9, S30 Pro, S30 Pro Max, S30 Ultra
- Ortur LM2 Pro, LM3, LM3 Ultra
- AtomStack A5 / A10 / A20 / X20 Pro
- Comgrow Z1, TwoTrees TS2 / TS3
- Generic 5W / 10W / 20W fallback categories

**CO₂ lasers**
- K40, OMTech 50W / 60W
- Glowforge Basic / Plus / Pro
- Boss LS-1416
- Generic CO₂ 40W / 60W fallback categories

---

## ⚠️ Important disclaimer

**All settings are starting-point estimates, not guaranteed values.**

Real-world results depend on factors this tool cannot know: lens focus accuracy, lens cleanliness, material moisture content, brand and batch variation, ambient temperature, table flatness, and machine calibration. Always run a test cut on scrap before committing to your workpiece. Never leave a running laser unattended.

---

## Contributing

This database grows with community input. If you have tested, reliable settings for a machine or material not listed — or corrections to existing entries — contributions are welcome.

**To suggest settings:**
- Open an [Issue](../../issues) and describe the machine, material, thickness, and settings that worked for you
- Or submit a Pull Request with changes directly to `index.html`

**To add a new machine:**
1. Add an `<option>` to the appropriate `<optgroup>` in the machine select dropdown
2. Add the machine key and display name to `getMachineName()`
3. Map it to the correct wattage category in `machineToCategory`
4. Optionally add material-specific overrides to the `DB` object if the machine behaves significantly differently from its wattage class

The settings database is in the `DB` object in `index.html`. Each entry follows this structure:

```js
'wattage_category': {
  material_key: {
    cut: {
      power: [min, max],   // percentage range
      speed: 300,          // mm/min (diode) or speed_mms: 20 (CO₂)
      passes: [1, 2],      // single number or range
      air: 'High',         // Off / Low / Medium / High / Max
      kerf: 0.12,          // mm
      focus: 'surface',    // 'surface' or 'mid'
      confidence: 90,      // 0–100, how well-tested this data is
      notes: '...',
      lb_tip: '...'
    },
    engrave: { ... }
  }
}
```

---

## Tech stack

- Pure HTML, CSS, and vanilla JavaScript — zero dependencies, zero frameworks
- Single file (`index.html`) — the entire site is one file
- Deployed via [Cloudflare Pages](https://pages.cloudflare.com/) — free tier, deploys automatically on every push to `main`

---

## Roadmap

- [ ] Community settings submission form
- [ ] RMD (Required Minimum Distribution) calculator — second site in the portfolio
- [ ] More materials: anodized aluminum, stone tile, leather tooling
- [ ] More machines as they are released and tested
- [ ] Printable settings cheat sheet (PDF export)

---

## License

MIT — see [LICENSE](LICENSE) for details.

You are free to use, fork, and build on this. If you do something cool with it, feel free to share.

---

*Built by a hobbyist, for hobbyists. Settings are based on real-world testing on a Longer Ray 5 20W and community data. Contributions welcome.*
