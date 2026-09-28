# Nyquist, Taxa de Símbolos e Taxa Útil, com Dados Reais

Neste laboratório, vocês analisaram a gravação real de um transmissor de rádio e comparam
três taxas distintas do mesmo sistema:

| Taxa | O que representa | 
|---|---|
| Limite de Nyquist | Teto teórico que a banda do canal permite | 
| Taxa de símbolos | Velocidade com que o protocolo transmite | 
| Taxa útil (goodput) | Informação efetivamente entregue por segundo | 


Spoiller, ao longo do curso veremos a relação com:
   - modulação (assunto da proxima aula)
   - e os protocolos de camdas superiores (especialmente da camada 7)

Ao final do laboratório, o aluno deve ser capaz de:

- Distinguir símbolo, baud e bit por segundo, e explicar quando as duas últimas coincidem.
- Aplicar o teorema de Nyquist na forma geral, incluindo o termo de níveis por símbolo.
- Medir a largura de banda de um sinal real a partir do seu espectro, distinguindo sinal de
  ruído do receptor.
- Calcular a taxa útil (goodput) e explicar por que ela difere da taxa bruta de transmissão.
- Relacionar decisões de projeto de um sistema embarcado (energia, ambiente, ausência de canal
  de retorno) com as características observadas no sinal.
- Não confundir a taxa de amostragem do receptor com a largura de banda do sinal.

Requisitos técnicos: Python 3 com `numpy`, `scipy` e `matplotlib`.

## Dados utilizados

O sinal analisado é a gravação de um sensor **TPMS** (*Tire Pressure Monitoring System*),
modelo Jansite TY02S, operando em 433,92 MHz. O sensor fica instalado dentro do pneu do
veículo e transmite pressão e temperatura ao computador de bordo.

As restrições de engenharia desse dispositivo são o fio condutor pedagógico do laboratório:
bateria lacrada que deve durar anos, ambiente metálico e em rotação, e ausência total de canal
de retorno, ou seja, o sensor nunca recebe confirmação de recebimento. A última restrição
explica diretamente o comportamento que os alunos observarão na medição de goodput.

Parâmetros documentados do protocolo:

| Parâmetro | Valor |
|---|---|
| Frequência de operação | 433,92 MHz ± 38 kHz |
| Modulação | FSK binária |
| Duração de cada símbolo | 52 µs, ou seja, 19,23 kbaud |
| Tamanho do pacote | 7 bytes, ou seja, 56 bits |

Os dados foram capturados por um RTL-SDR e está publicada no banco de testes aberto do
projeto de código aberto `rtl_433`, disponível em
<https://github.com/merbanan/rtl_433_tests>. 


