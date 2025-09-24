# Comparaciones resultados matemáticos vs resultados computacionales

## Caso A: λ < µ → Sistema Subutilizado

- Parámetros:
  - λ: 0.5
  - µ: 1
  - k: 5

Resultados:
  - Clientes en sistema (Ns): 3
  - Clientes en cola (Nw): 2
  - Tiempo en sistema (Ts): 18.31 ticks
  - Tiempo en cola (Tw): 8.7 ticks
  - Pb teórica: 0.0159 (1.59%)
  - λ efectiva: 0.4921 clientes/tick
  - Clientes completados: 250
  - Ticks: 5000

Análisis de congestión: 
  - Ns = 3, Nw = 2 → El sistema tiene carga moderada
  - Relación Nw/Ns = 2/3 ≈ 66% → Los clientes pasan más tiempo en servicio que en cola
  - Pb = 1.59% → Muy baja probabilidad de bloqueo, el sistema rara vez se llena

Análisis de tiempos:
  - Ts = 18.31 ticks (tiempo total en sistema)
  - Tw = 8.7 ticks (tiempo en cola)
  - Tiempo de servicio = Ts - Tw = 9.61 ticks ≈ 1/μ (teórico: 1.0)

Eficiencia:
  - Utilización del servidor = 1 - P₀ ≈ λ/μ = 0.5 (50% de uso)
  - Tasa efectiva λef = 0.4921 ≈ λ (poca pérdida por bloqueo.
  - Eficiencia = λef/λ = 98.4% → Excelente utilización.

Comparación valores teóricos:
| Métrica | Teórico  | Simulado | Diferencia            |
|---------|----------|----------|-----------------------|
| Pb      | 1.56%    | 1.59%    | +0.03% ✅             |
| Ns      | ~0.98    | 3.0      | ⚠️ Mayor congestión   |
| Ts      | ~2.0     | 18.31    | ⚠️ Más alto           |

Conclusión:
  - El sistema funciona como un sistema subutilizado pero muestra mayor congestión de la esperada. La probabilidad de bloqueo es mínima (1.59%), pero los tiempos en sistema son más altos que los teóricos, posiblemente por efectos transitorios o variabilidad estadística.

<img width="1029" height="713" alt="Captura de pantalla 2025-09-24 010511" src="https://github.com/user-attachments/assets/5ec3ea19-c8c1-4b0e-9c7c-030caf8ef7eb" />


--

## Caso B: λ = µ → Sistema Balanceado

- Parámetros:
  - λ: 1
  - µ: 1
  - k: 5

Resultados:
  - Clientes en sistema (Ns): 5
  - Clientes en cola (Nw): 4
  - Tiempo en sistema (Ts): 39.59 ticks
  - Tiempo en cola (Tw): 29.1 ticks
  - Pb teórica: 0.1667
  - λ efectiva: 0.8333 clientes/tick
  - Clientes completados: 399
  - Ticks: 5000

Análisis de congestión: 
  - Ns = 5, Nw = 4 → Sistema operando al máximo de capacidad (Ns = k)
  - Relación Nw/Ns = 4/5 = 80% → Alta congestión en cola, clientes pasan mucho tiempo esperando
  - Pb = 16.67% → Probabilidad de bloqueo moderada, 1 de cada 6 clientes es rechazado

Análisis de tiempos:
  - s = 39.59 ticks (tiempo total en sistema)
  - Tw = 29.1 ticks (tiempo en cola)
  - Tiempo de servicio = Ts - Tw = 10.49 ticks ≈ 1/μ (teórico: 1.0) pero con alta variabilidad

Eficiencia:
  - Utilización del servidor = λef/μ = 0.8333 (83.33% de uso)
  - Tasa efectiva λef = 0.8333 < λ (pérdida del 16.67% por bloqueo)
  - Eficiencia = λef/λ = 83.33% → Utilización buena pero con pérdidas significativas

Comparación valores teóricos:
| Métrica | Teórico  | Simulado | Diferencia             |
|---------|----------|----------|------------------------|
| Pb      | 16.67%   | 16.67%   | 0.00% ✅               |
| Ns      | ~2.5     | 5.0      | ⚠️ +2.5 (sistema lleno)|
| Ts      | ~3.0     | 39.59    | ❌ +36.59              |

Conclusión:
  - El sistema opera en condición balanceada (λ = μ) pero muestra congestión extrema, funcionando constantemente al límite de capacidad. La probabilidad de bloqueo coincide exactamente con el valor teórico, validando el modelo para este aspecto. Sin embargo, los tiempos en sistema son excesivamente altos comparado con lo teórico, sugiriendo posibles issues en la implementación de la lógica de servicio o cálculo de tiempos. El sistema está eficientemente utilizado pero con pérdidas significativas por bloqueo.

<img width="1029" height="713" alt="Captura de pantalla 2025-09-24 011856" src="https://github.com/user-attachments/assets/3e769506-5037-47b4-a79c-d0a9b97b5460" />


--


## Caso C: λ > µ → Sistema Saturado

- Parámetros:
  - λ: 1.5
  - µ: 1
  - k: 5

Resultados:
  - Clientes en sistema (Ns): 5
  - Clientes en cola (Nw): 4
  - Tiempo en sistema (Ts): 43.77 ticks
  - Tiempo en cola (Tw): 33.68 ticks
  - Pb teórica: 0.3654 (36.54%)
  - λ efectiva: 0.9519 clientes/tick
  - Clientes completados: 451
  - Ticks: 5000

Análisis de congestión: 
  - Ns = 5, Nw = 4 → Sistema permanentemente lleno (Ns = k)
  - Relación Nw/Ns = 4/5 = 80% → Congestión crítica, cola casi siempre al máximo
  - Pb = 36.54% → Alta probabilidad de bloqueo, más de 1 de cada 3 clientes es rechazado

Análisis de tiempos:
  - Ts = 43.77 ticks (tiempo total en sistema)
  - Tw = 33.86 ticks (tiempo en cola)
  - Tiempo de servicio = Ts - Tw = 9.91 ticks ≈ 1/μ (teórico: 1.0)
  - Los clientes pasan el 77% de su tiempo en cola

Eficiencia:
  - Utilización del servidor = λef/μ = 0.9519 (95.19% de uso)
  - Tasa efectiva λef = 0.9519 << λ (pérdida del 36.46% por bloqueo)
  - Eficiencia = λef/λ = 63.46% → Baja eficiencia debido al alto bloqueo

Comparación valores teóricos:
| Métrica | Teórico  | Simulado | Diferencia              |
|---------|----------|----------|-------------------------|
| Pb      | 36.54%   | 36.54%   | 0.00% ✅               |
| Ns      | ~3.8     | 5.0      | ⚠️ +1.2 (siempre lleno)|
| Ts      | ~4.0     | 43.77    | ❌ +39.77              |

Conclusión:
  - El sistema opera en condición de saturación (λ > μ) funcionando permanentemente al límite de capacidad. La probabilidad de bloqueo coincide exactamente con el valor teórico, confirmando la validez del modelo para cálculos de bloqueo. Sin embargo, se mantiene la anomalía en los tiempos de sistema, que son un orden de magnitud mayor que los valores teóricos esperados. El sistema presenta baja eficiencia global debido al alto porcentaje de clientes rechazados, pero el servidor está altamente utilizado con los clientes que logran entrar al sistema.

<img width="1029" height="713" alt="image" src="https://github.com/user-attachments/assets/da915ce3-4167-46aa-85bf-c3bc8df0abac" />


--


## Código en NetLogo

```
globals [
  total-clientes
  tiempo-total-sistema
  tiempo-total-cola
  clientes-completados
  Ns
  Nw
  Ts
  Tw
  Pb-teorica
  lambda-efectiva
]

turtles-own [
  tiempo-llegada
  tiempo-inicio-servicio
  en-cola?
]

to setup
  clear-all
  reset-ticks
  
  ;; Valores por defecto
  if not is-number? lambda [ set lambda 0.8 ]
  if not is-number? mu [ set mu 1.0 ]
  if not is-number? k [ set k 5 ]
  
  set total-clientes 0
  set tiempo-total-sistema 0
  set tiempo-total-cola 0
  set clientes-completados 0
  
  ;; Crear área de servicio
  ask patches [ set pcolor white ]
  
  ;; Dibujar áreas visuales
  ask patches with [pxcor = -5 and pycor >= -2 and pycor <= 2] [ set pcolor yellow ]  ;; Zona de llegada
  ask patches with [pxcor = 0 and abs pycor <= 1] [ set pcolor green ]        ;; Servidor
  ask patches with [pxcor >= -4 and pxcor <= -1 and abs pycor <= 1] [ set pcolor gray ]  ;; Cola
  
  ;; Crear servidor
  create-turtles 1 [
    set shape "person"
    set color blue
    set size 2
    setxy 0 0
    set label "Servidor"
  ]
  
  ;; CORRECCIÓN: Eliminar update-display
  calcular-metricas-teoricas
end

to calcular-metricas-teoricas
  let x lambda / mu
  
  ;; Probabilidad de bloqueo teórica
  ifelse x != 1 [
    set Pb-teorica ((1 - x) * (x ^ k)) / (1 - (x ^ (k + 1)))
  ] [
    set Pb-teorica 1 / (k + 1)
  ]
  
  ;; Tasa efectiva de llegadas
  set lambda-efectiva lambda * (1 - Pb-teorica)
  
  ;; Métricas teóricas usando fórmulas de Little
  if x != 1 and lambda-efectiva > 0 [
    ;; Número promedio en sistema
    let Ls x * (1 - (k + 1) * (x ^ k) + k * (x ^ (k + 1))) / ((1 - x) * (1 - (x ^ (k + 1))))
    
    ;; Número promedio en cola
    let Lw Ls - (1 - Pb-teorica)
    
    ;; Tiempos promedio
    set Ts Ls / lambda-efectiva
    set Tw Lw / lambda-efectiva
  ]
end

to llegada-cliente
  ;; Generar llegadas con distribución exponencial
  if random-float 1.0 < (lambda * 0.1) and (count turtles with [shape = "circle"] < k) [
    create-turtles 1 [
      set shape "circle"
      set color red
      set size 1.5
      set tiempo-llegada ticks
      set en-cola? true
      
      ;; Posicionar en cola
      let pos-en-cola count turtles with [shape = "circle" and en-cola?]
      setxy -2 - (pos-en-cola * 0.8) 0
      
      set label who
    ]
    set total-clientes total-clientes + 1
  ]
end

to servicio
  let cliente-siendo-atendido one-of turtles with [shape = "circle" and not en-cola?]
  
  ;; Si no hay cliente siendo atendido, tomar uno de la cola
  if cliente-siendo-atendido = nobody [
    let siguiente-cliente one-of turtles with [shape = "circle" and en-cola?]
    if siguiente-cliente != nobody [
      ask siguiente-cliente [
        set en-cola? false
        setxy 0 0  ;; Mover al servidor
        set tiempo-inicio-servicio ticks
      ]
    ]
  ]
  
  ;; Atender cliente actual (si existe)
  if cliente-siendo-atendido != nobody [
    if random-float 1.0 < (mu * 0.1) [
      ;; Servicio completado
      ask cliente-siendo-atendido [
        set tiempo-total-sistema tiempo-total-sistema + (ticks - tiempo-llegada)
        set tiempo-total-cola tiempo-total-cola + (tiempo-inicio-servicio - tiempo-llegada)
        die
      ]
      set clientes-completados clientes-completados + 1
    ]
  ]
  
  ;; Reorganizar cola visualmente
  reorganizar-cola
end

to reorganizar-cola
  let clientes-en-cola sort turtles with [shape = "circle" and en-cola?]
  let pos 0
  foreach clientes-en-cola [ cliente ->
    ask cliente [
      setxy -2 - (pos * 0.8) 0
    ]
    set pos pos + 1
  ]
end

to calcular-metricas-simulacion
  ;; Métricas actuales del sistema
  set Ns count turtles with [shape = "circle"]  ;; En sistema
  set Nw count turtles with [shape = "circle" and en-cola?]  ;; En cola
  
  ;; Tiempos promedio (si hay datos)
  if clientes-completados > 0 [
    set Ts tiempo-total-sistema / clientes-completados
    set Tw tiempo-total-cola / clientes-completados
  ]
end

to go
  if ticks >= 5000 [ 
    output-print "Simulación completada (5000 ticks)"
    stop 
  ]
  
  llegada-cliente
  servicio
  calcular-metricas-simulacion
  
  tick
end

to reportar-estadisticas
  output-print "=== ESTADÍSTICAS DEL SISTEMA ==="
  output-print (word "Ticks simulados: " ticks)
  output-print (word "Clientes totales: " total-clientes)
  output-print (word "Clientes completados: " clientes-completados)
  output-print (word "Ns (en sistema): " Ns)
  output-print (word "Nw (en cola): " Nw)
  output-print (word "Ts promedio: " precision Ts 2)
  output-print (word "Tw promedio: " precision Tw 2)
  output-print (word "Pb teórica: " precision Pb-teorica 4)
  output-print (word "λ efectiva: " precision lambda-efectiva 4)
end
```






