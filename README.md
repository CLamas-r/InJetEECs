# In-jet heavy-quark energy–energy correlators in proton–nucleus collisions

## Overview

This directory contains numerical notebooks and figures for the heavy-quark-pair
contribution to the in-jet energy–energy correlator (EEC) in proton–nucleus
collisions. The calculation considers a gluon from the projectile proton
scattering from a small-x target and producing a heavy quark–antiquark pair.
Proton and nuclear targets are described using GBW and MV-type dipole models.

The notebooks compare RHIC and LHC kinematics and two normalization choices:
the rate of jets containing the heavy pair and the leading-order (LO) gluon-jet
rate. They provide numerical results within the approximations specified below.
All three notebooks contain their own solver and can be executed independently.
The included notebooks retain their executed outputs.

## Included files

| File | Description |
| --- | --- |
| `in_jet_eec_gbw_mv.ipynb` | LHC baseline calculation with interchangeable GBW/MV dipoles, transverse-momentum and nuclear-scale scans, and numerical diagnostics. |
| `in_jet_eec_rhic_comparison.ipynb` | EEC per pair-containing jet; RHIC scans, LHC reference and matched-energy controls, scale diagnostics, and numerical checks. |
| `in_jet_eec_gluon_normalization.ipynb` | Comparison of pair-jet and LO gluon-jet normalization; adjoint-dipole checks and nuclear modification of the pair rate per gluon jet. |
| `eec_results/` | Saved LHC tables, diagnostics, metadata, and the figures `eec_and_nuclear_modification.png`, `parameter_scans.png`, and `dipole_models.png`. |
| `rhic_eec_comparison.png` | Proton and nuclear EECs at RHIC and their ratios, with the previous LHC bin as a reference. |
| `matched_energy_controls.png` | Collision-energy comparison at fixed jet momentum, rapidity, and target mass number. |
| `normalization_comparison.png` | Nuclear ratios with the pair-jet and LO gluon-jet denominators. |
| `unchanged_angular_shape.png` | Ratios rescaled to their value at angular separation 0.1, illustrating the common angular shape for the two denominators. |

The four top-level PNG files and the LHC figures in `eec_results/` are reference outputs. Re-execution writes regenerated
figures and numerical tables into the output directories described below.

## Definitions and conventions

All momenta and masses are in GeV; transverse coordinate distances are in
GeV inverse. Positive jet rapidity is the proton-going direction. The jet
transverse momentum is denoted by $P=p_T$, the angular separation by $R_L$,
and the angular acceptance by $0<R_L<R_J$.

For the heavy-quark momentum fraction $z$, define $b=z(1-z)$ and

$$
\boldsymbol p_1=z\boldsymbol P+\boldsymbol k,
\qquad
\boldsymbol p_2=(1-z)\boldsymbol P-\boldsymbol k,
\qquad
|\boldsymbol k|=bP R_L.
$$

The final relation is the leading-power angular approximation used in the
notebooks. The energy weight for the single heavy-quark–antiquark pair is
$b$. The default longitudinal integration covers $0<z<1$.
The projectile and target momentum fractions are evaluated at the fixed jet bin:

$$
x_p=\frac{P e^{y_J}}{\sqrt{s_{NN}}},
\qquad
x_t=\frac{P e^{-y_J}}{\sqrt{s_{NN}}}.
$$

### EEC per pair-containing jet

For target $X=p,A$, let $\mathcal I_X(P,k;z)$ denote the transverse convolution
of the combined splitting kernel with the product of two fundamental dipoles,
including the azimuthal integral over $\boldsymbol k$. The implemented EEC is

