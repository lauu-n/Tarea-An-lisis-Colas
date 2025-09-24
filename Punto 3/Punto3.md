# Simulación de Sistema de Colas M/M/1/k en NetLogo

## Descripción del Proyecto
Simulación de un sistema de colas con capacidad limitada (modelo M/M/1/k) para analizar el comportamiento de clientes en un sistema de servicio con restricciones de capacidad.

## Objetivos
    - Modelar y simular un sistema de colas con capacidad finita
    - Calcular métricas de desempeño: Ns, Nw, Ts, Tw
    - Validar fórmulas teóricas de probabilidad de bloqueo (Pb)
    - Analizar el comportamiento bajo diferentes condiciones de carga

## Parámetros del Modelo
| Parámetro | Descripción                           | Rango Típico     |
|-----------|---------------------------------------|------------------|
| λ (lambda) | Tasa de llegada de clientes           | 0.1 - 2.0       |
| μ (mu)     | Tasa de servicio                      | 0.5 - 3.0       |
| k          | Capacidad máxima del sistema          | 1 - 10          |

## Métricas Calculadas

### Métricas Principales
- **Ns**: Número de clientes en el sistema
- **Nw**: Número de clientes en cola
- **Ts**: Tiempo promedio en el sistema
- **Tw**: Tiempo promedio en cola
- **Pb**: Probabilidad teórica de bloqueo
- **λef**: Tasa efectiva de llegadas
    
### Fórmulas Teóricas Implementadas:

- Para (x ≠ 1):

$$
\text {PB}= {\frac{(1-x)x^k}{1-x^(k+1)}}
$$

- Para (x = 1):
$$
\text {PB}= {\frac{1}{k+1}}
$$

- Tasa efectiva:

$$
{\lambda}<sub>ef</sub> = {\lambda}(1 - P_B) = {\lambda}(1 - P_k)
$$


## Cómo Ejecutar la Simulación

### Requisitos
- NetLogo 6.3.0 o superior
- [Descargar NetLogo](https://ccl.northwestern.edu/netlogo/)

### Pasos para Ejecutar
1. **Abrir el Modelo**: Descargar el archivo `.nlogo` y abrir con NetLogo.
2. **Configurar Parámetros**: Ajustar los sliders: lambda, mu, k
    - Valores recomendados para inicio:
      - λ = 0.5
      - μ = 1.0
      - k = 5
3. **Inicializar el Sistema**: Hacer clic en el botón *setup*.
4. **Ejecutar la Simulación**:
    - Ejecución continua: Botón *go*
    - Paso a paso: Botón *go once*
    - Parar: Hacer clic nuevamente en *go*
5. **Ver Resultados**: Monitorear métricas en tiempo real y usar el botón *Estadísticas* para reporte detallado.

## Casos de Estudio

### Caso A: Sistema Subutilizado (λ < μ)
- λ = 0.5, μ = 1.0, k = 5
- Pb baja (~1.6%)
- Sistema estable
- Baja congestión

### Caso B: Sistema Balanceado (λ = μ)
- λ = 1.0, μ = 1.0, k = 5
- Pb moderada (~16.7%)
- Sistema en equilibrio
- Congestión media

### Caso C: Sistema Saturado (λ > μ)
- λ = 1.5, μ = 1.0, k = 5
- Pb alta (~36.5%)
- Sistema sobrecargado
- Alta congestión

## Análisis de Resultados

### Interpretación de Métricas
- **Ns > k**: Error en simulación
- **Tw ≈ Ts**: Servidor rápido, cola larga
- **Pb > 30%**: Sistema necesita más capacidad
- **λef ≈ λ**: Buen desempeño del sistema

### Validación del Modelo
Comparar valores simulados con teóricos:
- Pb teórica vs observada
- Ley de Little: Ns = λef × Ts

### Optimizaciones Recomendadas
- Ejecutar mínimo 5,000 ticks para estado estable.
- Descartar primeros 1,000 ticks como transitorios.
- Repetir simulaciones para validación estadística.

## Referencias Teóricas

### Modelo M/M/1/k
- Sistema de colas con un servidor
- Tiempos entre llegadas exponenciales
- Tiempos de servicio exponenciales
- Capacidad máxima: k clientes

