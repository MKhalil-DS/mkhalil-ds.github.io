---
permalink: /research/
title: "My Physics Research"
author_profile: true
---

![Gravitational waves from binary black holes](/images/research/Gravitational-Waves.jpg "Gravitational Waves Simulation")

*Gravitational waves (GWs)* were first detected by [LIGO in 2015](https://www.ligo.caltech.edu/news/ligo20160211), and since then, over a hundred events have been observed by a global network of four detectors comprising the LIGO-Virgo-KAGRA collaboration. These observations have provided valuable insights into binary black holes and neutron stars, helping us understand their properties and how they form.

Detecting GW signals is challenging because they are usually weaker than the background noise. To identify these signals, we match the data to a waveform template bank that covers the expected parameter space for compact binaries. More accurate waveforms lead to better detections and parameter inference.

The most accurate waveforms come from numerical relativity (NR) simulations, but these are computationally expensive, which makes them impractical to cover the entire parameter space. Therefore, it is crucial to complement NR results by accurate analytical waveform models that are computationally efficient.

My [research](https://scholar.google.com/citations?hl=en&user=eukGPR4AAAAJ&view_op=list_works&sortby=pubdate) focused on improving the accuracy of gravitational waveforms through the following complementary directions: 
1. extending analytical approximation methods for binary dynamics to higher orders,
2. developing accurate effective-one-body waveform models, and
3. identifying some signatures of modified gravity theories on GWs.


Analytical Approximation Methods
===================
Three main approximation methods are used for modeling the dynamics of binary systems and their GW emissions: 

1. *The post-Newtonian (PN) approximation* is an expansion in small velocities and large separations, making it suitable for comparable-mass binaries in bound orbits.

2. *The post-Minkowskian (PM) approximation* is an expansion in large separations, making it suitable for scattering encounters, since arbitrary velocities could be reached. 

3. *Gravitational self-force (GSF)* is an expansion in the small mass-ratio, making it suitable for intermediate and extreme mass-ratio inspirals.

![Analytical Approximation Methods: PN, PM, GSF](/images/research/PN-PM-SF.jpg "Analytical Approximation Methods")

I contributed to the derivation of several novel PN results for the conservative dynamics ([Antonelli+ 2020](https://arxiv.org/abs/2003.11391), [Antonelli+ 2020](https://arxiv.org/abs/2010.02018), [Khalil 2021](https://arxiv.org/abs/2110.12813), [Bautista+ 2024](https://arxiv.org/abs/2408.01871)), using an approach that combines PN, PM, and GSF methods.

In the dissipative dynamics, I calculated the spin contributions to the energy and angular momentum fluxes, as well as the waveform modes for both circular (to 3.5PN order in [Henry+ 2022](https://arxiv.org/abs/2209.00374)) and eccentric orbits (to 3PN order in [Henry & Khalil 2023](https://arxiv.org/abs/2308.13606)).

Effective-One-Body Waveform Models
================
![EOB map](/images/research/EOB_map_spin.jpg "EOB map")

Approximation methods can be combined with NR results to construct semi-analytic waveform models, such as the *effective-one-body(EOB) formalism*, which maps the binary motion to that of a test body in a deformed black hole background.

I contributed to the development of several EOB models, including the state-of-the-art models SEOBNRv5 ([Khalil+ 2023](https://arxiv.org/abs/2303.18143), [Pompili+ 2023](https://arxiv.org/abs/2303.18039), [Ramos-Buades+ 2023](https://arxiv.org/abs/2303.18046), [Gamboa+ 2024](https://arxiv.org/abs/2412.12823), [Gamboa+ 2024](https://arxiv.org/abs/2412.12831)), which are currently used by the LIGO-Virgo-KAGRA collaboration and other researchers to analyze GW events. The python code for the models is publicly available at [https://git.ligo.org/waveforms/software/pyseobnr](https://git.ligo.org/waveforms/software/pyseobnr).

![EOB precessing-spin waveform](/images/research/Precess_waveform_v5P.jpg)
*Example for a precessing-spin waveform showing showing excellent agreement between our model and NR simulations*

Modified Gravity Theories
================

To test gravity theories using GW observations, we need waveform models that can account for deviations from general relativity. 

I computed the effect on GWs of specific theories, such as Einstein-Maxwell-dilaton theory ([Khalil+ 2018](https://arxiv.org/abs/1809.03109)), and developed a theory-agnostic effective action approach to model scalarization ([Khalil+ 2019](https://arxiv.org/abs/1906.08161)), which is a non-perturbative phenomenon in several theories in which compact objects undergo a phase transition in the strong-field regime and acquire scalar charge.
This allowed us to quantify the effect of scalarization on binary dynamics and waveforms ([Khalil+ 2022](https://arxiv.org/abs/2206.13233)).

![EFT approach](/images/research/approach.jpg)
*An illustration of the theory-agnostic approach, which splits the fields of the full theory into small (UV) and long (IR) wavelength regimes, and integrate out the UV parts, effectively shrinking the compact object to a point whose action is an integral over a worldline.*
