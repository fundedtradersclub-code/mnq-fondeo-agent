# Cambios

## v5 (2026-11-14)

Correcciones sobre "Apex 25k Agent Pro v4 - MNQ (Fixed)":

- **Riesgo con tope real.** En v4 el stop era `max(ATR × multiplicador, riesgo ÷ 2)`: el riesgo en
  dólares funcionaba como stop *mínimo* y, con ATR alto, una operación de 1 contrato podía perder más
  de lo configurado. Ahora el stop sale del ATR (con un mínimo en puntos) y se calculan los contratos
  para no pasar del riesgo. Si ni 1 contrato cabe, no hay señal.
- **Contratos calculados.** v4 decía "puntos y contratos MNQ" pero no calculaba contratos. Usa el
  valor del punto del contrato del gráfico (MNQ 2 USD, NQ 20 USD).
- **Una operación a la vez.** v4 contaba como operación cada vela que cumplía la condición, así que
  tres velas seguidas agotaban el máximo diario. Ahora sigue la operación hasta el stop, el objetivo o
  el fin del horario.
- **Noticias en hora de Nueva York.** Las fechas de v4 no tenían zona horaria y Pine no las
  interpretaba como hora de Nueva York.
- **Rango nocturno real.** "ON High/Low" en v4 era el máximo y mínimo del día anterior completo.
  Ahora es 18:00-09:30 (configurable); el día anterior se muestra aparte.
- **Sin repintado.** Señales, etiquetas y gestión se calculan con la vela cerrada.

Nuevo:

- Breakeven automático al llegar a un nivel de R (simulado y con alerta para moverlo en tu plataforma).
- Monitoreo del trailing drawdown para cuentas 25K / 50K: límite, margen restante y bloqueo de
  entradas que se coman el colchón.
- Pérdida diaria máxima (regla personal), etiqueta cuando una señal no entra por riesgo o margen,
  alertas de salida, breakeven y poco margen.
