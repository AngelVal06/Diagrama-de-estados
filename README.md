# Diagrama-de-estados

## Código:

@startuml
state "Stand-by" as StandBy
state "Validar Tarjeta" as ValidarTarjeta
state "Solicitar PIN" as SolicitarPIN
state "Validar PIN" as ValidarPIN
state "Tarjeta Retenida" as TarjetaRetenida
state "Opciones de Transacción" as OpcionesTransaccion
state "Realizar Transacción" as RealizarTransaccion
state "Finalizar Sesión" as FinalizarSesion

[*] --> StandBy

StandBy --> ValidarTarjeta : Tarjeta introducida
ValidarTarjeta --> StandBy : Tarjeta no válida
ValidarTarjeta --> SolicitarPIN : Tarjeta válida

SolicitarPIN --> ValidarPIN : PIN introducido
ValidarPIN --> SolicitarPIN : PIN incorrecto (intentos < 3)
ValidarPIN --> TarjetaRetenida : PIN incorrecto (3 intentos)
ValidarPIN --> OpcionesTransaccion : PIN correcto

SolicitarPIN --> FinalizarSesion : Cancelar
ValidarPIN --> FinalizarSesion : Cancelar

OpcionesTransaccion --> RealizarTransaccion : Transacción seleccionada
RealizarTransaccion --> OpcionesTransaccion : Transacción finalizada
OpcionesTransaccion --> FinalizarSesion : Cancelar

FinalizarSesion --> StandBy : Sesión finalizada

TarjetaRetenida --> StandBy : Tarjeta retenida

@enduml

## Descripción: 

Claro, te lo explico como si fuera un colega que no sabe mucho del tema, pero quiere entender cómo funciona un cajero automático paso a paso. Vamos allá:

---

### **Diagrama de Estados del Cajero Automático (Explicación sencilla)**

Imagina que el cajero es como un robot que tiene diferentes "modos" o "estados" en los que puede estar. Dependiendo de lo que hagas tú (el usuario), el cajero cambia de un modo a otro. Vamos a ver cada uno de esos modos y qué pasa en cada caso:

---

#### **1. Stand-by (Modo de Espera)**
- Espera a que metas la tarjeta.


#### **2. Validar Tarjeta (Verificar la Tarjeta)**
- Verifica si la tarjeta es buena.

#### **3. Solicitar PIN (Pedir el Número Secreto)**
- Te pide tu PIN para asegurarse de que eres tú.


#### **4. Validar PIN (Verificar el Número Secreto)**
- Si todo está bien, te deja hacer lo que quieras (sacar dinero, etc.).


#### **5. Tarjeta Retenida (El Cajero se Queda con la Tarjeta)**
- Si te equivocas mucho, se queda con la tarjeta.


#### **6. Opciones de Transacción (Elegir qué Hacer)**
- Aquí el cajero te muestra un menú con las cosas que puedes hacer, como:
  - Sacar dinero.
  - Ver cuánto dinero tienes.
  - Pagar facturas, etc.

#### **7. Realizar Transacción (Hacer lo que Elegiste)**
- En este modo, el cajero está haciendo lo que le pediste.
- Cuando termina, te pregunta si quieres hacer algo más o si prefieres terminar.


#### **8. Finalizar Sesión (Terminar)**
- El cajero te devuelve la tarjeta (si no la retuvo antes) y vuelve al modo de espera (Stand-by).

