# ELASTICITY

For elastic materials, the strains and effective stresses are related in a one-to-one manner — that is, the strains generated through loading along one stress path will be recovered when unloading along the same stress path.

Assuming linear elasticity, the relation between the strains and the effective stresses can be expressed as:

$$
\boldsymbol{\varepsilon}^e = \mathbb{C}^e \boldsymbol{\sigma}' \Longleftrightarrow \boldsymbol{\sigma}' = \mathbb{D}^e \boldsymbol{\varepsilon}^e
$$

where $$\mathbb{C}^e$$ is the **compliance modulus** and $$\mathbb{D}^e$$ is the **stiffness modulus**.

---

## Isotropic Elasticity

The most common assumption regarding the stiffness of geomaterials is **isotropy**, i.e., that the properties are the same in all directions (vertically and horizontally).

In this case, the compliance and stiffness moduli, related in a one-to-one manner, may be expressed either in terms of **Young's modulus** $$E$$ and **Poisson's ratio** $$\nu$$, or in terms of **bulk modulus** $$K$$ and **shear modulus** $$G$$.

The compliance modulus is given by:

$$
\mathbb{C}^e = \frac{1}{E}
\begin{bmatrix}
1 & -\nu & -\nu &  &  &  \\
-\nu & 1 & -\nu &  &  &  \\
-\nu & -\nu & 1 &  &  &  \\
 &  &  & 2(1+\nu) &  &  \\
 &  &  &  & 2(1+\nu) &  \\
 &  &  &  &  & 2(1+\nu)
\end{bmatrix}
$$

or equivalently,

$$
\mathbb{C}^e =
\begin{bmatrix}
\frac{1}{9}K^{-1}+\frac{1}{3}G^{-1} & \frac{1}{9}K^{-1}-\frac{1}{6}G^{-1} & \frac{1}{9}K^{-1}-\frac{1}{6}G^{-1} &  &  &  \\
\frac{1}{9}K^{-1}-\frac{1}{6}G^{-1} & \frac{1}{9}K^{-1}+\frac{1}{3}G^{-1} & \frac{1}{9}K^{-1}-\frac{1}{6}G^{-1} &  &  &  \\
\frac{1}{9}K^{-1}-\frac{1}{6}G^{-1} & \frac{1}{9}K^{-1}-\frac{1}{6}G^{-1} & \frac{1}{9}K^{-1}+\frac{1}{3}G^{-1} &  &  &  \\
 &  &  & G^{-1} &  &  \\
 &  &  &  & G^{-1} &  \\
 &  &  &  &  & G^{-1}
\end{bmatrix}
$$

where

$$
K = \frac{E}{3(1-2\nu)}, \quad G = \frac{E}{2(1+\nu)}
$$

---

The stiffness modulus is given by:

$$
\mathbb{D}^e = \frac{E}{(1+\nu)(1-2\nu)}
\begin{bmatrix}
1-\nu & \nu & \nu &  &  &  \\
\nu & 1-\nu & \nu &  &  &  \\
\nu & \nu & 1-\nu &  &  &  \\
 &  &  & \frac{1}{2}(1-2\nu) &  &  \\
 &  &  &  & \frac{1}{2}(1-2\nu) &  \\
 &  &  &  &  & \frac{1}{2}(1-2\nu)
\end{bmatrix}
$$

or equivalently,

$$
\mathbb{D}^e =
\begin{bmatrix}
K+\frac{4}{3}G & K-\frac{2}{3}G & K-\frac{2}{3}G &  &  &  \\
K-\frac{2}{3}G & K+\frac{4}{3}G & K-\frac{2}{3}G &  &  &  \\
K-\frac{2}{3}G & K-\frac{2}{3}G & K+\frac{4}{3}G &  &  &  \\
 &  &  & G &  &  \\
 &  &  &  & G &  \\
 &  &  &  &  & G
\end{bmatrix}
$$

---

### Relation Between Elastic Parameters

| Given Parameters | $$E =$$              | $$\nu =$$            | $$K =$$                 | $$G =$$                |
| ---------------- | -------------------- | -------------------- | ----------------------- | ---------------------- |
| $$(E, \nu)$$     | $$E$$                | $$\nu$$              | $$\frac{E}{3(1-2\nu)}$$ | $$\frac{E}{2(1+\nu)}$$ |
| $$(K, G)$$       | $$\frac{9KG}{3K+G}$$ | $$K - \frac{2G}{3}$$ | $$K$$                   | $$G$$                  |

_Table: Relation between elastic parameters._

---

## Undrained Conditions

Under **undrained conditions**, the relation between the elastic strains and the total pressures can be shown to be:

$$
\boldsymbol{\varepsilon}^e = \mathbb{C}^e_u \boldsymbol{\sigma}
$$

where

$$
\mathbb{C}^e_u = \frac{1}{E_u}
\begin{bmatrix}
1 & -\tfrac{1}{2} & -\tfrac{1}{2} &  &  &  \\
-\tfrac{1}{2} & 1 & -\tfrac{1}{2} &  &  &  \\
-\tfrac{1}{2} & -\tfrac{1}{2} & 1 &  &  &  \\
 &  &  & 3 &  &  \\
 &  &  &  & 3 &  \\
 &  &  &  &  & 3
\end{bmatrix}
= \frac{1}{3G}
\begin{bmatrix}
1 & -\tfrac{1}{2} & -\tfrac{1}{2} &  &  &  \\
-\tfrac{1}{2} & 1 & -\tfrac{1}{2} &  &  &  \\
-\tfrac{1}{2} & -\tfrac{1}{2} & 1 &  &  &  \\
 &  &  & 3 &  &  \\
 &  &  &  & 3 &  \\
 &  &  &  &  & 3
\end{bmatrix}
$$

where

$$
E_u = \frac{3E}{2(1+\nu)}
$$

is the **undrained Young’s modulus**.

---

This is the **elastic law used for the Tresca material**.

