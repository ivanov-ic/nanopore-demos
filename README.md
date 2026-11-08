# Nanopore interactive demos

Two interactive demos for the lecture on nanopores and single-molecule technologies for nanomedicine,
Department of Chemistry, Imperial College London. Each demo runs entirely in the browser from a single
HTML file, needs no network connection once loaded, and works on a phone, a laptop, or a lecture-theatre
projector.

**Live site:** https://ivanov-ic.github.io/nanopore-demos/

| Demo | What it shows |
|---|---|
| [N1.1 The pore as a molecule counter](https://ivanov-ic.github.io/nanopore-demos/n1-1-pore-counter.html) | How a nanopore turns single molecules into a current signal: each dip is one molecule, its depth gives the size, and its rate gives the concentration. |
| [N1.2 How many events do you need?](https://ivanov-ic.github.io/nanopore-demos/n1-2-event-statistics.html) | Why a single-molecule measurement of a rare biomarker still needs a long recording: counting statistics for healthy and patient samples. |

## N1.1 The pore as a molecule counter

A cylindrical pore in a thin membrane separates two chambers of 0.1 mol dm⁻³ KCl. A voltage drives an ionic
current, and every molecule that threads through the pore blocks part of it.

- **Slow motion.** One translocation, stretched in time, with the particle (or a DNA strand) and the current
  trace drawn from the same clock, so that the dip begins when the particle enters the pore.
- **Live record.** A 1 s window of the current that scrolls in real time and follows every control.
- **Long record.** A 2, 10, or 60 s record in which each protein's events are drawn in its own colour.
- **Molecules.** A protein modelled as a sphere (one or two species), a 9.1 kbp DNA carrier, and the same
  carrier with targets bound at three sites. Keys 1, 2, and 3 switch the view.
- **Teaching points.** The depth of a dip reports the size and the rate reports the concentration. Proteins
  of similar size give dips that overlap, which is why a bare nanopore is not selective, and why a
  position-encoded DNA carrier, whose bound targets are read as peaks at known fractions of its length, is
  used to give selectivity.

### What is computed

| Quantity | Model |
|---|---|
| Open-pore conductance | G = σ / (4L/πd² + 1/d), a cylinder plus access resistance [1] |
| Blockade by a sphere | DeBlois and Bean, ΔR/R = a³F / (d²L<sub>eff</sub>), with F = 1/(1 − 0.8 (a/d)³) and L<sub>eff</sub> = L + 0.8 d [1, 2] |
| Capture rate | η c N<sub>A</sub> (4D·d/2 + μI₀/σ): the Smoluchowski diffusion limit plus the drift flux through a hemisphere around the pore, with D from the Stokes–Einstein relation and μ = zeD/k<sub>B</sub>T; background in [3, 4]. Electro-osmosis is ignored. |
| Noise | Johnson noise 4k<sub>B</sub>TG plus one constant excess term, through a single-pole filter with equivalent noise bandwidth πB/2 |
| Detection | A dip is counted when the filtered current passes a threshold of n times the rms noise, with a hold time and a refractory period; the expected histogram shape is built by running 1000 model events through the same filter and detector |

### The DNA carrier models

The 9.1 kbp three-site carrier follows the carrier described in Ren et al. [5], whose main text gives the
design positions (0.18, 0.48, and 1.0 of the contour), the measured fractional positions with their spreads
(0.21 ± 0.07, 0.55 ± 0.11, and 0.98 ± 0.02), the binding ratios (about 13 per cent per site in the variant
panel, and 18.4 per cent of events with all three sites bound for full-length RNA), and reference peak
sizes for protein-bound 10 kbp carriers. A bound site adds a peak above the DNA level at its position, with
position along the contour read as time at constant speed.

The following are **not** in the main text of [5], so the demo exposes them as editable parameters in a
table, each tagged as assumed or as a reference value, and they are placeholders until replaced from the
paper's Supplementary Figs. S18 to S22 or the raw traces [6]:

- the DNA level (47 pA, assumed from the 10 kbp folding ratio);
- the dwell time and the noise;
- the peak amplitude and width at the first site, and for RNA targets generally (the reference values used
  are the S and N protein values for 10 kbp carriers);
- the fraction of the event covered by a fold.

The signal amplitudes are the paper's empirical values in pA, not computed from the pore physics. The
paper's measurements used a quartz nanopipette in 2 mol dm⁻³ LiCl, which the demo does not model.

## N1.2 How many events do you need?

A nanopore sees one molecule at a time, so the fraction of carrier events that carry a bound target is a
count, and a count has an uncertainty of about 1/√N.

- **Capture rate** of a 48.5 kbp-class DNA carrier into the pore, from the same diffusion plus drift model
  as N1.1, with a 2 ms dwell.
- **Binding** of a target to one aptamer per carrier, using the exact two-component equilibrium [7]. The
  carriers are not in excess, so they take target out of solution: adding carriers raises the event rate
  but lowers the bound fraction.
- **Samples.** Simulated healthy and patient samples are drawn as Poisson numbers of events, each carrying
  a binomial number of bound targets, and the chance that a randomly chosen patient reads higher than a
  randomly chosen healthy control is computed with a normal approximation, which the page says is rough
  below about ten events. The time needed for a chance of 0.95 follows from the same formula.
- **Limits.** The only noise is counting noise. Every healthy sample has the same true bound fraction, and
  so does every patient, which real people do not.

The motivating data are the α-synuclein measurements in cerebrospinal fluid [8], where the fraction of
carrier events with a subpeak separates patients with Parkinson's disease from healthy controls, using the
carrier approach introduced in [9].

## Checks that were run

- The conductance, the blockade, and the noise were recomputed independently in Python and compared with the
  values the pages display, to three significant figures, at the defaults and at the presets.
- The conductance reproduces σd for a zero-length pore and σπd²/4L for a long pore, and the blockade
  reproduces 1.5 times the excluded-volume fraction for a small sphere.
- The simulated noise matches the analytic rms at 1, 10, 50, and 100 kHz, and the live stream's event rate,
  detection fraction, and mean depth agree with the model library.
- Simulated carrier events reproduce the input positions, spreads, binding fractions, and folding fraction.
- For N1.2, a Monte Carlo run agrees with the analytic chance of separation (0.958 against 0.955 at the
  default).

These demos are teaching models. They are not analysis software and are not for clinical use.

## Files

| File | What it is |
|---|---|
| `index.html` | The landing page. |
| `n1-1-pore-counter.html` | N1.1. |
| `n1-2-event-statistics.html` | N1.2. |
| `javascript-test.html` | A page that tests whether scripts run where a demo is opened. |
| `OFL.txt` | The licence of the embedded typefaces. |

Each demo is one self-contained file with the fonts embedded, so any of them can be opened directly from
disk. Do not rename the files once links or QR codes point to them.

## Using them

- **In a lecture:** open the demo in a browser beside the slides and press F11. In N1.1, keys 1, 2, and 3
  switch between the slow motion, the live record, and the long record.
- **In Canvas:** scripts in uploaded files are blocked, so embed the published page in the HTML view of a
  page: `<iframe src="https://ivanov-ic.github.io/nanopore-demos/n1-1-pore-counter.html" width="100%" height="2200" title="The pore as a molecule counter"></iframe>`

## References

1. Kowalczyk SW, Grosberg AY, Rabin Y, Dekker C. Modeling the conductance and DNA blockade of solid-state
   nanopores. *Nanotechnology* **22**, 315101 (2011).
2. DeBlois RW, Bean CP. Counting and sizing of submicron particles by the resistive pulse technique.
   *Review of Scientific Instruments* **41**, 909 (1970).
3. Wanunu M, Morrison W, Rabin Y, Grosberg AY, Meller A. Electrostatic focusing of unlabelled DNA into
   nanoscale pores using a salt gradient. *Nature Nanotechnology* **5**, 160 (2010).
4. Grosberg AY, Rabin Y. DNA capture into a nanopore: interplay of diffusion and electrohydrodynamics.
   *Journal of Chemical Physics* **133**, 165102 (2010).
5. Ren R, Cai S, Fang X, et al. Multiplexed detection of viral antigen and RNA using nanopore sensing and
   encoded molecular probes. *Nature Communications* **14**, 7362 (2023). doi:10.1038/s41467-023-43004-9
6. Ren R, Cai S. Example data of the nanopore translocation experiments for [5]. Zenodo (2023).
   doi:10.5281/zenodo.8143395
7. Morrison JF. Kinetics of the reversible inhibition of enzyme-catalysed reactions by tight-binding
   inhibitors. *Biochimica et Biophysica Acta* **185**, 269 (1969).
8. Liu et al. *ACS Nano* **17**, 22999 (2023).
9. Sze Y, et al. *Nature Communications* **8**, 1552 (2017).

## How to cite

Ivanov AP. Nanopore interactive demos. Imperial College London, 2026.
https://ivanov-ic.github.io/nanopore-demos/

## Licence

The demos are © 2026 Aleksandar P. Ivanov, licensed under CC BY-NC-ND 4.0
(https://creativecommons.org/licenses/by-nc-nd/4.0/). The embedded typefaces, IBM Plex Sans, IBM Plex Mono,
and Source Serif 4, are under the SIL Open Font License 1.1 (`OFL.txt`).
