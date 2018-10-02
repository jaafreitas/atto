# ATTO Educacional
Informações sobre o [Kit Robótica Educacional ATTOBOX (KTR-13)](http://attoeducacional.com.br/produtos/#KTR13).

# Instalação Arduino + Ardublock
O Ardublock oficial atualmente só funciona com versões mais antigas da IDE do Arduino. Recomendamos a seguinte configuração:
* [Arduino 1.6.9](https://downloads.arduino.cc/arduino-1.6.9-windows.exe)
* [Ardublock 20130712](https://ufpr.dl.sourceforge.net/project/ardublock/ardublock-all-20130712.jar)

Abaixo temos uma versão do Arduino 1.6.9 com o Ardublock já configurado. Para utilizar é só descompactar em uma pasta e iniciar o aplicativo do arduino que está dentro da nova pasta gerada.
* [Arduino 1.6.9 + Ardublock 20130712](https://github.com/jaafreitas/atto/releases/download/v1.0/arduino-1.6.9-windows.ardublock.zip)

# Capacitação
* [Apresentação na formação de professores em maio de 2018 na Rede Municipal de São Paulo](https://docs.google.com/presentation/d/1-66BY88nIFKMLU0I78xY9dok_Q6FcfNTvEGfrUrLoSI/edit?usp=sharing)
* [Módulo introdutório para os POIEs da Rede Municipal de São Paulo](https://docs.google.com/presentation/d/1inzewvjghmF-ega02I1XdL2QNajITBSi9WvUowwFNfA/edit?usp=sharing)

# Exemplos Ardublock
## [Blink](ExemplosArdublock/01.%20Blink.abp)
Faz o acionamento de um atuador digital de forma cíclica. Serve por exemplo para fazer um LED ficar piscando.

## [AnalogReadSerial](ExemplosArdublock/01.%20AnalogReadSerial.abp)
Faz a leitura de um sensor analógico e escreve o seu valor entre 0 e 1023 no Monitor Serial

## [AnalogInOutSerial](ExemplosArdublock/03.%20AnalogInOutSerial.abp)
Faz a leitura de um sensor analógico e escreve o seu valor entre 0 e 1023 no Monitor Serial. Além disso, faz a conversão para os valores compreendidos pelos atuadores analógicos e também escreve no Monitor Serial.

## [AnalogReadVoltage](ExemplosArdublock/01.%20AnalogReadVoltage.abp)
Faz a leitura de um sensor analógico e escreve o valor em volts no Monitor Serial. Serve como um multímetro/voltímetro que consegue ler valores entre 0V e 5V.

## [DigitalReadSerial](ExemplosArdublock/01.%20DigitalReadSerial.abp)
Faz a leitura de um sensor digital e escreve o seu valor (0 ou 1) no Monitor Serial, onde 1 significa que o sensor foi acionado. Utilizado por exemplo para verificar o estado de um botão.

## [ServoSweep](ExemplosArdublock/ServoSweep.abp)
Faz o servo ficar se mexendo entre 0 e 180 graus e depois entre 180 graus até 0 para sempre.

## [ServoKnob](ExemplosArdublock/ServoKnob.abp)
Faz o controle do servo a partir de um sensor analógico, como por exemplo um potenciômetro.

## [Demo](ExemplosArdublock/Demo.abp)
Demonstração de diversas funcionalidade no mesmo programa, entra ela temos:
* Botão / chave magnética (sensor digital) acende um LED (atuador digital)
* Potenciômetro (sensor analógico) controla um servo motor (protocolo digital)
* Luminosidade (sensor analógico) controla um MotorDC (atuador PWM)
* Sensor de distância ultrasônico (protocolo digital) controla um Buzzer (protocolo digital)

# [Módulo Bluetooth XBee (HC-06)](#bluetooth)
O módulo bluetooth deve ser encaixado dentro do AttoBox. Para isso, remova a tampa com as legendas e encaixe o módulo seguindo a orientação do desenho em branco na placa verde.

A seguir temos uma programação em C++ para Arduino que pode ser utilizada para testes iniciais. Para enviar esta programação, certifique-se que a chave bluetooth no AttoBox está na posição 2. Após feita a programação, mude a chave para a posição 1 para poder utilizar o módulo bluetooth. Este procedimento é necessário toda a vez que uma nova programação for feita.
```cpp
void setup() {
  Serial.begin(9600);
}

void loop() {
  while (Serial.available()) {
    digitalWrite(LED_BUILTIN, HIGH);
    Serial.print(".");
    Serial.readString();
    delay(1000);
  }
  digitalWrite(LED_BUILTIN, LOW);        
  delay(100);
}
```
O programa começa com a definição da velocidade da comunicação serial em 9600 bps. Quando recebemos qualquer comunicação por bluetooth, o LED interno ascende por 1 segundo. Caso exista alguma espécie de terminal no programa utilizado, este mostrará um ponto para confirmar o recebimento dos dados.

Note que o módulo bluetooth HC-06 funciona apenas em modo escravo, ou seja, ele aguarda uma conexão de um outro dispositivo bluetooth como um computador, celular Android ou outros módulos bluetooth como o HC-05. Atenção: não funciona com iPhones ou outros dispositivos que sejam exclusivamente Bluetooth 4.0 (BLE).

Para testar a comunicação, utilize um celular Android com qualquer programa com suporte ao bluetooth como por exemplo o BLEJoystick. Após estabelecer a comunicação bluetooth, o LED do módulo bluetooh que está dentro do AttoBox ficará acesso direto.
