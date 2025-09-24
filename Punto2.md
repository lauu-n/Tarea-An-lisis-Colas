# Encontrar N<sub>s</sub> , T<sub>s</sub> , N<sub>w</sub> , T<sub>w</sub>
# Modelo M/M/1/K/∞

## Probabilidades de estado

Por tanto, para \(x \neq 1\):

$$
P_0 = {\frac{1 - x}{1 - x^{k+1}}}, \qquad 
P_n = {\frac{(1-x)x^n}{1 - x^{k+1}}}, \quad n = 0, ..., k
$$

Caso \(x = 1\):

$$
P_n = {{\frac{1}{k+1}}}, \quad n = 0, ..., k
$$

---

## Probabilidad de bloqueo \(P_B\)

$$
P_B = P_k = {\frac{(1-x)x^k}{1 - x^{k+1}}}, \quad (x \neq 1)
$$

y si \(x = 1\):

$$
P_B = {\frac{1}{k+1}}
$$

---

## Tasa efectiva de llegadas

Llegadas reales al sistema:

$$
\lambda_{ef} = \lambda (1 - P_B) = \lambda (1 - P_k)
$$

---

## Número esperado en el sistema \(N_s\)

Para \(x \neq 1\):

$$
N_s = {\frac{x \big(1 - (k+1)x^k + kx^{k+1}\big)}{(1-x)(1 - x^{k+1})}}
$$

Caso \(x = 1\):

$$
N_s = {\frac{k}{2}}
$$

---

## Número esperado en la cola \(N_w\)

Definición:

$$
N_w = N_s - (1 - P_0)
$$

Caso \(x = 1\):

$$
N_w = \frac{k(k-1)}{2(k+1)}
$$

---

## Tiempo esperado en el sistema \(T_s\)

Aplicando la Ley de Little con la tasa efectiva:

$$
T_s = {\frac{N_s}{\lambda_{ef}}}
$$

Caso \(x = 1\):

$$
T_s = {\frac{k+1}{2\lambda}}
$$

---

## Tiempo esperado en cola \(T_w\)

$$
T_w = T_s - \frac{1}{\mu}
$$

Caso \(x = 1\):

$$
T_w = {\frac{k-1}{2\lambda}}
$$

---

# Resumen de fórmulas (x ≠ 1)

- **Probabilidades:**

![P0](https://latex.codecogs.com/svg.image?\color{white}P_0=\frac{1-x}{1-x^{k+1}})
![Pn](https://latex.codecogs.com/svg.image?\color{white}P_n=\frac{(1-x)x^n}{1-x^{k+1}})

- **Bloqueo:**

![PB](https://latex.codecogs.com/svg.image?\color{white}P_B=\frac{(1-x)x^k}{1-x^{k+1}})

- **Llegadas efectivas:**

![Lambdaef](https://latex.codecogs.com/svg.image?\color{white}\lambda_{ef}=\lambda(1-P_B))

- **Usuarios en el sistema:**

![Ns](https://latex.codecogs.com/svg.image?\color{white}N_s=\frac{x(1-(k+1)x^k+kx^{k+1})}{(1-x)(1-x^{k+1})})

- **Usuarios en cola:**

![Nw](https://latex.codecogs.com/svg.image?\color{white}N_w=N_s-(1-P_0))

- **Tiempo en el sistema:**

![Ts](https://latex.codecogs.com/svg.image?\color{white}T_s=\frac{N_s}{\lambda_{ef}})

- **Tiempo en cola:**

![Tw](https://latex.codecogs.com/svg.image?\color{white}T_w=\frac{N_w}{\lambda_{ef}})







