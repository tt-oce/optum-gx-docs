# Notation

In this section, a number of frequently used quantities are defined.

## Stress

The stress vector $$\boldsymbol{\sigma}$$  is given by:

$$
\begin{array}{lcl}
\boldsymbol{\sigma} = (\sigma_x,\sigma_y,\sigma_z,\tau_{xy},\tau_{yz},\tau_{zx})^\mathrm{T} & & \textsf{(3D)}\\
\boldsymbol{\sigma} = (\sigma_x,\sigma_y,\sigma_z,\tau_{xy})^\mathrm{T} & & \textsf{(plane strain)}\\
\boldsymbol{\sigma} = (\sigma_x,\sigma_y,\sigma_\theta,\tau_{xy})^\mathrm{T} & & \textsf{(axisymmetry)}
\end{array}
$$

The conventional sign convention of continuum mechanics (compression taken as negative) is used throughout. The principal stresses are ordered as:

$$
\sigma_1\leq \sigma_2 \leq\sigma_3
$$

For problems dominated by compression, $\sigma\_1$ will usually be the numerically largest principal stress.\
The mean stress, noting the sign convention, is given by:

$$
p = -\frac{1}{3}(\sigma_x+\sigma_y+\sigma_z) = -\frac{1}{3}(\sigma_1+\sigma_2+\sigma_3)
$$

A related quantity, the modified mean stress, is defined as:

$$
\tilde p = p + c/\tan\phi
$$

where $c$ and $\phi$ are the Mohr-Coulomb cohesion and friction angle respectively.\
The deviatoric stress is given by

$$
q= \sqrt{\frac{1}{2}(\sigma_x-\sigma_y)^2+\frac{1}{2}(\sigma_y-\sigma_z)^2+\frac{1}{2}(\sigma_z-\sigma_x)^2+3\tau_{xy}^2+3\tau_{yz}^2+3\tau_{zx}^2}
$$

Under triaxial conditions, $\sigma\_z=\sigma\_1$, $\sigma\_x=\sigma\_y=\sigma\_3$, $\tau\_{xy}=\tau\_{yz}=\tau\_{zx}=0$, the mean and deviatoric stresses reduce to:

$$
p=-\frac{1}{3}(\sigma_1+2\sigma_3),\quad q= |\sigma_1-\sigma_3|
$$

The Lode angle is given by

$$
\theta = \arctan\left[\frac{1}{\sqrt 3}\left(\frac{\sigma_2-\sigma_3}{\sigma_1-\sigma_3}-1\right)\right]
$$

This angle varies between $-30^\circ$ corresponding to triaxial compression and $+30^\circ$ corresponding to triaxial extension.

## Effective stress

The effective stress is given by

$$
\boldsymbol{\sigma}' = \boldsymbol{\sigma}+\boldsymbol{m}p_w
$$

where $m=(1,1,1,0,0,0)^\mathrm{T}$ and $p\_w$ is the fluid pressure. This is made up of a seepage pressure and possibly an excess pore pressure:

$$
p_w = p_s + p_e
$$

where $p\_s$ is the seepage pressure (steady-state or transient) and $p\_e$ is the excess pore pressure generated in response to deformation for the relevant analysis types and Drainage settings. It is noted that while stresses follow the standard continuum mechanics sign conventions (negative in compression), the opposite convention is used for fluid pressures.

## Strain

The strain vector $\boldsymbol{\varepsilon}$ is given by:

$$$
\begin{array}{lcl}
\boldsymbol{\varepsilon} = (\varepsilon_x,\varepsilon_y,\varepsilon_z,\tau_{xy},\tau_{yz},\tau_{zx})^\mathrm{T}& & \textsf{(3D)}\\
\boldsymbol{\varepsilon} = (\varepsilon_x,\varepsilon_y,\varepsilon_z,\tau_{xy})^\mathrm{T}& & \textsf{(plane strain)}\\
\boldsymbol{\varepsilon} = (\varepsilon_x,\varepsilon_y,\varepsilon_\theta,\tau_{xy})^\mathrm{T}& & \textsf{(axisymmetry)}
\end{array}$$

The conventional continuum mechanics sign convention (strains negative in contraction) is used throughout. The principal
stresses are ordered as:
$$$

\varepsilon\_1\leq \varepsilon\_2 \leq\varepsilon\_3

$$
For problems dominated by compression, $\varepsilon_1$ will usually be the numerically largest principal strain.

The volumetric strain is given by
$$

\varepsilon\_v = \varepsilon\_x+\varepsilon\_y+\varepsilon\_z = \varepsilon\_1+\varepsilon\_2+\varepsilon\_3

$$
The deviatoric strain is given by
$$

\varepsilon\_q=\frac{2}{3}\sqrt{\frac{1}{2}(\varepsilon\_x-\varepsilon\_y)^2+\frac{1}{2}(\varepsilon\_y-\varepsilon\_z)^2+\frac{1}{2}(\varepsilon\_z-\varepsilon\_x)^2+\frac{3}{4}\gamma\_{xy}^2+\frac{3}{4}\gamma\_{yz}^2+\frac{3}{4}\gamma\_{zx}^2}

$$
A related quantity, often referred to as just the shear strain, is given by
$$

\gamma=\frac{3}{2}\varepsilon\_q

$$
Under triaxial conditions, $\varepsilon_z=\varepsilon_1$, $\varepsilon_x=\varepsilon_y=\varepsilon_3$,
$\tau_{xy}=\tau_{yz}=\tau_{zx}=0$, the volumetric and deviatoric strains reduce to:
$$

\varepsilon\_v=\varepsilon\_1+2\varepsilon\_3,\quad \varepsilon\_q= \frac{2}{3}|\varepsilon\_1-\varepsilon\_3|

$$
### Strain types

A basic premise of classic plasticity theory is the additive decomposition of the total strain into elastic and inelastic components. In GX, two types of inelastic strain are relevant: plastic strains and creep strains. The total strain is thus:
$$

\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^e + \boldsymbol{\varepsilon}^p + \boldsymbol{\varepsilon}^c

$$
where
$$

\begin{array}{lcl} \boldsymbol{\varepsilon}^e & = & \textsf{elastic strains}\ \boldsymbol{\varepsilon}^p & = & \textsf{plastic strains}\ \boldsymbol{\varepsilon}^c & = & \textsf{creep strains} \end{array}