$$
C_X^{\mathrm{pair}}(R_L)=
\frac{
\Theta(R_J-R_L)R_L\int_0^1 dz\,b^3
\mathcal I_X(P,bP R_L;z)
}{
\int_0^{R_J}dR'\,R'\int_0^1 dz\,b^2
\mathcal I_X(P,bP R';z)
}.
$$

The energy weight is included inside the $z$ integral. The denominator is the
unweighted pair-containing jet cross section with the same angular acceptance.
The EEC integrates to the mean pair energy weight,
$\int_0^{R_J}dR_L\,C_X^{\mathrm{pair}}=\langle b\rangle_X$, rather than unity.
The nuclear ratio is

$$
R_{pA}^{\mathrm{pair}}(R_L)=
\frac{C_A^{\mathrm{pair}}(R_L)}{C_p^{\mathrm{pair}}(R_L)}.
$$

Common coupling, projectile-PDF, target-area, and fixed-bin factors cancel
within each conditional EEC under the implemented approximations.
There is no additional factor $1/A$ in this ratio.

The convolution uses the positive combined kernel

$$
K(\boldsymbol k,\boldsymbol\ell;z)=\frac12\left[
m_Q^2\left(\frac{1}{k^2+m_Q^2}-\frac{1}{\ell^2+m_Q^2}\right)^2
+\bigl(z^2+(1-z)^2\bigr)
\left|\frac{\boldsymbol k}{k^2+m_Q^2}
-\frac{\boldsymbol\ell}{\ell^2+m_Q^2}\right|^2
\right].
$$

The transverse integration variable in the implementation is
$\boldsymbol q$, with
$\boldsymbol\ell=\boldsymbol k+z\boldsymbol P-\boldsymbol q$ and dipole
product $F_{F,X}(q)F_{F,X}(|\boldsymbol P-\boldsymbol q|)$.

### LO gluon-jet normalization

Let $W_X(R_L)$ be the weighted differential pair cross section, $D_X$ its
unweighted cross section integrated over the jet acceptance, and $G_X$ the LO
gluon-jet cross section in the same infinitesimal momentum and rapidity bin.
Then

$$
C_X^{g}(R_L)=\frac{W_X(R_L)}{G_X}
=f_X C_X^{\mathrm{pair}}(R_L),
\qquad f_X=\frac{D_X}{G_X},
$$

$$
R_{pA}^{g}(R_L)=\frac{f_A}{f_p}R_{pA}^{\mathrm{pair}}(R_L).
$$

The factor $f_A/f_p$ is independent of $R_L$ at fixed jet kinematics and cuts.
This normalization retains the nuclear modification of pair production per
gluon jet and preserves the logarithmic angular slope of the ratio.

The gluon denominator uses the adjoint dipole. Consistently with the
large-$N_c$, factorized treatment of the pair numerator,

$$
S_{\mathrm{adj},X}(r)=S_{F,X}(r)^2,
\qquad
F_{\mathrm{adj},X}(P)=
\int d^2q\,F_{F,X}(q)F_{F,X}(|\boldsymbol P-\boldsymbol q|).
$$

The gluon-normalization notebook computes the nuclear ratios and $f_A/f_p$.
Its `reduced_W_*` and `reduced_D_*` exports omit common cross-section
prefactors. They are reduced integrals, not absolute EECs, absolute pair
probabilities, or event yields. The physical gluon-normalized pair EEC starts
at $O(\alpha_s)$; the common coupling cancels in its nuclear ratio.

## Dipole models and parameters

The Fourier-transform convention is

$$
F_{F,X}(q)=\int\frac{d^2r}{(2\pi)^2}
e^{-i\boldsymbol q\cdot\boldsymbol r}S_{F,X}(r).
$$

The implemented models are

$$
S_F^{\mathrm{GBW}}(r)=e^{-r^2Q_s^2/4},
\qquad
F_F^{\mathrm{GBW}}(q)=\frac{e^{-q^2/Q_s^2}}{\pi Q_s^2},
$$

$$
S_F^{\mathrm{MV}}(r)=
\exp\left[-\frac{r^2Q_s^2}{4}
\ln\left(e+\frac{1}{r\Lambda_{\mathrm{MV}}}\right)\right].
$$

The MV Fourier transform is evaluated numerically. Both models use the same
GBW-based estimate of the input scale:

$$
Q_{s,p}^2(x_t)=Q_{s,0}^2\left(\frac{x_0}{x_t}\right)^{\lambda_s},
\qquad
Q_{s,A}^2(x_t)=cA^{1/3}Q_{s,p}^2(x_t).
$$

| Parameter | Default value |
| --- | --- |
| Heavy-quark mass $m_Q$ | 1.3 GeV |
| Angular acceptance $R_J$ | 0.6 |
| Nuclear enhancement coefficient $c$ | 0.75 |
| Proton scale $Q_{s,0}^2$ | 1 GeV squared |
| Reference fraction $x_0$ | $3.04\times10^{-4}$ |
| Exponent $\lambda_s$ | 0.29 |
| MV infrared parameter $\Lambda_{\mathrm{MV}}$ | 0.2 GeV |
| Minimum $z$ cut | 0 |

The reported operational scale satisfies $S_F(2/Q_{\mathrm{op}})=e^{-1}$.
It is a diagnostic of the model profile and is distinct from the MV input
$Q_s$. In the adjoint prescription, both models use $Q_s\to\sqrt{2}Q_s$;
finite-$N_c$ Casimir scaling is not substituted into this approximation.

### Kinematic cases

| Case | $\sqrt{s_{NN}}$ [GeV] | $y_J$ | $p_T$ [GeV] | Target $A$ | Included in |
| --- | ---: | ---: | ---: | ---: | --- |
| RHIC | 200 | 2 | 5, 7.5, 10 | 197 (Au) | RHIC-comparison and gluon-normalization notebooks |
| LHC reference | 5020 | 3 | 25 | 208 (Pb) | All three notebooks |
| LHC momentum scan | 5020 | 3 | 15, 25, 40 | 208 (Pb) | LHC-baseline notebook |
| Matched-energy controls | 5020 | 2 | 5, 10 | 197 (Au) | RHIC-comparison notebook |

The 5020 GeV Au cases are theoretical controls that vary collision energy
while holding other inputs fixed. They do not identify an experimental Au run.
The LHC-baseline notebook also varies the nuclear coefficient over
$c=0.5,0.75,1.0$ at the reference jet momentum.

## Reproducing the calculation

The recorded execution environment uses Python 3.12.4 with NumPy 1.26.4,
SciPy 1.13.1, pandas 2.2.2, Matplotlib 3.8.4, IPython 8.25.0,
ipykernel 6.28.0, nbformat 5.9.2, nbclient 0.8.0, nbconvert 7.10.0,
and Notebook 7.0.8.

From this directory, create an environment and install these package versions:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install numpy==1.26.4 scipy==1.13.1 pandas==2.2.2 matplotlib==3.8.4 ipython==8.25.0 ipykernel==6.28.0 nbformat==5.9.2 nbclient==0.8.0 nbconvert==7.10.0 notebook==7.0.8
python -m ipykernel install --sys-prefix --name injet-eec --display-name "In-jet EEC"
python -m notebook
```

Open a notebook, select the **In-jet EEC** kernel, and execute all cells
in order. Each notebook is independent; there is no required execution order
between them. Run from the directory containing the notebooks so output paths
resolve consistently.

Alternatively, execute from the command line and save separate executed copies:

```bash
jupyter nbconvert --to notebook --execute --ExecutePreprocessor.kernel_name=injet-eec --ExecutePreprocessor.timeout=900 --output=in_jet_eec_gbw_mv.executed in_jet_eec_gbw_mv.ipynb
jupyter nbconvert --to notebook --execute --ExecutePreprocessor.kernel_name=injet-eec --ExecutePreprocessor.timeout=900 --output=in_jet_eec_rhic_comparison.executed in_jet_eec_rhic_comparison.ipynb
jupyter nbconvert --to notebook --execute --ExecutePreprocessor.kernel_name=injet-eec --ExecutePreprocessor.timeout=900 --output=in_jet_eec_gluon_normalization.executed in_jet_eec_gluon_normalization.ipynb
```

The execution timeout applies to each cell. Runtime depends on the machine.
The fixed seed provides reproducible sampling for a given numerical environment;
minor floating-point differences between platforms may remain.

## Numerical method and generated outputs

The default integration uses eight independently scrambled Sobol sequences
with $2^{18}$ points each, seed 260922, 48 Gauss–Legendre radial nodes,
and a 16384-point Hankel-transform grid for MV. The LHC-baseline angular scan
contains 65 logarithmically spaced angles from 0.008 to 0.6. The RHIC-comparison
and gluon-normalization notebooks add the exact points 0.1 and 0.3.
The LHC parameter scans use $2^{16}$ points per scramble, six scrambles,
40 radial nodes, and 45 displayed angles at the default settings.
The rate denominator integrates the full interval
$0<R_L<R_J$, including angles below the first displayed point.

GBW uses exact Gaussian sampling of the normalized dipole product. Its common
hard-momentum exponential cancels analytically before numerical evaluation.
MV uses a Fourier transform with Gaussian subtraction and importance sampling
over the full transverse plane. Numerical uncertainty is estimated from the
independent scrambles, with correlated sampling for the two targets.

The notebooks create the following directories relative to the working directory:

| Output directory | Contents |
| --- | --- |
| `eec_results/` | LHC EEC and ratio CSV tables, parameter-scan tables, three figures, scale and Fourier checks, disk and integration diagnostics, convergence tables, and run metadata. A saved copy is included. |
| `rhic_results/` | Case/model CSV tables, NPZ replicate arrays, the two RHIC figures, scale and Fourier checks, ratio decomposition, mass/disk diagnostics, convergence tables, and run metadata. |
| `gluon_normalization_results/` | Case/model CSV tables and NPZ arrays, the two normalization figures, rate-factor summaries, adjoint checks, convergence tables, and run metadata. |

Repeated execution replaces generated files with the same names in these
directories. The top-level reference PNG files remain available for comparison.
Numerical bands and exported errors describe integration uncertainty only.

To vary the calculation, edit `Physics` and `Numerics` in the first code cell.
The LHC-baseline notebook uses `MODEL` and `COMPARE_MODELS` to select models;
`RUN_PARAMETER_SCAN` and `RUN_CONVERGENCE` control its optional calculations.
In the RHIC-comparison and gluon-normalization notebooks, edit `CASES` to
select kinematic bins. Their scan and convergence cells explicitly iterate
over GBW and MV; those loops determine which models run. New dipoles can be registered in
`DIPOLE_MODELS` with the interface used by the supplied implementations.

Included checks cover kernel positivity and its zero at equal momenta,
an analytically solvable constant-kernel case, identical-target unity,
Fourier-transform normalization and direct quadrature, an independent
disk integration of the pair rate, and numerical refinement. The gluon
notebook additionally checks the adjoint convolution and the constant
multiplicative relation between the two nuclear ratios. Stored outputs
record successful execution of these checks.

## Scope and interpretation

The calculation retains the heavy-quark mass in the splitting kernel and
uses leading-power, massless-jet kinematics for momentum fractions, angular
mapping, and energy weights. Jet bins are infinitesimal. The angular acceptance
is the partonic pair cut implemented above; there is no detector simulation
or jet-clustering calculation.

The target treatment uses a factorized dipole product and the stated
large-$N_c$ adjoint prescription. The MV scale is a GBW-based estimate rather
than an independently fitted MV scale. BK/JIMWLK evolution, NLO corrections,
fragmentation, additional projectile channels, and matching to a dilute
reference are outside this implementation. The LO gluon denominator contains
only the gluon channel; an inclusive experimental jet denominator would also
require quark and antiquark channels.

The pair mass satisfies

$$
M_J^2=\frac{m_Q^2+k^2}{z(1-z)},
\qquad
\frac{M_J^2}{p_T^2}\geq\frac{4m_Q^2}{p_T^2}.
$$

The lower bounds are 0.2704, 0.1202, and 0.0676 at 5, 7.5, and 10 GeV.
The 5 GeV bin therefore requires particular care when applying the
leading-power approximation. These bounds and the exported mass diagnostics
are not estimates of a theoretical uncertainty.

At fixed jet kinematics, $x_t$ is constant across the angular scan; varying
$R_L$ changes the relative momentum. The dipole arguments also contain
the jet momentum, so a comparison of $k$ with $Q_s$ alone does not classify
the full convolution as saturated or dilute. A change in the conditional
EEC can arise from angular redistribution and from energy sharing. The
gluon normalization additionally retains changes in the pair rate per jet.
Differences between GBW and MV should be considered when interpreting a
nuclear modification as evidence for saturation.

## arXiv ancillary-file packaging

For a TeX/PDFLaTeX-source submission, place this README, the three notebooks,
the reference figures, and the supplied numerical outputs in an `anc/`
directory at the root of the submission archive. Preserve the `eec_results/`
subdirectory. Keep manuscript TeX sources outside `anc/`. The notebooks
use relative output paths and do not require an `anc/` prefix in their code.
This README describes the numerical material; manuscript compilation is
independent of notebook execution.

See the official [arXiv ancillary-file instructions](https://info.arxiv.org/help/ancillary_files.html)
for the submission procedure and supported submission types.

## Model references

- K. Golec-Biernat and M. Wüsthoff, *Saturation Effects in Deep Inelastic
  Scattering at low $Q^2$ and its Implications on Diffraction*,
  [arXiv:hep-ph/9807513](https://arxiv.org/abs/hep-ph/9807513).
- T. Lappi and H. Mäntysaari, *Single inclusive particle production at high
  energy from HERA data to proton–nucleus collisions*,
  [arXiv:1309.6963](https://arxiv.org/abs/1309.6963).

These references supply model and factorization context. The EEC scans in
this directory are produced by the included notebooks.
