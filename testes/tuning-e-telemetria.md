# Tuning, telemetria e logs

Sem medição, tuning vira uma conversa entre sensações. “Parece lento”, “acho que passou um pouco”, “ontem estava melhor”. A telemetria existe para dar forma a isso.

## O que mostrar

```text
LOOP
tempo do ciclo
tensão da bateria

POSE
x, y, heading

SHOOTER
target RPM, actual RPM, erro, derivada, pronto

INTAKE
contador, sensores, modo, anti-jam

VISION
alvo, distância, lateral, yaw, idade do frame

SUPERSTRUCTURE
estado pedido, estado ativo, interlock, falha
```

Não envie tudo em toda iteração se isso derrubar o loop. Atualize o painel em frequência menor e salve logs com cuidado. Telemetria demais pode virar o próprio problema que tentava encontrar.

## Medidor de loop

```java
long now = System.nanoTime();
double dt = (now - previousLoopNs) / 1e9;
previousLoopNs = now;

telemetry.addData("loop_ms", dt * 1000.0);
```

Observe média, máximo e picos. Um loop normal rápido com pausas enormes ainda prejudica derivada, odometria e resposta.

## Formato de log

```text
timestamp,target,measurement,error,output,battery,state
```

Inclua unidade no cabeçalho ou na documentação. Não misture graus e radianos, metros e polegadas, RPM e ticks por segundo.

## Sessão de tuning

1. Defina uma pergunta: “qual é o settling time do shooter?”
2. Trave todas as outras variáveis.
3. Faça várias tentativas.
4. Salve os dados.
5. Compare gráfico de alvo, medição e saída.
6. Mude uma constante.
7. Repita nas mesmas condições.

## Métricas úteis

* rise time;
* overshoot;
* settling time;
* erro estacionário;
* pico de corrente;
* variação com tensão;
* dispersão entre tentativas.

Uma única curva bonita não prova repetibilidade. Compare dez. O robô real não entrega o mesmo atrito todos os dias, e é justamente essa variação que o controle precisa atravessar.

## Registro de alteração

Para cada tuning, anote:

```text
data
commit do código
configuração mecânica
constantes antigas e novas
bateria
resultado
decisão
```

Sem o commit, você pode guardar um gráfico excelente de um robô que já não existe mais.

