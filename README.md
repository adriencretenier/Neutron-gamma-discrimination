# Neutron–Gamma Discrimination Using Two Complementary Methods

**Adrien Creténier & Louis Hardouin**
NPAC Master's programme (Nuclear, Particle, Astroparticle physics and Cosmology), Université Paris-Saclay — Lab project, academic year 2024–2025
Experiment carried out at CEA Paris-Saclay (Orme des Merisiers) over one month

---

## Overview

A ²⁵²Cf source emits both fast neutrons and γ rays through spontaneous fission. Both are neutral particles and both produce light in an organic scintillator, so telling them apart is a classic problem in nuclear instrumentation.

In this project we discriminated neutrons from γ rays with two independent techniques, then compared them event by event:

1. **Time of Flight (ToF)** — a BaF₂ inorganic scintillator detects the prompt fission γ ray (start signal), and an NE213 liquid organic scintillator placed 1.1 m away detects the slower neutron (stop signal).
2. **Pulse Shape Discrimination (PSD)** — in the NE213 alone, neutron-induced pulses have a longer slow-decay tail than γ-induced pulses, so the ratio of tail charge to total charge identifies the particle.

This is a training project: the experiment reproduces a well-established measurement and does not aim at new results. Its value lies in building the full chain — detector setup, calibration, acquisition, data analysis, and a critical comparison of two methods.

## Repository contents

| File | Description |
|---|---|
| `article.pdf` | Short paper (4 pages) presenting the setup, the analysis and the discussion |
| `neutron_gamma_discrimination.ipynb` | Jupyter notebook containing the full data analysis |

## Experimental setup

- **Source:** ²⁵²Cf, activity 362 ± 4 kBq
- **γ detector (start):** BaF₂ scintillator + PMT, 2100 V, 10 cm from the source
- **Neutron / γ detector (stop):** NE213 liquid organic scintillator + PMT, 1100 V, 110 cm from the source
- **Electronics:** coincidence module generating 150 ns logic gates; waveforms digitised with MATACQ at 0.5 ns sampling over ~1 µs
- **Calibration:** detector operating points set with cosmic-muon coincidences; timing alignment and NE213 energy calibration (Compton edge, backscatter peak) with a ⁶⁰Co source

## Analysis (notebook)

The notebook processes about 45,000 recorded coincidences and covers:

- **Waveform processing:** baseline subtraction, peak finding, charge integration over the TOT, FAST and DELAYED windows
- **Time of flight:** ToF histogram, Gaussian fit of the γ peak, definition of a neutron region and an ambiguous region, conversion of ToF into neutron kinetic energy
- **Detector efficiency:** measured neutron spectrum divided by a Watt fission spectrum to extract the energy-dependent efficiency of the NE213
- **PSD:** DELAYED/TOT vs TOT scatter plot, optimisation of the integration windows by maximising the Figure of Merit
  $\mathrm{FOM} = |\mu_\gamma - \mu_n| / (\sigma_\gamma + \sigma_n)$
- **Background rejection:** removal of accidental coincidences (stray photons) using a DELAYED/TOT vs ToF diagram
- **Cross-validation:** event-by-event agreement between ToF and PSD in several energy bins

## Main results

- **PSD separation:** FOM = 2.26 ± 0.01 with the optimised DELAYED window (33.5–360 ns after the signal falls below 20 % of its maximum), versus 1.94 ± 0.02 for the FAST/TOT method.
- **Agreement between methods** improves with deposited energy and exceeds 99 % for both particles above 0.63 MeVee:

  | Energy (MeVee) | Neutrons (%) | γ rays (%) |
  |---|---|---|
  | 0.28 – 0.45 | 93.9 ± 0.8 | 98.6 ± 0.2 |
  | 0.45 – 0.63 | 97.7 ± 0.5 | 98.8 ± 0.3 |
  | 0.63 – 0.80 | 99.2 ± 0.4 | 99.2 ± 0.3 |
  | 0.80 – 1.32 | 99.6 ± 0.2 | 99.4 ± 0.3 |

- **Neutron counting:** 3478 ± 59 neutrons detected in 40 min, compatible with the expected (4.9 ± 1.1) × 10³ within 1.3 standard deviations.
- **Complementarity:** ToF is most reliable for low-energy neutrons (long flight times), while PSD identifies the high-energy neutrons (8–12 MeV) whose flight times overlap with the γ peak.

## Limitations

- A systematic timing offset of 17 ± 4 ns was observed between measured and expected ToF values, most likely introduced by chaining two coincidence-module channels. The peak *separation* (50 ± 4 ns measured vs 51 ± 1 ns expected) is unaffected.
- The BaF₂ detector is noisy, producing accidental starts that had to be removed in the analysis.
- PSD becomes less reliable below ~0.5 MeVee.

## Possible extensions

- Train a neural network on waveforms labelled by ToF to discriminate neutrons and γ rays automatically.
- Repeat the measurement with a single coincidence channel to remove the timing offset.

## Requirements

Python 3 with Jupyter, NumPy, SciPy and Matplotlib.

## Acknowledgements

We thank the NPAC teaching team and CEA Paris-Saclay for access to the equipment and their guidance throughout the project.
