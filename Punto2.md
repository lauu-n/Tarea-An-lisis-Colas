# Encontrar N<sub>s</sub> , T<sub>s</sub> , N<sub>w</sub> , T<sub>w</sub>

- N<sub>s</sub> : Número de usuarios en el sistema
- T<sub>s</sub> : Tiempo en el sistema
- N<sub>w</sub> : Número de usuarios en cola
- T<sub>w</sub> : Tiempo en la cola

$$
\text {Probabilidad n clientes en sistema}: {\text{x}} = \frac{\lambda}{\mu} · P<sub>n</sub>
$$

## Probabilidades en estado estacionario P_n

Ecuaciones de balance:
P<sub>n</sub> = $\ x^n$ P<sub>0</sub> , *n* = 0, 1, ..., *k*

Normalizar como: 

$$\sum_{n=0}^k P_n$$

$$\left(P_0 \sum_{n=0}^k x^n \right) → \left( P_0 {\frac{1 - x^(k+1)}{1-x}} = 1 (x ≠ 1) \right)$$

Por tanto para x ≠ 1:

$$\left(P_0 = {\frac{1 - x}{1-x^(k+1}}\right) , \left( P_n {\frac{(1-x)x^n}{1-x^(k+1)}} , n = 0, ..., k \right)$$

Caso x = 1

$$\left(P<sub>n</sub> = {\frac{1}{k+1}}\right) , \left(n = 0, ..., k \right)$$

## Probabilidad de bloqueo P_B

$$
\text {PB = Pk}= {\frac{(1-x)x^k}{1-x^(k+1)}(x ≠ 1)}
$$

y si x = 1: 

$$
\text {PB}= {\frac{1}{k+1}}
$$

## Tasa efectiva de llegadas

Llegadas reales al sistema:


$$
{\lambda}<sub>ef</sub> = {\lambda}(1 - P_B) = {\lambda}(1 - P_k)











