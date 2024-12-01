
# `<Home Security Project EA076>`

## Apresentação

O presente projeto foi originado no contexto das atividades da disciplina de graduação *EA076 - Laboratório de Sistemas Embarcados*, visando o uso da placa BitDogLab para aumentar nossos conhecimentos
nos sistemas embarcados.



  
## Descrição do Projeto
 O objetivo principal deste projeto é criar um sistema de segurança eficiente, focado em casas de menor porte, mas que também possa ser otimizado para residências maiores. O sistema de segurança proporciona 
  conforto aos moradores. Ele inclui funcionalidades como: sensor de distância para detecção de presença, permitindo monitoramento conforme desejado pelo usuário e podendo também acionar um alarme 
 sonoro, se desejado (por exemplo, ao sair de casa); sensor de gás e fumaça com alerta ao usuário, ativado ao detectar níveis potencialmente perigosos e sensor de temperatura e umidade
 de fumaça e sensor de temperatura e umidade, informando constantemente ao usuário do estado atual do dia.


## Descrição Funcional
Sistema de Segurança:
O sistema de segurança inclui 2 funções, primeiro temos o sistema em si, ele monitorará seu estado de ligado ou desligado de acordo com o que o usuário quiser, se ele for ativado enquanto a porta está aberta, ele irá fechar a porta e ligar e sistema de segurança ao mesmo tempo. Também temos a função de mudança de estado da porta do outro botão, porém, ele irá primeiro olhar se o sistema de segurança está ativado, caso o sistema de segurança esteja ativado irá manter o estado da porta anterior, caso contrário, muda o estado da porta a vontade do usuário.

Sensor de Distância:
O sensor de distância é usado como sensor de presença, é estabelecida uma distância base para conseguir perceber que uma distância diferente a essa significa uma presença detectada, ao detectar a presença irá a enviar a mensagem de presença detectada e se desejado pelo usuário poderá acionar o sistema de segurança.

Sensor de Temperatura e Umidade:
O sensor de temperatura e umidade funciona constantemente transmitindo informações a cada atualização, por enquanto está o funcionamento padrão é atualizar os dados a cada segundo porém pode ser modificado diretamente no código.

Sensor de Gâs e fumaça:
O sensor de gâs e fumaça funciona com monitoramento constante do ambiente, ao valor passar o limiar, significa que foi reconhecido o valor mínimo para que o sensor de fato esteja detectando gâs ou fumaça e irá enviar um alerta ao usuário.

Raspberry Pi Pico W: 
O Raspberry Pi Pico W é o núcleo do sistema, coordenando a operação de todos os sensores, atuadores e a placa. Junto com a placa, oferecem várias portas I/O, alta capacidade de processamento e flexibilidade para futuras expansões e também oferece a conexão Wi-fi que era necessária para nosso projeto. Ele facilita a integração de múltiplos sensores e dispositivos de saída, garantindo que o sistema seja robusto e escalável.


### Configurabilidade

Configuração de Alarmes: É possível definir quando os alarmes sonoros devem ser ativados, como por exemplo, apenas quando o sistema de segurança esteja ativado.

Notificações Personalizadas: Os moradores podem configurar o sistema para receber notificações alerta via servidor web.


### Eventos

#### Eventos Periódicos:

Verificação de Níveis de Gás e Fumaça : Monitoramento contínuo dos níveis de gás e fumaça no ambiente.

Leitura de Temperatura: O sensor realiza leituras de temperatura em intervalos regulares de 1 segundo.

Verificação do estado da porta e sistema de segurança: Monitoramento continuo do estado de ambos.

#### Eventos Não Periódicos:

Detecção de Presença: Ativado quando um movimento é detectado.

Alerta de Gás ou Fumaça: Ativado ao detectar níveis perigosos de gás ou fumaça.

Mudar estado da porta: Com o botão, muda estado da porta, somente irá mudar o estado se o sistema de segurança estiver desligado, também será mudado caso a porta esteja aberta e o sistema de segurança seja ligado.

Mudar estado sistema de segurança: Desliga ou liga o sistema de segurança de acordo ao que usuário preferir no momento.



#### Blocos Funcionais
##### Sensores:

Sensor de Presença: Detecta movimento e envia sinais ao controlador central.

