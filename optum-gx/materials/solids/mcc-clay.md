# Modified Cam Clay

The critical state models developed by Roscoe and his co-workers (Roscoe, 1968; Schofield, 1968) in the 1960s have been widely applied in geomechanics and form the basis of many subsequent models. The Modified Cam Clay (MCC) model of Roscoe (1968) has been particularly popular. A slightly modified and extended version of this model (including creep and a finite cohesion, while prohibiting crossing of the critical state line) is implemented in GX.

---

## Summary of material parameters

### Stiffness
- **Parameter Set A**  
  - $$\kappa^*$$: modified swelling index  
  - $$\lambda^*$$: modified compression index  
- **Parameter Set B**  
  - $$C_s$$: conventional swelling index (approximate, see Section “Oedometric compression”)  
  - $$C_c$$: conventional compression index (approximate, see Section “Oedometric compression”)  
- $$\nu$$: Poisson’s ratio  

### Strength
- $$c'$$: cohesion  
- $$\phi'$$: friction angle  

### Initial Conditions
- **OCR**: overconsolidation ratio (see Section “Initial stresses and overconsolidation ratio”)  
- $$K_0$$: earth pressure at rest coefficient  
- $$e_0$$: initial void ratio (only used for Stiffness Parameter Set B)  

### Creep
- If creep is enabled: $$\mu^*/\lambda^*$$ — relative creep index  

---

## Governing equations

### Elasticity
The volumetric and deviatoric stress–strain relations are given by  
$$
\dot{\varepsilon}_v^e = \frac{1}{K}\dot p', \quad \varepsilon_q = \frac{1}{3G}\dot q
$$  

where  
$$
K = \frac{p'}{\kappa^*}, \quad G = \frac{3(1-2\nu)}{2(1+\nu)}K
$$  

with $$\kappa^*$$ being a material parameter (the modified swelling modulus). The general 3D elastic stress–strain relation is:  
$$
\dot{\boldsymbol{\varepsilon}} = \mathbb{C}^e \dot{\boldsymbol{\sigma}}
$$  
where $$\mathbb{C}^e$$ is given in the Elasticity section.

---

### Yield and failure surfaces

The yield function is:  
$$
F = q^2 - M^2 p'(p_c - p')
$$  
where $$p_c$$ (the preconsolidation pressure) functions as a hardening variable, and  
$$
M = \frac{3\sin\phi'}{\sqrt{3}\cos\theta + \sin\theta\sin\phi'}
$$  
where $$\phi'$$ is the friction angle and $$\theta$$ is the Lode angle.

![Modified Cam Clay yield surfaces cut off by failure (critical state) line \(q = Mp'\)](../../.gitbook/assets/mcc_yield.png)

The yield surface represents an ellipse in $$p'-q$$ space whose size is governed by $$p_c$$. The line $$q = Mp'$$ passes through its apex — the critical state line. In the current implementation, crossing this line is prohibited. The critical state line acts as a Mohr–Coulomb failure line:  
$$
F_f = |\sigma_1 - \sigma_3| + (\sigma_1 + \sigma_3)\sin\phi
$$

---

### Flow rules

For the yield surface (associated flow rule):  
$$
\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda}\frac{\partial F}{\partial \boldsymbol{\sigma}}
$$  
This implies compaction for all stress states on the yield surface, except at the top of the ellipse where $$\dot{\varepsilon}_v^p = 0$$.

For the failure surface (nonassociated flow rule):  
$$
\dot{\boldsymbol{\varepsilon}}^p_f = \dot{\lambda}_f\frac{\partial G_f}{\partial \boldsymbol{\sigma}}
$$  
where  
$$
G_f = |\sigma_1 - \sigma_3|
$$  
implying zero dilation.

---

### Hardening law

The change in $$p_c$$ is proportional to the plastic volumetric strain:  
$$
\dot p_c = \frac{p_c}{\lambda^* - \kappa^*}\dot{\varepsilon}_v^p
$$  
where $$\lambda^*$$ is the modified compression index. The yield surface expands ($$\dot p_c > 0$$) up to the critical state line ($$\dot p_c = 0$$).

---

### Cohesion

Cohesion is introduced by modifying the mean effective stress:  
$$
\tilde{p}' = -\frac{1}{3}(\sigma_x' + \sigma_y' + \sigma_z') + \frac{c'}{\tan\phi'}
$$

---

### Creep

