# VSSS Communication Base - RASPBERRY PI PICO & NRF24L01 🛰️

Este repositório contém o projeto de hardware (PCB) da base emissora/receptora desenvolvida para a equipe **roboAp (UTFPR - Apucarana)**. O módulo é responsável pelo link de comunicação entre a estação de processamento (PC) e os robôs da categoria **Very Small Size Soccer (VSSS)**.

## 📋 Visão Geral

A placa atua como um dongle USB de alto desempenho. Ela utiliza o processamento do **RP2350** para gerenciar o tráfego de dados e o rádio **NRF24L01** para a transmissão em tempo real, garantindo baixa latência nos comandos de trajetória.

## 🛠 Especificações de Hardware

* **Microcontrolador:** PI PICO 2 RP2350
* **Transceptor:** NRF24L01+ (2.4 GHz)
* **Alimentação:** Barramento USB (5V)
* **Interface:** Serial-to-SPI Bridge

## 📐 Destaques do Design (Layout & RF)

O projeto foca na integridade do sinal e na redução de ruído eletromagnético (EMI), considerando o ambiente crítico de competições:

* **RF Overhang (Antena em Balanço):** O conector do NRF24L01 foi posicionado na borda da PCB com o transceptor em balanço (*overhanging*). Isso projeta a antena para fora da área da placa, eliminando a absorção de sinal pelo plano de cobre.
* **Isolamento de Camadas:** Roteamento de sinais e trilhas de alimentação realizado na camada inferior (**B.Cu**), mantendo o módulo de rádio na camada superior (**F.Cu**) para minimizar o acoplamento parasita.
* **Filtragem de Transientes:** Preparada para a inclusão de capacitores de desacoplamento (**100nF cerâmico** e **10µF eletrolítico**) próximos aos pinos de alimentação do NRF. Essencial para estabilizar os picos de corrente durante a transmissão.
* **EMC Optimization:** Firmware configurado para desativar os rádios internos do ESP32 (WiFi/Bluetooth), focando os recursos de energia e processamento exclusivamente no protocolo SPI do rádio externo.

## 📂 Estrutura do Repositório

* `/Hardware`: Arquivos de projeto da PCB (KiCad/EasyEDA), Esquema Elétrico e Gerbers.
* `/Firmware`: Código fonte para a ponte serial e configuração de baixa latência do NRF24L01.
* `/Docs`: Relatórios de testes de bancada e medições de performance.

## 🔧 Configuração e Uso

1. **Firmware:** Ao carregar o código, certifique-se de utilizar `WiFi.mode(WIFI_OFF)` para garantir a estabilidade do link de RF.
2. **Conexão:** Plugue via USB e utilize o terminal (ou software de estratégia) para enviar os comandos via porta Serial.
3. **Hardware:** Recomendado o uso de capacitores de filtro se a comunicação apresentar perda de pacotes (*Packet Loss*) em distâncias superiores a 2 metros.

## 👥 Créditos

* **Desenvolvedor:** Michel Rochytor Lima Barbosa
* **Instituição:** UTFPR - Campus Apucarana
* **Equipe:** [roboAp - Robotics Team](https://github.com/roboap)

---
Projeto desenvolvido sob licença MIT.