Sensor de Gás: Monitora a concentração de gás e fumaça no ambiente e envia um sinal ao controlador quando níveis perigosos são detectados.


Sensor de Temperatura: Monitora a Temperatura do ambiente e envia um sinal para controlador da informação lida.

#### Controlador Central

Microcontrolador: O núcleo do sistema, responsável por receber sinais dos sensores, processar esses sinais e tomar decisões com base na programação interna. 

#### Unidades de Alerta

LED de Indicação: Podem ser configurados os leds da matriz ou da placa para acender para indicar a detecção de presença.

Alarmes Sonoros: Buzzers podem ser ativados em resposta a sinais dos sensores de gás e fumaça, ou conforme configurado pelo usuário para o sensor de presença.

Display de LCD: Pode ser configurado para apresentar de forma clara e instantânea a temperatura ambiente aos moradores.


## Especificações 

### Especificação Estrutural

#### Sensores 

Sensores de Presença:
O sensor escolhido é o HC-SR501, um sensor infravermelho com alimentação recomendada de 5V DC. Sua saída é um pulso digital: 1 (3,3V) quando detecta movimento e 0 (0V) quando não há movimento. A sensibilidade do sensor é configurável, permitindo distinguir entre a movimentação de objetos e de pessoas. O principal motivo para sua escolha é o alcance, que chega a 7 metros, com um ângulo de 120 graus, permitindo cobrir todo o cômodo e uma parte principal do quintal ou da entrada da casa. O sensor possui um baixo consumo de energia, aproximadamente 65mA, e funciona em uma faixa de temperatura de -20 a 80 graus Celsius, sendo adequado para uso no Brasil e em outras regiões com condições climáticas variadas.

Sensor de Gás e Fumaça:
O sensor escolhido é o MQ-2 possui alimentação recomendada de 5V DC, ele monitora ocorrências de vazamento de gás e de fumaça, sendo especialmente benéfico para nosso projeto em áreas como a cozinha. O ajuste de sensibilidade é feito via potenciômetro, facilitando seu uso. Possui analógica baseada na variação de resistencia sendo necessário um conversor ADC ou uma entrada analógica, no nosso caso, a bitdoglab tem a entrada analógica necessária, permitindo uma comunicação mais simples com a unidade de controle. Consome pouca energia, contribuindo para a eficiência energética do sistema. É um sensor de baixo custo, o que é vantajoso para a viabilidade econômica do projeto.

Sensor de Temperatura e Umidade

O sensor escolhido é o  AHT10, um sensor de temperatura e umidade. Ele possui uma alimentação recomendada de 3.3 - 5V DC e usa uma interface I2C, também disponivel na bitdoglab.
O AHT10 tem uma faixa de medição que vai de -40 a +85 graus Celsius e umidade de 0% a 100%. O principal motivo para a escolha deste sensor é sua precisão de ±0,3 graus nas medições graus Celsius e precisão de ±0.024%, podendo ter uma resolução maior, que atende aos requisitos do nosso projeto.


#### Atuadores

Matriz de LEDs: A BitDogLab contém uma Matriz de LEDs para identificação visual do que o usuário preferir, no nosso caso, optamos por usar ele para mostrar o estado da porta.

Alarme Sonoro: um buzzer poderá ser ativado em caso de possíveis invasões quando os donos não estiverem na residência, ou se for identificada uma alta concentração de fumaça ou gás de cozinha. Isso fornecerá um alerta audível para os ocupantes da casa ou para vizinhos, indicando uma situação de emergência.

Display LCD: um Display poderá ser utilizado para exibir a temperatura medida pelo sensor de temperatura e umidade. Isso permitirá que os ocupantes monitorem a temperatura em tempo real, o que pode ser útil para garantir o conforto e a segurança, especialmente em situações como controle de temperatura ambiente ou detecção de superaquecimento em determinadas áreas.


#### Conexões Usadas

Sensor de Temperatura e Umidade: Pin 1 e 0 correspondente ao I2C.

Servomotor : GPIO 17.

Sensor de Presença: GPIO 9 para Trigger, GPIO 16 para Echo.

Sensor de Gas: GPIO 28, entrada analógica disponivel.

O resto das conexões 5V e terra foram usadas diretamente da bitdoglab conectada com a placa personalizada.




