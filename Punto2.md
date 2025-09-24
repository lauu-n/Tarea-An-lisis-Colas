# Encontrar N<sub>s</sub> , T<sub>s</sub> , N<sub>w</sub> , T<sub>w</sub>

- N<sub>s</sub> : Número de usuarios en el sistema
- T<sub>s</sub> : Tiempo en el sistema
- N<sub>w</sub> : Número de usuarios en cola
- T<sub>w</sub> : Tiempo en la cola

$$
\text {Probabilidad n clientes en sistema}: {\text{x}} = \frac{\lambda}{\mu} · P<sub>n</sub>
$$

## Probabilidades en estado estacionario P_n

$$ \sum_{n=0}^k P_n $$

Entonces la distribución normalizada es:
\[
P_n = \frac{x^n}{\sum_{m=0}^k x^m} = \frac{(1 - x) x^n}{1 - x^{k+1}}
\]


