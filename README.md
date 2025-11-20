# IoT para Monitoramento Remoto de Pacientes

Este repositório contém o protótipo de um sistema IoT para monitoramento remoto de sinais cardíacos, utilizando **ESP32**, **sensor de ECG (AD8232 ou potenciômetro no Wokwi)**, **LED** e **buzzer**, com comunicação pela internet via **Wi-Fi (TCP/IP)** e **protocolo MQTT**.

O projeto foi desenvolvido como parte de um trabalho da disciplina de OBJETOS INTELIGENTES CONECTADOS, alinhado ao **ODS 3 – Saúde e Bem-estar**, com foco em monitoramento contínuo e geração de alertas locais e remotos.

---

## 1. Visão geral do sistema

O sistema:

- Lê continuamente um sinal analógico de ECG (AD8232 ou um potenciômetro simulando o sensor).
- Verifica se o sinal está dentro de uma faixa considerada normal.
- Em caso de anomalia:
  - Acende o **LED** (alerta visual).
  - Após 2 segundos de persistência, aciona o **buzzer** (alerta sonoro).
  - Publica uma mensagem de alerta em um tópico MQTT.
- Publica periodicamente os valores do sinal no broker MQTT para monitoramento remoto.
- Permite **controle manual** do LED e do buzzer via comandos MQTT (ex.: `RESET`, `LED_OFF`, `BUZZER_ON`).

---

## 2. Arquitetura resumida

- **Camada de dispositivo (edge)**: ESP32 + sensor de ECG (ou potenciômetro) + LED + buzzer.
- **Conectividade**: Wi-Fi (TCP/IP) integrado ao ESP32.
- **Protocolo de aplicação**: MQTT.
- **Broker MQTT**: `test.mosquitto.org` (broker público da Eclipse Foundation).
- **Cliente MQTT para testes**: MQTTX (ou similar).

Os tópicos MQTT utilizados são:

- `iot/monitor/ecg` → publicação dos valores do sinal (ECG).
- `iot/monitor/alert` → publicação de alertas em caso de anomalia.
- `iot/monitor/cmd` → recepção de comandos (ex.: `RESET`, `LED_OFF`, `LED_ON`, `BUZZER_ON`, `BUZZER_OFF`).

Mais detalhes em [`docs/comunicacao_mqtt.md`](docs/comunicacao_mqtt.md).

---

## 3. Hardware utilizado

Resumo dos componentes:

- **ESP32 DevKit V1** – microcontrolador com Wi-Fi integrado.
- **Sensor AD8232 de ECG** (ou potenciômetro no Wokwi para simulação).
- **LED 5mm vermelho** – alerta visual.
- **Buzzer ativo 5V** – alerta sonoro.
- Protoboard, jumpers e fonte/USB.

A descrição detalhada (incluindo funções e ligações) está em [`docs/hardware.md`](docs/hardware.md).

---

## 4. Como reproduzir o projeto

### 4.1. Pré-requisitos

- **IDE Arduino** instalada.
- **Placa ESP32** configurada na IDE (Board Manager).
- Biblioteca Wi-Fi e MQTT (ex.: `WiFi.h`, `PubSubClient.h`).
- Acesso a uma rede **Wi-Fi**.
- Cliente MQTT (ex.: **MQTTX**, MQTT Explorer ou outro).
- Opcional: conta no **Wokwi** e arquivo de simulação deste repositório.

### 4.2. Clonar o repositório

```bash
git clone https://github.com/duuranh-coder/IoT-Heartbeat-Monitor.git
cd iot-monitoramento-pacientes
