# Proyecto de simulación en NetLogo: Cola $\ M / M / 1 / K / ∞ $

## Descripción  
Este proyecto consiste en el desarrollo de un modelo en **NetLogo** que permite simular el comportamiemto de la cola:
$\ M / M / 1 / K / ∞ $

El modelo utiliza **sliders, botones y monintores** para que el usuario pueda controlar parámetros de la simulación y observar en tiempo real el comportamiento de las variables más importantes.  

##  Funcionalidades principales  
- Controlar parámetros del sistema mediante **sliders**.  
- Visualización gráfica en la interfaz de NetLogo.  
- Registro de variables mediante **monitores y gráficos**.  
- Simulación paso a paso o automática.  

## Estructura del proyecto  
- `Punto1.md` → Analiza el comportamiento de la cola.
- `Punto2.md` → Encuentra número de usuarios y tiempos, tanto en el sistema como en la cola.
- `Punto3.md` (Carpeta) → Compilación del análisis y representación de la cola.
  - `Punto3.nlogox` → Archivo principal con el código del modelo.
  - `Punto3.md` → Documentación de la representación gráfica de la cola.
  - `AnalisisPunto3.md` → Análisis de la representación gráfica de la cola.
- `Punto4.md` → Análisis concepto de congestión usando sistema de pérdida.
- `README.md` → documentación principal del proyecto.  

## Requisitos para ejecutarlo
- NetLogo 6.3.0 o superior
- [Descargar NetLogo](https://ccl.northwestern.edu/netlogo/)

## Pasos para ejecutarlo
1. **Abrir el Modelo**: Descargar el archivo `.nlogox` y abrir con NetLogo.
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

## Parámetros principales  
- x < 1: λ < μ → Sistema estable
- x = 1: λ = μ → Sistema balanceado
- x > 1: λ > μ → Sistema inestable

- **slider-1** → lambda (λ): Tasa de llegada de clientes al sistema, Frecuencia con la que llegan nuevos clientes, Intensidad de la demanda del servicio
- **slider-2** → mu (μ): Tasa de servicio del sistema, Velocidad con la que se atiende a los clientes.
- **slider-3** → k (Capacidad): Número máximo de clientes permitidos en el sistema, Capacidad total (en servicio + en cola), Límite físico del sistema.


---


### Laura Niño
