# Texto para publicar en TradingView

## Título

MNQ Fondeo Agent v5: contratos por riesgo, breakeven y trailing drawdown

## Descripción

MNQ Fondeo Agent es un asistente para operar futuros MNQ (Micro E-mini Nasdaq-100) en cuentas de fondeo de 25K y 50K. Su objetivo es que una buena entrada no termine en una cuenta perdida por un mal cálculo de tamaño o por acercarse demasiado al trailing drawdown.

QUÉ HACE

• Sesgo: el precio debe estar del mismo lado del VWAP y fuera del rango nocturno (máximo o mínimo entre las 18:00 y las 09:30 de Nueva York).
• Confirmación: vela de impulso que rompe el máximo o mínimo de la vela anterior, con volumen sobre su promedio. Antes de la entrada marca un "setup casi confirmado".
• Stop por ATR (con un mínimo en puntos) y objetivo en múltiplos de R.
• Calcula cuántos contratos usar para no pasar del riesgo en dólares que elijas, con el valor del punto del contrato del gráfico (MNQ 2 USD, NQ 20 USD). Si ni un contrato cabe, no da la señal y lo indica en el gráfico.
• Una operación a la vez: la sigue hasta el stop, el breakeven, el objetivo o el fin del horario. Mueve el stop a breakeven al llegar al nivel de R que configures.
• Cuenta de fondeo: con tu saldo actual y tu saldo máximo calcula el nivel que no puedes tocar y el margen que te queda. Bloquea entradas cuyo riesgo se coma el colchón mínimo que definas.
• Límites diarios: máximo de operaciones y pérdida diaria máxima (sobre las operaciones simuladas del indicador).
• Bloqueo por noticias: hasta tres horarios en hora de Nueva York, con minutos de bloqueo antes y después.
• Todo se calcula con la vela cerrada: las señales no cambian después de aparecer.

EN EL GRÁFICO

VWAP, rango nocturno, máximo y mínimo del día anterior, entrada, stop y objetivo de la operación activa, fondo de color para el horario de entradas, noticias y límite diario, y una tabla con: límite de la cuenta, margen restante, operaciones del día, contratos y riesgo, P&L simulado, horario, noticias y si puedes operar.

CÓMO USARLO

1. Gráfico de MNQ1! en 1 a 5 minutos.
2. En la configuración, sección "Cuenta de fondeo": tamaño de cuenta, saldo actual y saldo máximo alcanzado tal como aparecen en el panel de tu firma. Actualízalos antes de cada sesión.
3. Ajusta el riesgo por operación, el máximo de contratos y el horario de entradas (por defecto 09:30 a 11:45 de Nueva York).
4. Carga las noticias de la semana (IPC, empleo, Fed) en la sección "Noticias".
5. Para alertas con precios de entrada, salida y breakeven, crea una alerta con la condición "Cualquier llamada a alert()". También hay condiciones separadas para setups, entradas, noticias, máximo diario y poco margen.

LÍMITES

• Es un indicador: no ejecuta órdenes ni ve tu cuenta real. El saldo lo escribes tú, y el P&L del día es una simulación de sus propias señales.
• Las entradas se simulan al cierre de la vela de señal; en real puede haber deslizamiento. Si una vela toca el stop y el objetivo, se asume el stop.
• Los valores de trailing drawdown por defecto (1.500 para 25K, 2.500 para 50K) son referenciales y editables. Las reglas cambian según la firma y la cuenta: verifícalas siempre en tu panel.
• No tiene relación con ninguna firma de fondeo.

Este indicador es una herramienta de apoyo y no constituye asesoría financiera. Operar futuros implica un riesgo alto de pérdida; los resultados pasados o simulados no garantizan resultados futuros.

---

## Description (English)

MNQ Fondeo Agent is an assistant for trading MNQ (Micro E-mini Nasdaq-100) futures on 25K and 50K funded/evaluation accounts. Its goal is to keep a good entry from blowing an account because of bad position sizing or getting too close to the trailing drawdown.

WHAT IT DOES

• Bias: price must be on the same side of VWAP and outside the overnight range (high or low between 18:00 and 09:30 New York time).
• Confirmation: a momentum candle breaking the previous candle's high or low with above-average volume. A "setup almost confirmed" label appears beforehand.
• ATR-based stop (with a minimum in points) and a target in R multiples.
• Calculates how many contracts to trade so you never exceed your dollar risk, using the chart contract's point value (MNQ 2 USD, NQ 20 USD). If not even one contract fits, there is no signal and the chart says why.
• One trade at a time, tracked until stop, breakeven, target or end of session. Moves the stop to breakeven at the R level you choose.
• Funded account: from your current balance and highest balance it computes the level you cannot touch and the room you have left, and blocks entries whose risk would eat your minimum buffer.
• Daily limits: max trades and max daily loss (based on the indicator's simulated trades).
• News filter: up to three times in New York time, with a blackout window before and after.
• Everything is calculated on closed bars: signals do not change after they appear.

ON THE CHART

VWAP, overnight range, previous day high/low, entry, stop and target of the active trade, background colors for the entry window, news and daily limit, and a table with: account limit, remaining room, trades today, contracts and risk, simulated P&L, session, news and whether you can trade.

HOW TO USE

1. MNQ1! chart, 1 to 5 minutes.
2. In the settings, "Cuenta de fondeo" section: account size, current balance and highest balance as shown in your firm's dashboard. Update them before each session.
3. Set risk per trade, max contracts and entry window (default 09:30-11:45 New York).
4. Enter this week's news times (CPI, jobs, Fed) in the "Noticias" section.
5. For alerts with entry, exit and breakeven prices, create an alert with "Any alert() function call". Separate conditions exist for setups, entries, news, daily max and low margin.

LIMITATIONS

• It is an indicator: it does not place orders or read your real account. You enter the balance yourself, and the daily P&L is a simulation of its own signals.
• Entries are simulated at the close of the signal bar; real fills may differ. If a bar hits both stop and target, the stop is assumed.
• Default trailing drawdown values (1,500 for 25K, 2,500 for 50K) are reference values and editable. Rules differ by firm and account: always check yours.
• Not affiliated with any prop firm.

This indicator is a support tool and is not financial advice. Trading futures involves a high risk of loss; past or simulated results do not guarantee future results.
