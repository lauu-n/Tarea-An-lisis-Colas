# Comparaciones resultados matemáticos vs resultados computacionales

## Código en NetLogo
'' bash
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
''


## Caso A: λ < µ


