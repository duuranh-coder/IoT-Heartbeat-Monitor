# IoT Heartbeat Monitor – Scenario 2 (MQTT)

Este repositório contém o projeto "IoT Heartbeat Monitor – Scenario 2 (MQTT)", desenvolvido como parte da disciplina Objetos Inteligentes Conectados.

O sistema monitora um sinal de ECG simulado, identifica anomalias e envia alertas via MQTT, permitindo também controle remoto de atuadores (LED e buzzer).

---

## 🎯 Objetivo do Projeto

Criar um protótipo IoT capaz de:

- Ler continuamente um sinal cardíaco (simulado com potenciômetro no Wokwi).
- Detectar anomalias com base em limites pré-definidos.
- Gerar alertas locais (LED e buzzer).
- Publicar dados e alertas via MQTT.
- Receber comandos remotos (LED_ON, BUZZER_OFF, RESET, etc.).
- Demonstrar uma arquitetura IoT completa: sensor → ESP32 → Wi-Fi → MQTT → cliente remoto.

---

## 📂 Estrutura do Repositório

```
.
├─ README.md
├─ codigo-esp32/
│  └─ sketch.ino
├─ wokwi/
│  ├─ diagram.json
│  ├─ libraries.txt
│  └─ projeto-wokwi.txt
└─ docs/
   ├─ arquitetura.md
   ├─ hardware.md
   ├─ comunicacao_mqtt.md
   └─ projeto-esp32-fisico.txt
```

---

## 🌐 Comunicação via Internet / MQTT

O projeto utiliza:

- Wi-Fi para comunicação TCP/IP.
- Broker MQTT público: test.mosquitto.org
- Tópicos:
  - Publicação dos valores de ECG: iot/monitor/ecg
  - Publicação de alertas: iot/monitor/alert
  - Recebimento de comandos: iot/monitor/cmd

Documentação completa da comunicação está em:
- docs/comunicacao_mqtt.md

---

## 🖥️ Rodando no Wokwi (Simulação)

Resumo:

1. Acesse o Wokwi (https://wokwi.com).
2. Importe os arquivos da pasta "wokwi" (diagram.json e libraries.txt).
3. Cole o código de codigo-esp32/sketch.ino no editor do Wokwi.
4. Clique em "Play" para iniciar a simulação.
5. Opcional: use um cliente MQTT externo (por exemplo, MQTTX) para assinar e enviar comandos.

Guia passo a passo detalhado:
- wokwi/projeto-wokwi.txt

---

## ⚙️ Rodando em um ESP32 Físico

Resumo:

1. Abra o arquivo codigo-esp32/sketch.ino na Arduino IDE.
2. Ajuste os dados da rede Wi-Fi:
   - ssid = "NOME_DA_SUA_REDE"
   - password = "SENHA_DA_SUA_REDE"
3. Mantenha o broker MQTT como test.mosquitto.org, porta 1883.
4. Faça o upload para o ESP32.
5. Use um cliente MQTT (como MQTTX) para assinar os tópicos e enviar comandos.

Guia detalhado:
- docs/projeto-esp32-fisico.txt

---

## 🔌 Hardware Utilizado

Principais componentes:

- ESP32 DevKit V1.
- Potenciômetro simulando o sinal de ECG (no Wokwi).
- LED de indicação (GPIO 25).
- Buzzer de alerta (GPIO 26).

Detalhes de ligações, pinos e alimentação:
- docs/hardware.md

---

## 🧱 Arquitetura do Sistema

Descrição da arquitetura em camadas, fluxo de funcionamento e lógica principal do sistema:
- docs/arquitetura.md

---

## 📡 Tópicos MQTT e Protocolo

Descrição dos tópicos utilizados, payloads, comandos aceitos e fluxo MQTT:
- docs/comunicacao_mqtt.md

---

## 👨‍💻 Autores

- Alecsei da Costa  
- Victor Duran  

Projeto desenvolvido para a disciplina Objetos Inteligentes Conectados – Mackenzie.

---

## 📘 Licença

Uso acadêmico.
