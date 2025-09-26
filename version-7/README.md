# Henry Estrategia Trading v7 - Sesión Nueva York 🗽

## Descripción General

La **Henry Estrategia Trading v7** es una evolución especializada del sistema v4, diseñada específicamente para operar durante la apertura de la sesión de Nueva York con reglas estrictas de gestión de riesgo y frecuencia de trading.

## 🎯 Filosofía de la Versión 7

### Enfoque Disciplinado
Esta versión implementa un enfoque de **trading disciplinado** que aprovecha la **volatilidad de apertura de Nueva York** mediante:
- **Ventana de trading limitada**: Solo 30 minutos de operación activa
- **Máximo 2 trades por día**: Control estricto de frecuencia
- **Lógica de recuperación**: Segundo trade solo si el primero fue negativo
- **Cierre forzoso**: Sin posiciones overnight

### Horarios Específicos (Hora de Madrid)
- **16:30 - 17:00**: Ventana de trading activa
- **16:00 - 16:30**: Preparación (primera media hora después de apertura NY)
- **17:00**: Cierre forzoso de todas las posiciones

## 🔧 Nuevos Parámetros de la v7

### Gestión de Sesión
```pinescript
max_trades_per_day = 2          // Máximo trades por día
ny_open_hour = 16               // Inicio trading (Madrid)
ny_open_minute = 30             // Minuto de inicio
ny_close_hour = 17              // Cierre forzoso (Madrid)
ny_close_minute = 0             // Minuto de cierre
```

### Parámetros Heredados de v4
- Detección de velas gigantes (multiplicador 1.5x)
- Expansión SMA 20/200 (80% del pico anterior)
- Planitud SMA20 (0.3% threshold)
- Trailing stop automático
- Ratio riesgo/beneficio 2:1

## 📊 Lógica de Trading Avanzada

### Reglas de Entrada
1. **Condiciones Técnicas**: ✅ Vela gigante + Expansión + Dirección correcta
2. **Condiciones Temporales**: ✅ Sesión NY activa (16:30-17:00 Madrid)
3. **Condiciones de Frecuencia**: ✅ Trades disponibles según lógica diaria

### Lógica de Gestión Diaria
```
DÍA NUEVO → Resetear contador a 0

PRIMER TRADE:
├── Si POSITIVO → Fin del día (máximo profit alcanzado)
└── Si NEGATIVO → Permitir segundo trade (oportunidad de recuperación)

SEGUNDO TRADE:
└── Sin más oportunidades (fin del día independiente del resultado)
```

### Ventajas del Sistema
- **Control de drawdown**: Máximo 2 pérdidas por día
- **Maximización de ganancias**: Para cuando hay profit
- **Gestión emocional**: Reglas claras evitan over-trading
- **Foco temporal**: Aprovecha momento de mayor volatilidad

## 🕐 Gestión Temporal Automática

### Conversión de Horarios
```pinescript
Madrid UTC+1 → UTC automático
16:30 Madrid = 15:30 UTC
17:00 Madrid = 16:00 UTC
```

### Estados de Sesión
- **INACTIVA**: Fuera del horario 16:30-17:00
- **ACTIVA**: Dentro del horario, trades permitidos
- **CIERRE FORZOSO**: 17:00 en punto, todas las posiciones se cierran

## 🎮 Panel de Control Avanzado

### Información de Sesión
- **Estado NY**: ACTIVA/INACTIVA con código de colores
- **Contador de trades**: 0/2, 1/2, 2/2 (máximo alcanzado)
- **Resultado 1er trade**: SÍ/NO/N-A
- **Horarios**: Inicio y cierre configurables visibles

### Estados de Bloqueo
- **"MAX TRADES"**: Ya se hicieron 2 trades o 1er trade fue positivo
- **"FUERA DE SESIÓN"**: Signal detectada pero fuera de horario
- **"ESPERANDO"**: Condiciones técnicas no cumplidas

### Información en Tiempo Real
- **P&L actual**: De la posición abierta
- **Precios clave**: Entrada, stop loss, take profit
- **Estado técnico**: Expansión, vela gigante, dirección vs SMA200

## 🚨 Sistema de Alertas Inteligentes

### Alertas de Trading
- **🚀 SEÑAL COMPRA NY**: Incluye validación completa
- **🔻 SEÑAL VENTA NY**: Incluye validación completa
- **⚠️ POSICIÓN CERRADA**: Notifica cuando se cierra por SL/TP
- **⏰ CIERRE FORZOSO**: Notifica cierre por fin de sesión

### Validaciones en Alertas
Cada alerta confirma:
- ✅ Condiciones técnicas cumplidas
- ✅ Sesión NY activa
- ✅ Trades disponibles según reglas diarias

## 🎨 Visualización Mejorada

### Indicadores Visuales
- **Fondo azul claro**: Sesión NY activa
- **Fondo verde**: Zona de expansión + SMA plana
- **Fondo amarillo**: Solo expansión (falta SMA plana)
- **Señales grandes**: 🚀 Compra / 🔻 Venta con validación completa

### Líneas de Referencia
- **SMA 20** (azul): Media móvil rápida
- **SMA 200** (roja): Media móvil lenta
- **Stop Loss** (rojo): Nivel de riesgo
- **Take Profit** (verde): Objetivo de ganancia

## 🔄 Proceso de Ejecución Diario

### 16:00 Madrid - Preparación
- Sistema monitorea condiciones técnicas
- Sin ejecución de trades (primera media hora)

