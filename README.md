# MNQ Fondeo Agent

**Indicador de TradingView para operar futuros MNQ (Micro E-mini Nasdaq-100) en cuentas de fondeo
de 25K y 50K sin romper las reglas por un mal cálculo.**

Te dice cuándo hay una entrada, con cuántos contratos para no pasar de tu riesgo, dónde va el stop,
cuándo moverlo a breakeven y cuánto dinero te queda antes de tocar el trailing drawdown. Si una
operación no cabe en tu riesgo o en el margen de tu cuenta, no la marca y te dice por qué.

> ⚠️ **No es asesoría financiera ni garantiza pasar una evaluación.** Operar futuros implica riesgo
> de perder dinero. Este indicador no tiene relación con ninguna firma de
> fondeo: los valores de drawdown que trae son referenciales. **Verifica siempre las reglas vigentes
> de tu cuenta en el panel de tu firma.**

Pine Script v5 · probado: ambas versiones cargan en TradingView sobre MNQ1!.

## Dos versiones

| Archivo | Tipo | Para qué |
|---|---|---|
| [`mnq-fondeo-agent.pine`](mnq-fondeo-agent.pine) | Indicador (v5) | Señales, riesgo y control de la cuenta. |
| [`mnq-fondeo-agent-estrategia.pine`](mnq-fondeo-agent-estrategia.pine) | Estrategia (v6) | Lo mismo, y además **abre y cierra operaciones simuladas solo en TradingView** para copiarlas a mano en tu cuenta. Dibuja zonas de stop loss y take profit, avisa dos veces ("prepárate" y la entrada confirmada) y muestra resultados en el Probador de estrategias. |

La estrategia **no se conecta a ningún bróker ni ejecuta órdenes reales**: muchas firmas de fondeo no
permiten el trading automatizado, y este diseño deja que copies cada operación tú mismo. Un interruptor
en la configuración (**Modo**) la deja en "solo señales".

Para recibir los avisos en el celular: botón ⏰ → Condición: la estrategia → **"Cualquier llamada a
alert()"**. Llegan el "prepárate", la entrada con contratos, SL y TP, el aviso de mover a breakeven y la
salida.

## Qué hace

**Señales**
- Sesgo con VWAP y el rango nocturno real (máximo y mínimo entre las 18:00 y las 09:30 de Nueva York).
- Confirmación con vela de impulso que rompe la anterior y volumen sobre el promedio.
- Aviso de "setup casi confirmado" antes de la entrada.
- Todo se calcula con la vela cerrada: las señales **no repintan**.

**Riesgo por operación**
- Stop por ATR (con un mínimo en puntos).
- **Contratos calculados** para no pasar del riesgo en dólares que elijas. Si ni un contrato cabe, no
  hay señal ("stop muy amplio para tu riesgo").
- Objetivo en R y **stop a breakeven** al llegar al nivel de R que configures.
- Una operación a la vez: la sigue hasta el stop, el breakeven, el objetivo o el fin del horario, y
  recién entonces cuenta la siguiente.

**Cuenta de fondeo**
- Cuenta de 25K o 50K, con su trailing drawdown típico (1.500 / 2.500 USD) o el valor que indiques.
- Con tu saldo actual y tu saldo máximo calcula el **límite que no puedes tocar** y el **margen que te
  queda**. Bloquea entradas cuyo riesgo se coma el colchón mínimo que fijes.
- Máximo de operaciones por día y pérdida diaria máxima (regla personal, simulada).
- Bloqueo por noticias en hora de Nueva York.

**En pantalla**
- VWAP, rango nocturno, máximo y mínimo del día anterior, entrada, stop y objetivo.
- Tabla de control: límite de la cuenta, margen, operaciones del día, tamaño, P&L simulado, horario,
  noticias y si puedes operar.
- Alertas de entrada, salida, breakeven, setups, noticias, máximo diario y poco margen.

## Instalación

1. En TradingView abre un gráfico de **MNQ1!** (de 1 a 5 minutos).
2. Abajo, pestaña **Pine Editor** → menú del nombre del script → **Crear nuevo** → **Indicador** (o **Estrategia** para la v6).
3. **Borra todo el texto de ejemplo** (Ctrl + A y Supr) y pega el contenido del archivo que elegiste. Si queda el ejemplo, TradingView muestra el error
   *"Scripts must contain one declaration statement… Your script has 2 (CE10243)"*.
4. Pulsa **Guardar** y luego **Añadir al gráfico**.
5. En la configuración del indicador (⚙️), completa **Cuenta de fondeo**: tamaño, saldo actual y saldo
   máximo alcanzado, tal como aparecen en el panel de tu firma.
6. Actualiza las fechas de **Noticias** (IPC, empleo, Fed) de la semana.

Para alertas: botón ⏰ → Condición: *MNQ Fondeo Agent v5* → "Cualquier llamada a alert()" para recibir
entrada, salida y breakeven con precios.

## Límites importantes

- **Es un indicador, no ejecuta órdenes.** No se conecta a tu cuenta ni mueve tu stop: te avisa para
  que lo hagas tú o para que configures lo mismo en tu plataforma (por ejemplo, una plantilla ATM de
  NinjaTrader con el mismo stop, objetivo y breakeven).
- **No ve tu saldo real.** El saldo actual y el máximo los escribes tú; actualízalos antes de cada
  sesión. El P&L del día es una simulación de las señales del indicador, no tus operaciones reales.
- Simula entradas al cierre de la vela de señal; en real puede haber deslizamiento.
- Si en una misma vela se tocan stop y objetivo, asume el stop.
- Las reglas de las firmas cambian (drawdown, contratos máximos, horarios, consistencia). Revisa las
  tuyas.

## Cambios respecto a la v4

Ver [CHANGELOG.md](CHANGELOG.md).

## Licencia

MIT. Hecho por [El Migrante Digital](https://www.instagram.com/elmigrante.digital/).
