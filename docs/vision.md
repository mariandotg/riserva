# Visión — riserva

## Problema

Los agentes de IA no saben cuánta cuota les queda. No lo saben de su propia
suscripción ni de las suscripciones de otros proveedores. Para obtener el
porcentaje real, un agente hace muchas tool calls o navega hasta encontrarlo.

Por eso dispatch reparte tareas sin saber si la cuota del proveedor alcanza.

## Qué es

riserva es una primitiva: una CLI y un MCP que devuelven cuánto uso queda en
cada suscripción de IA. Quien la consume decide qué hacer con el dato:

- un agente decide si puede seguir;
- dispatch decide si la cuota de un proveedor alcanza para una tarea;
- un dev consulta el uso de Claude con un comando;
- un dev arma su propia UI de uso encima y se enfoca solo en la UI.

Proveedores de la v1: Claude, Codex y Cursor. Es también un proyecto de
estudio: se construye desde cero.

## Audiencia

1. **Agentes**, primero: el orquestador (`dispatch-board`) y los agentes
   despachados.
2. **Devs que pagan varias suscripciones de IA** y reparten trabajo entre CLIs.

## Alternativas

| Alternativa | Qué hace | Diferencia |
|---|---|---|
| CodexBar | App de barra de menú en macOS con el porcentaje de cada suscripción; trae una CLI con salida JSON | riserva es la capa para agentes: un MCP con el uso propio de cada agente. No depende de CodexBar. |
| ccusage | Cuenta tokens y costo desde los logs locales | ccusage mide tokens gastados; riserva mide la cuota que queda del plan. |

## Qué NO es

1. **No es un router.** No decide a qué proveedor va una tarea. Eso lo decide dispatch.
2. **No es una app de escritorio ni de barra de menú.** Vive en la terminal y no ocupa memoria en reposo.
3. **No es un tracker de costos ni de facturación.** No suma dólares ni tokens históricos.
4. **No es un proxy.** No intercepta ni cuenta llamadas a la API en tránsito.
5. **No es observabilidad de LLMs.** No guarda trazas, prompts ni latencias.
6. **No gestiona cuentas ni credenciales.** Lee las que ya guarda cada CLI. No hace login ni rota keys.

## Horizontes

- **3 meses:** `dispatch-board` sugiere el target de cada ticket con datos de riserva.
- **12 meses:** otros devs usan riserva.
- **3 años:** sin definir.
