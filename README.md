# Sistema de Monitoramento de Luminosidade com LDR e STM32

## Sobre o projeto

Este projeto consiste no desenvolvimento de um sistema embarcado para monitoramento da luminosidade utilizando um **sensor LDR (Light Dependent Resistor)** e o microcontrolador **STM32L031K6T6**, desenvolvido e simulado na plataforma **Wokwi**.

O sistema realiza a leitura analógica do sinal proveniente do LDR e, de acordo com o valor obtido pelo conversor analógico-digital (ADC), aciona um dos três LEDs utilizados como indicadores visuais. Os valores das leituras também são enviados ao **Monitor Serial**, permitindo acompanhar o comportamento do sensor durante a simulação.

## Objetivos

* Realizar a leitura de um sensor LDR utilizando o STM32;
* Compreender o funcionamento de uma entrada analógica;
* Processar os valores obtidos pelo ADC;
* Utilizar limiares para classificação das leituras;
* Controlar LEDs por meio de saídas digitais;
* Monitorar os valores obtidos através da comunicação serial;
* Simular o funcionamento do sistema utilizando o Wokwi.

## Componentes utilizados

* STM32L031K6T6;
* Sensor LDR;
* LED verde;
* LED amarelo;
* LED vermelho;
* Resistor de 1K OHMS;
* Plataforma Wokwi.

## Funcionamento do circuito

O sensor LDR é conectado à alimentação de **3,3 V** e ao **GND**, enquanto sua saída analógica (**AO**) é conectada à entrada analógica **A0** do microcontrolador. A saída digital **DO** do módulo não é utilizada.

Os três LEDs são utilizados para fornecer um feedback visual das leituras realizadas pelo sistema. O programa compara o valor obtido pelo ADC com os limites definidos e aciona o LED correspondente:

| Leitura do ADC  | LED acionado |
| --------------- | ------------ |
| Menor que 350   | 🟢 Verde     |
| Entre 350 e 700 | 🟡 Amarelo   |
| Maior que 700   | 🔴 Vermelho  |

> **Observação:** o valor exibido pelo `analogRead()` não corresponde diretamente à intensidade luminosa em lux. O valor configurado em lux no sensor do Wokwi é convertido pelo modelo do LDR em uma resposta elétrica, que posteriormente é interpretada pelo ADC do microcontrolador.

## Funcionamento do código

O programa inicializa a comunicação serial com velocidade de **115200 baud** e configura os pinos dos LEDs como saídas digitais.

Durante a execução, o microcontrolador realiza uma leitura analógica do LDR utilizando:

```cpp
analogRead(0)
```

O valor obtido é comparado com os limites de **350** e **700**. De acordo com a faixa identificada, um dos LEDs é acionado. Após isso, o valor da leitura é enviado ao Monitor Serial e o sistema aguarda **1 segundo** antes de realizar uma nova leitura.

## Fluxo de funcionamento

```text
        Sensor LDR
            ↓
     Leitura analógica
            ↓
        ADC / STM32
            ↓
    Comparação do valor
       ↙      ↓      ↘
   < 350   350–700   > 700
      ↓       ↓        ↓
   🟢 Verde 🟡 Amarelo 🔴 Vermelho
            ↓
      Monitor Serial
            ↓
       Aguarda 1s
            ↓
          Repete
```

## Resultados

Durante a simulação, foi possível observar que a variação da luminosidade configurada no sensor altera o valor retornado pelo ADC. Por exemplo, uma luminosidade elevada pode resultar em uma leitura analógica baixa, enquanto uma luminosidade reduzida pode resultar em uma leitura analógica elevada.

O acionamento dos LEDs permitiu representar visualmente as diferentes faixas da leitura, enquanto o Monitor Serial possibilitou acompanhar os valores numericamente durante a execução.


## 👩‍💻 Autora

**Anna Beatriz Pena**
Projeto acadêmico — Engenharia da Computação.
