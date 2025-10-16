# FarmTech Solutions - Fase 2: Sistema de Irrigação Inteligente

## Integrantes do Grupo
- Nome do Aluno 1 - RM
- Nome do Aluno 2 - RM
- ...

## 1. Introdução
Este projeto simula um dispositivo IoT para automação da irrigação em uma fazenda inteligente. O sistema utiliza um ESP32 para coletar dados de sensores (simulados) de umidade do solo, pH e níveis de nutrientes (NPK) para tomar decisões sobre quando acionar uma bomba d'água.

## 2. Cultura Agrícola e Lógica de Decisão
A cultura escolhida para este projeto foi o **Tomate**. A lógica para acionar a irrigação foi baseada nas seguintes necessidades da planta:
- **Umidade do Solo:** A irrigação é acionada se a umidade cair abaixo de 60%.
- **pH do Solo:** O sistema só irriga se o pH estiver na faixa ideal de 6.0 a 6.8.
- **Nutrientes (NPK):** Todos os três macronutrientes (N, P, K) devem estar em níveis adequados (botões pressionados).
- **Resumo:** A bomba só liga se todas as condições acima forem atendidas.

## 3. Circuito no Wokwi
O circuito foi montado na plataforma Wokwi.com utilizando um ESP32 e os seguintes componentes...

**(Insira aqui o print do seu circuito)**

Link para a simulação: [Link do seu projeto Wokwi aqui]

## 4. Funcionamento do Código
O código do ESP32 (`FarmTech_Fase2.ino`) está estruturado em:
- **Setup:** Inicializa os sensores e define os pinos.
- **Loop:**
    1. Realiza a leitura contínua dos sensores.
    2. Converte o valor do LDR para uma escala de pH (0-14).
    3. Exibe os dados no Monitor Serial para depuração.
    4. Aplica a lógica de decisão e aciona ou desaciona o relé.

## 5. "Ir Além": Integração com API de Clima
(Se aplicável) Foi desenvolvido um script em Python (`weather_check.py`) que consulta a API OpenWeatherMap para verificar a previsão de chuva. Se há previsão, a irrigação é suspensa para economizar água. A integração foi feita de forma manual, onde o resultado do script informa a decisão a ser tomada na simulação.

