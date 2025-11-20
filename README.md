# IoT Heartbeat Monitor (Scenario 2 – MQTT)

Este repositório contém o protótipo **IoT Heartbeat Monitor – Scenario 2 (MQTT)**, desenvolvido na disciplina **Objetos Inteligentes Conectados**.  
O objetivo é monitorar um sinal de batimento cardíaco (ECG simulado), gerar **alertas locais** (LED + buzzer) e **alertas remotos** via **MQTT**, permitindo também **controle manual** dos atuadores por mensagens MQTT.

## 1. Visão geral do sistema

- Microcontrolador: **ESP32**
- Entradas:
  - Sinal de ECG simulado (via potenciômetro no Wokwi) no pino **ECG_PIN = 34**
- Saídas:
  - **LED** no pino **LED_PIN = 25**
  - **Buzzer** no pino **BUZZER_PIN = 26**
- Lógica básica:
  - Lê o valor analógico do “ECG” e compara com limites:
    - `LOW_THRESHOLD = 500`
    - `HIGH_THRESHOLD = 2000`
  - Se o sinal ficar fora da faixa:
    - Acende o LED (modo automático, se não houver override manual).
    - Se a anomalia persistir (≈ 2 segundos), liga o buzzer.
    - Publica uma mensagem de **alerta** via MQTT.
  - Em condições normais:
    - LED e buzzer permanecem desligados (a menos que estejam em modo manual).
  - Por MQTT é possível:
    - Ligar/desligar LED e buzzer manualmente.
    - Enviar um comando `RESET` para voltar ao modo automático.

O projeto dialoga com o **ODS 3 – Saúde e Bem-estar**, ao simular um sistema de monitoramento remoto que poderia ser adaptado a contextos reais de acompanhamento de pacientes.

---

## 2. Arquitetura em alto nível

- **Camada de Dispositivo (Edge)**  
  ESP32 + sensor/ECG simulado + LED + buzzer.
- **Camada de Comunicação**  
  Wi-Fi (TCP/IP) do ESP32 conectado a um **broker MQTT público**.
- **Camada de Aplicação**  
  Clientes MQTT (por exemplo, MQTTX) que:
  - Recebem os valores de ECG.
  - Recebem alertas.
  - Enviam comandos de controle.

Mais detalhes estão em:

- [`docs/arquitetura.md`](docs/arquitetura.md)
- [`docs/hardware.md`](docs/hardware.md)
- [`docs/comunicacao_mqtt.md`](docs/comunicacao_mqtt.md)

---

## 3. Tópicos MQTT usados

O sketch utiliza o broker público:

```cpp
const char* mqtt_server = "test.mosquitto.org";