For certain clays, creep contributes significantly to total deformation. The empirical law is:  
$$
\varepsilon_v^c = \frac{C_\alpha}{1+e}\log_{10}\left(\frac{t}{t_{90}}\right)
$$  
and more generally between times $$t_n$$ and $$t_{n+1}$$:  
$$
\Delta\varepsilon_v^c = \frac{C_\alpha}{1+e}\log_{10}\left(\frac{t_{n+1}}{t_n}\right)
$$  
For a layer of depth $$H$$, the vertical settlement due to creep is:  
$$
\Delta u^c = H\frac{C_\alpha}{1+e}\log_{10}\left(\frac{t_{n+1}}{t_n}\right)
$$  

In OPTUM GX, creep follows Borja (1985):  
$$
\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^e + \boldsymbol{\varepsilon}^p + \boldsymbol{\varepsilon}^c
$$  
with creep potential  
$$
\frac{d\Phi^c}{dt} = \frac{\mu^*}{\tau_0}\exp\left(-\frac{1}{\mu^*}\Phi^e\right), \quad \Phi(0)=0
$$  
and creep strain evolution  
$$
\frac{d\boldsymbol{\varepsilon}^c}{dt} = \boldsymbol{a}\frac{d\Phi^c}{dt}
$$  
where $$\boldsymbol{a} = \frac{\partial F^c}{\partial \boldsymbol{\sigma}'}$$ and  
$$
F^c = \tilde{p}' + \frac{q^2}{M^2\tilde{p}'}
$$  
Typically $$\mu^*/\lambda^*$$ ranges from 0.02–0.1 for natural materials prone to creep.

For 1D conditions:  
$$
\varepsilon_v^c = \mu^*\ln\left(\frac{t + \tau_0}{\tau_0}\right)
$$  
and  
$$
\Delta\varepsilon_v^c = \mu^*\ln\left(\frac{t + \tau_0}{t_{90} + \tau_0}\right)
$$  
which approaches the empirical form for $$t \gg \tau_0 = 1$$ day.

---

## Initial stresses and overconsolidation ratio

The overconsolidation ratio is:  
$$
\text{OCR} = \frac{\sigma_{v,0}'}{\sigma_{c,0}}
$$  
In the oedometer test (1D), the stresses at yield are:  
$$
\begin{aligned}
\sigma_x'{}^* &= \sigma_{x,0}' + (\text{OCR} - 1)\frac{\nu}{1 - \nu}\sigma_{z,0}' \\
\sigma_y'{}^* &= \sigma_{y,0}' + (\text{OCR} - 1)\frac{\nu}{1 - \nu}\sigma_{z,0}' \\
\sigma_z'{}^* &= \text{OCR}\,\sigma_{z,0}' \\
\tau_{xy}^* &= \tau_{xy,0}, \quad
\tau_{yz}^* = \tau_{yz,0}, \quad
\tau_{zx}^* = \tau_{zx,0}
\end{aligned}
$$  

The corresponding preconsolidation pressure:  
$$
p_{c,0} = \tilde{p}'{}^* + \frac{q^{*2}}{M^2 \tilde{p}'{}^*}
$$  

---

## Isotropic compression

For isotropic compression ($$\sigma_1' = \sigma_2' = \sigma_3' = p'$$), before yield:  
$$
\dot{\varepsilon}_v = \frac{\kappa^*}{p'}\dot{p}'
$$  
At yield ($$p' = p_c$$):  
$$
\dot{\varepsilon}_v = \frac{\lambda^*}{p'}\dot{p}'
$$  
Thus:  
$$
\frac{d\varepsilon_v}{dp'} =
\begin{cases}
\frac{\kappa^*}{p'}, & p' < p_c \\
\frac{\lambda^*}{p'}, & p' = p_c
\end{cases}
$$  

![Normal compression line (NCL) and unloading–reloading line (URL) in \(\ln p'-\varepsilon_v\) space (left) and idealized oedometric response in \(\log\sigma_v'-e\) space.](../../.gitbook/assets/sscc3_NEW4.png)

---

## Oedometric compression

In the oedometer test, all strains except the vertical are zero. The result is a bilinear relation:  
$$
\frac{de}{d\log_{10}\sigma_v'} =
\begin{cases}
C_s, & \sigma_v' < \sigma_c \\
C_c, & \sigma_v' = \sigma_c
\end{cases}
$$  
where  
$$
e = (1 + e_0)(1 - \varepsilon_v) - 1
$$  
and approximate conversions are:  
$$
\begin{aligned}
\kappa^* &\approx \frac{C_s}{2.3(1 + e_0)} \\
\lambda^* &\approx \frac{C_c}{2.3(1 + e_0)}
\end{aligned}
$$  

In OPTUM GX, the user has a choice between two parameter sets: A ($$\kappa^*, \lambda^*$$) or B ($$C_s, C_c$$); In the case of Set B, the above relations are used to calculate equivalent $$\kappa^*$$ and $$\lambda^*$$.
