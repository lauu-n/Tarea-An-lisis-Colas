# Análisis de Congestión usando Sistema de Pérdida M/M/1/k

## Concepto Fundamental: Sistema de Pérdida
Un sistema de pérdida M/M/1/k es un modelo donde los clientes que encuentran el sistema lleno (k clientes) son rechazados inmediatamente, en lugar de esperar en una cola infinita.

## Análisis de Congestión por Casos

### Caso A: λ = 0.5, μ = 1.0, k = 5 (Subutilizado)
```
Pb = 1.59%, λef = 0.4921, Ns = 3, Nw = 2
```
- Análisis de congestión:
        - Baja congestión: Solo 1.59% de clientes perdidos
        - Utilización moderada: Ns = 3 de k = 5 (60% de capacidad)
        - Tiempos razonables: Tw = 8.7 ticks (44% del tiempo en cola)
        - Eficiencia alta: 98.4% de las llegadas son atendidas
    - El sistema opera cómodamente con margen de capacidad. La pérdida de clientes es mínima, indicando buen dimensionamiento.

### Caso B: λ = 1.0, μ = 1.0, k = 5 (Balanceado)
```
Pb = 16.67%, λef = 0.8333, Ns = 5, Nw = 4
```
- Análisis de congestión:
        - Congestión crítica: Sistema siempre lleno (Ns = k)
        - Pérdida significativa: 16.67% de clientes rechazados
        - Cuello de botella: Cola casi al máximo (Nw = 4)
        - Tiempos excesivos: Tw = 29.1 ticks (73% del tiempo en cola)
    - El sistema está sobredimensionado para la demanda actual. Se necesitaría aumentar k o μ para reducir las pérdidas.

### Caso C: λ = 1.5, μ = 1.0, k = 5 (Saturado)
```
Pb = 36.54%, λef = 0.9519, Ns = 5, Nw = 4
```
- Análisis de congestión:
        - Congestión extrema: 36.54% de clientes perdidos
        - Sistema sobrecargado: λ > μ genera colapso inevitable
        - Alta utilización: 95.19% del servidor, pero con grandes pérdidas
        - Eficiencia pobre: Solo 63.46% de eficiencia global
    - El sistema está claramente insuficiente para la demanda. Se requieren cambios estructurales (aumentar μ o k significativamente).


## Métricas Clave para Análisis de Congestión

1. Grado de Congestión por Pb

| Rango de Pb        | Nivel de Congestión   | Acción Recomendada             |
|--------------------|-----------------------|--------------------------------|
| Pb < 5%            | Congestión baja       | Sistema bien dimensionado      |
| 5% ≤ Pb < 20%      | Congestión moderada   | Monitorear, posible ajuste     |
| 20% ≤ Pb < 40%     | Congestión alta       | Considerar expansión           |
| Pb ≥ 40%           | Congestión crítica    | Rediseño necesario             |

2. Indicadores de Congestión en Tiempo Real
    - Congestión Leve (Ns < k/2):
        - Colas cortas o inexistentes
        - Tiempos de espera mínimos
        - Alta λef/λ (>95%)
    - Congestión Moderada (k/2 ≤ Ns < k):
        - Colas presentes pero manejables
        - Tiempos de espera aceptables
        - λef/λ entre 80-95%
    - Congestión Severa (Ns = k):
        - Sistema permanentemente lleno
        - Altos tiempos de espera
        - λef/λ < 80%
        - Necesidad de intervención


## Estrategias para Manejo de Congestión

### Para Reducir Pb (Probabilidad de Pérdida)

1. Aumentar Capacidad (k):
```
k actual = 5, Pb = 36.54%
k = 7 → Pb ≈ 20%
k = 10 → Pb ≈ 10%
```

2. Mejorar Tasa de Servicio (μ):
```
μ actual = 1.0, Pb = 36.54%
μ = 1.2 → Pb ≈ 25% 
μ = 1.5 → Pb ≈ 15% 
```

3. Gestionar demandas
    - Establecer citas o horarios
    - Ofrecer servicios en horas no pico
    - Implementar prioridades

## Conclusiones

- La Pb es el mejor indicador de congestión en sistemas de pérdida
- Ns = k indica congestión máxima - el sistema opera al límite
- λef/λ muestra la eficiencia real del sistema considerando pérdidas
- Los tiempos de espera afectan solo a los clientes que logran entrar
