# HYDRAULIC MODELS

Variably saturated flow through a deforming porous medium can be described by the mass balance equation:

$$
S\boldsymbol{m}^\mathrm{T}\frac{\partial \boldsymbol{\varepsilon}}{\partial t} + \frac{e}{1+e}\left(\frac{\partial S}{\partial t} + \frac{S}{K_w}\frac{\partial p_w}{\partial t}\right) + \nabla^\mathrm{T}\boldsymbol{v} = 0
$$

which is to be supplemented with the usual mechanical governing equation (momentum balance and strain-displacement relations) and the generalized Darcy’s law:

$$
\boldsymbol{v} = -K_r\boldsymbol{K}\nabla h_s = -K_r\boldsymbol{K}\nabla \left(\frac{p_w}{\gamma_w}+z\right)
$$

where:

- $$\boldsymbol{\varepsilon}$$ = Strain
- $$\boldsymbol{m} = (1,1,1,0,0,0)^\mathrm{T}$$, making $$\boldsymbol{m}^\mathrm{T}\boldsymbol{\varepsilon}$$ the volumetric strain
- $$K_w$$ = Bulk modulus of water (= 2,200 MPa)
- $$e$$ = Void ratio
- $$S$$ = Degree of saturation
- $$\boldsymbol{v} = (v_x,v_y,v_z)^\mathrm{T}$$ = Fluid velocity [m/s]
- $$\boldsymbol{K}$$ = Saturated hydraulic conductivity modulus [m/s]
- $$K_r$$ = Relative hydraulic conductivity (a function of degree of saturation)
- $$z$$ = Vertical coordinate
- $$\gamma_w$$ = Unit weight of water (= 9.8 kN/m³)
- $$p_s$$ = Pressure [kN/m²]
- $$h_s = p_s/\gamma_w + z$$ = Head

---

In OPTUM GX, the effects of deformation as a result of seepage are neglected, making the governing equation:

$$
\frac{e}{1+e}\left(\frac{\partial S}{\partial t} + \frac{S}{K_w}\frac{\partial p_s}{\partial t}\right) = \nabla^\mathrm{T}\left[K_r\boldsymbol{K}\nabla \left(\frac{p_s}{\gamma_w}+z\right)\right]
$$

Typical values of hydraulic conductivity for different materials are shown in Figure ref:hydrtable.

![Typical values of hydraulic conductivity $$K=K_x=K_y=K_z$$](./images/hydrtable.png)

---

Besides the constants $$n$$ and $$\boldsymbol{K}$$, the solution of this equation requires the **relative hydraulic conductivity relation** and the **saturation-pressure relation** (also known as the water retention curve or the soil water characteristic curve).

In OPTUM GX, the saturated hydraulic conductivity modulus is always given by:

$$
\boldsymbol{K} =
\begin{bmatrix}
K_x &  &  \\
 & K_y &  \\
 &  & K_z
\end{bmatrix}
$$

where $$K_x$$, $$K_y$$, and $$K_z$$ are the saturated hydraulic conductivities in the $$x$$, $$y$$, and $$z$$ directions, respectively.

---

## van Genuchten Model

The van Genuchten model is the most widely used hydraulic model in soil science. It relates degree of saturation to pressure head by:

$$
S =
\begin{cases}
S_r + (S_s - S_r)\left(1 + |\alpha \hat{h}|^n\right)^{-m} & \text{for } \hat{h} \le 0 \\
S_s & \text{for } \hat{h} > 0
\end{cases}
$$

where $$\hat{h} = -p/\gamma_w$$, $$m = 1 - 1/n$$, and:

- $$S_r$$ = Residual degree of saturation (may be slightly greater than 0)
- $$S_s$$ = Fraction of water-filled pores at full saturation (may be slightly less than 1)
- $$\alpha$$ [m⁻¹] = Model parameter related to air entry pressure
- $$n$$ = Model parameter related to the rate at which water is extracted from the soil once the air entry pressure has been exceeded

---

The relative hydraulic conductivity is related to the effective saturation $$S_e$$ as:

$$
K_r =
\begin{cases}
S_e^{1/2}\left[1 - \left(1 - S_e^{1/m}\right)^m\right]^2 & \text{for } S_e < 1 \\
1 & \text{for } S_e = 1
\end{cases}
$$

where

$$
S_e = \frac{S - S_r}{S_s - S_r}
$$

Alternatively, $$K_r$$ can be expressed in terms of $$\hat{h}$$ as:

$$
K_r =
\begin{cases}
\displaystyle\frac{\left[1 - |\alpha \hat{h}|^{n-1}\left(1 + |\alpha \hat{h}|^n\right)^{-m}\right]^2}{\left(1 + |\alpha \hat{h}|^n\right)^{m/2}} & \text{for } \hat{h} \le 0 \\
1 & \text{for } \hat{h} > 0
\end{cases}
$$

Typical values of the parameters $$n$$ and $$\alpha$$ are given in the table below, and typical retention and relative hydraulic conductivity curves are shown in Figure ref:vgfig3.

| Material        | No. of Samples | Clay Content Min | Clay Content Max | $$n_{min}$$ | $$n_{max}$$ | $$\alpha_{min}$$ (m⁻¹) | $$\alpha_{max}$$ (m⁻¹) |
| --------------- | -------------- | ---------------- | ---------------- | ----------- | ----------- | ---------------------- | ---------------------- |
| Sand            | 2              | 14               | 18               | 2.22        | 2.56        | 2.74                   | 2.65                   |
| Loamy sand      | 10             | 23               | 108              | 1.33        | 2.56        | 4.41                   | 2.35                   |
| Sandy loam      | 11             | 70               | 178              | 1.12        | 2.38        | 4.90                   | 1.27                   |
| Sandy clay loam | 15             | 208              | 349              | 1.06        | 1.85        | 3.92                   | 1.47                   |
| Loam            | 7              | 122              | 260              | 1.23        | 1.96        | 4.90                   | 1.76                   |
| Silt loam       | 5              | 120              | 270              | 1.14        | 1.25        | 9.60                   | 1.47                   |
| Silty clay loam | 8              | 280              | 390              | 1.14        | 1.43        | 8.82                   | 0.98                   |
| Clay loam       | 6              | 304              | 348              | 1.05        | 1.64        | 4.90                   | 0.78                   |
| Sandy clay      | 5              | 352              | 421              | 1.10        | 1.49        | 4.90                   | 1.76                   |
| Silty clay      | 2              | 420              | 460              | 1.09        | 1.10        | 6.37                   | 5.39                   |
| Clay            | 1              | 452              | 452              | 1.51        | 1.51        | 0.88                   | 0.88                   |

_Table: Soil properties of 72 samples and fitted van Genuchten model parameters_ ([after Ghan et al., 2010]).

![Dependence of $$S(\hat{h})$$ and $$K_r(\hat{h})$$ on $$\alpha$$ (top) and $$n$$ (bottom)](./images/vgfig3.png)

---

## Basic Model

The **Basic model**, which is the default model for all materials, is a van Genuchten model with parameters:

$$
\alpha = 4, \quad n = 4, \quad S_r = 0, \quad S_s = 1, \quad e = 1
$$

This gives a relatively steep pressure-saturation curve corresponding to a very coarse material.

