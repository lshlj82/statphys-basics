# Microstates and Macrostates, Interactively

An interactive, single-page web demo of the first concepts of statistical physics: microstates, macrostates, and multiplicity; two-state systems; the Einstein solid; and how counting microstates explains why heat flows from hot to cold, a first version of the second law of thermodynamics.

Created by **Claude Opus 5.5**, based on the lecture notes by **Sang Hoon Lee** (Statistical Physics 1, Chapter 2, The Second Law, Sections 2.1 to 2.3). It follows the demos for Chapter 1 (temperature and energy; heat and work; rates of processes).

## What's inside

**Two-state systems.** The eight outcomes of flipping three coins, grouped into macrostates by the number of heads, with their multiplicities and probabilities. A coin flipper for 3 to 10,000 coins flips them repeatedly and builds a histogram that converges to Ω(N, n)/2<sup>N</sup> with Ω(N, n) = N!/(n!(N − n)!), showing the number of microstates (2<sup>100</sup> ≈ 10<sup>30</sup> for 100 coins) against the number of macrostates (101). The same coins can be shown as the dipoles of a two-state paramagnet, whose total energy is fixed by the number pointing up.

**The Einstein solid.** Quantum oscillators storing energy in equal units, and the dots-and-bars argument for Ω(N, q) = C(q + N − 1, q): a random microstate is drawn as dots (energy units) and bars (dividers between oscillators), with its multiplicity. A table lists every microstate of three oscillators for q = 0 to 5 (1, 3, 6, 10, 15, 21 microstates).

**Interacting systems.** Two Einstein solids sharing energy, Ω<sub>total</sub> = Ω<sub>A</sub>Ω<sub>B</sub>, and the fundamental assumption of statistical mechanics. A chart of Ω<sub>total</sub> against q<sub>A</sub> for any N<sub>A</sub>, N<sub>B</sub>, and q<sub>total</sub>, with presets for the lecture's two examples: 3 + 3 oscillators with 6 units (462 microstates, 100 of them at q<sub>A</sub> = 3) and 300 + 200 oscillators with 100 units (about 9.3 × 10<sup>115</sup> microstates, sharply peaked at q<sub>A</sub> = 60).

**Watching energy flow.** A live simulation of the 300 + 200 oscillator system, starting with all the energy in one solid. At each step a random oscillator passes one unit to another random oscillator; every step is as likely as its reverse (detailed balance), so no microstate is preferred. The energy nonetheless flows irreversibly until q<sub>A</sub> settles near 60, and a histogram of the time spent at each q<sub>A</sub> converges to the exact multiplicity curve: the law of increase of multiplicity, one version of the second law of thermodynamics.

## Running it

There is nothing to build or install. The whole demo is one self-contained file, `index.html`, with all CSS and JavaScript inline.

Open it locally by double-clicking `index.html`, or serve the folder:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

### Publishing with GitHub Pages

1. Push this repository to GitHub.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, select your main branch and the `/ (root)` folder, then save.
4. After a minute or so, the demo will be live at `https://<your-username>.github.io/<repository-name>/`.

## Technical notes

- Plain HTML, CSS, and vanilla JavaScript drawn on `<canvas>`. No frameworks, no build step.
- Multiplicities are computed exactly from logarithms of factorials, so numbers like 9.3 × 10<sup>115</sup> are displayed without overflow.
- In the energy-flow simulation, each step picks an oscillator at random and, if it has energy, moves one unit to a random oscillator. The chance of any step equals the chance of its reverse, so the simulation samples all microstates equally in the long run. Checked against the exact distribution: over 4 × 10<sup>7</sup> steps, the simulated mean and spread of q<sub>A</sub> (59.96 and 5.37) match the exact values (60.00 and 5.36).
- The animations pause when scrolled off screen and start paused when the system asks for reduced motion.
- Long equations wrap on narrow screens.
- Equations are typeset with [MathJax 3](https://www.mathjax.org/) (SVG output, loaded from cdnjs), so they need no extra web fonts.
- The only other external resources are the Newsreader and Instrument Sans fonts from Google Fonts, with system font fallbacks if they fail to load.
- Opening the page requires an internet connection for MathJax; offline, the equations appear as raw TeX.
- Supports light and dark mode: it follows `prefers-color-scheme`, and a sun/moon button in the top-right corner switches by hand, and the choice is remembered across pages; and is responsive down to phone widths.

## Caveats

- The coin flipper draws at most 1,000 coins; larger flips are still computed in full.
- The histogram of time spent at each q<sub>A</sub> includes the initial flow of energy, so its low tail fades only as the run continues.

## Credits

- Demo: Claude Opus 5.5
- Physics content and examples: lecture notes by Sang Hoon Lee
- The lecture follows Daniel V. Schroeder, *An Introduction to Thermal Physics* (Sections 2.1 to 2.3).

## License

No license has been chosen yet. Add a `LICENSE` file (for example, MIT or CC BY 4.0) before sharing or reusing this project publicly, and confirm that any use of the lecture material is permitted by its author.
