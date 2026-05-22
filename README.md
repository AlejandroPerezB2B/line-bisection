# line-bisection

# Guía de implementación y ejecución del experimento de Line Bisection

## Descripción general

El experimento consiste en una tarea computarizada de *line bisection* en la que los participantes deben estimar la posición de una marca vertical situada sobre una línea horizontal. La tarea puede realizarse en dos condiciones experimentales:

1. **Condición individual**: el participante realiza la tarea solo en una cabina aislada.
2. **Condición compartida**: dos participantes realizan simultáneamente exactamente la misma tarea en laptops conectadas entre sí.

En ambas condiciones:
- los estímulos son idénticos,
- el procedimiento es el mismo,
- y las respuestas se introducen mediante teclado.

La manipulación experimental consiste únicamente en si la tarea se realiza:
- en aislamiento perceptivo,
- o en presencia simultánea de otro participante realizando la misma tarea.

---

# 1. Material necesario

## Hardware

- Dos laptops con Windows 11
- MATLAB instalado en ambos ordenadores
- Cable Ethernet
- Teclados funcionales

## Software

- Carpeta del experimento copiada en ambos ordenadores
- MATLAB con soporte para:
  - figuras gráficas,
  - `tcpserver`,
  - `tcpclient`

No se requiere Psychtoolbox para esta versión.

---

# 2. Archivos necesarios

La carpeta del experimento debe contener al menos:

```text
create_line_bisection_files.m
make_trial_orders.m
run_line_bisection_individual.m
run_line_bisection_shared_host.m
run_line_bisection_shared_client.m
lb_draw_trial.m
lb_get_response.m
lb_save_row.m