### 16:30 Madrid - Activación
```
1. Sistema activa ventana de trading
2. Monitor continuo de señales
3. Validación: Técnica + Temporal + Frecuencia
4. Ejecución inmediata si todas las condiciones ✅
```

### Durante la Sesión
```
TRADE 1 EJECUTADO:
├── Monitor resultado en tiempo real
├── Aplicar trailing stop si configurado
└── Actualizar estado para determinar TRADE 2

TRADE 2 (solo si TRADE 1 negativo):
├── Mismas validaciones técnicas
├── Última oportunidad del día
└── Sin más trades después
```

### 17:00 Madrid - Cierre
```
- Cierre automático de TODAS las posiciones
- Reseteo para el siguiente día
- Sin excepciones ni override manual
```

## 📈 Ventajas vs Versión 4

| Aspecto | v4 | v7 |
|---------|----|----|
| **Frecuencia** | Alta (24/7) | Controlada (2 max/día) |
| **Horario** | Continuo | 30 min específicos |
| **Gestión riesgo** | Por trade | Por día |
| **Disciplina** | Dependiente del trader | Automatizada |
| **Volatilidad** | Variable | Optimizada (apertura NY) |
| **Overnight** | Posible | Nunca |

## 💡 Casos de Uso Ideales

### Para Traders que Buscan:
- **Control emocional**: Reglas claras evitan decisiones impulsivas
- **Gestión de tiempo**: Solo 30 minutos de atención requerida
- **Riesgo limitado**: Máximo 2 pérdidas por día
- **Aprovechamiento de volatilidad**: Momento óptimo del mercado
- **Backtesting preciso**: Condiciones específicas y repetibles

### Instrumentos Recomendados:
- **Forex majors**: EUR/USD, GBP/USD, USD/JPY
- **Índices US**: SPY, QQQ, DJI (alta correlación con apertura NY)
- **Commodities**: Gold, Oil (reaccionan a apertura US)

## ⚙️ Configuración Óptima

### Parámetros Sugeridos
```
Timeframe: 5 minutos (probado)
Lookback candles: 6
Body multiplier: 1.5
Expansion threshold: 80%
Risk/reward ratio: 2.0
Trailing stop: Activado
```

### Ajustes por Instrumento
- **Forex**: Mantener configuración default
- **Índices**: Considerar body_multiplier 1.3 (mayor volatilidad)
- **Crypto**: Expansion_threshold 85% (más selectivo)

## 🛡️ Gestión de Riesgo Integral

### Por Trade
- Stop loss automático en extremos de vela gigante
- Take profit 2:1 respecto al riesgo
- Trailing stop para maximizar ganancias

### Por Día
- Máximo 2 trades (limitación de frecuencia)
- Parada temprana si primer trade positivo
- Cierre forzoso a las 17:00 (sin overnight)

### Por Semana/Mes
- Revisión de parámetros según rendimiento
- Ajuste de horarios si cambia horario de verano
- Análisis de win rate por día de la semana

## 📋 Instalación y Uso

### Pasos de Implementación
1. **Copiar código** en Pine Editor de TradingView
2. **Configurar horario local**: Ajustar si no estás en zona Madrid
3. **Configurar alertas**: Activar notificaciones de señales
4. **Realizar backtesting**: Verificar rendimiento histórico
5. **Paper trading**: Probar en demo antes de live
6. **Go live**: Con capital apropiado para el riesgo

### Monitoreo Diario
- **16:25**: Prepararse para posible trading
- **16:30-17:00**: Monitoring activo de señales
- **17:00+**: Revisión de resultados del día

## 🎯 Expectativas Realistas

### Frecuencia de Señales
- **Días sin trades**: Normal (condiciones no se cumplen)
- **Días con 1 trade**: Lo más común si hay señales
- **Días con 2 trades**: Solo si primer trade es negativo

### Rendimiento Esperado
- **Win rate**: Objetivo 40-50% (similar a v4)
- **Risk/reward**: 2:1 compensa win rate moderado
- **Drawdown**: Mejor controlado que v4 por limitación diaria
- **Consistencia**: Mayor debido a reglas estrictas

## 🔧 Troubleshooting

### Problemas Comunes
- **No aparecen señales**: Verificar horario local vs Madrid
- **Alertas no funcionan**: Confirmar configuración de notificaciones
- **Resultados diferentes**: Usar exactamente 5 minutos de timeframe

### Optimizaciones Avanzadas
- **Filtro de día de semana**: Evitar viernes (menor volatilidad)
- **Filtro de noticias**: Parar en días de NFP o FOMC
- **Análisis seasonal**: Mejor rendimiento en ciertos meses

## 📝 Conclusiones

La **Henry Estrategia Trading v7** representa una evolución hacia el **trading disciplinado y controlado**. Mediante la implementación de restricciones temporales y de frecuencia, busca:

- **Maximizar el aprovechamiento** de la volatilidad de apertura NY
- **Minimizar el riesgo** a través de reglas estrictas
- **Mejorar la disciplina** del trader mediante automatización
- **Simplificar la operativa** a 30 minutos diarios específicos

Esta versión es ideal para traders que buscan un enfoque **sistemático, controlado y menos demandante en tiempo**, manteniendo la efectividad técnica de la estrategia original.

---

*Versión 7 desarrollada por Henry Trading Systems*  
*Especializada para Sesión Nueva York - Septiembre 2025*
