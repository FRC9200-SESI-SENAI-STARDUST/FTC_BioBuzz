# Mecanismo de FLOWER

FLOWER parece um mecanismo separado porque exige outra geometria de pontuação. Isso não significa que ele precisa ser uma segunda máquina inteira dentro do robô.

## Objetivo mecânico

O elemento precisa chegar por cima, em uma abertura relativamente pequena e a aproximadamente 54,6 cm do piso. Uma solução inicial segura é:

* elevador curto ou braço simples;
* bucket ou passagem controlada;
* guia passiva de alinhamento;
* posição de recolhimento bem definida.

Não tente lançar à distância antes de provar que depositar de perto é lento demais. Uma solução curta e repetível quase sempre chega aos treinos antes.

## Alinhamento passivo

Um funil côncavo pode transformar alguns centímetros de erro em contato controlado. Ele deve guiar, não prender nem apoiar o robô de forma ilegal. Confirme a regra atual e teste aproximações tortas.

Às vezes um pedaço pequeno de plástico resolve o que uma câmera resolveria com latência, calibração e processamento. Não é uma disputa entre mecânica e software. É a busca pela solução que continua funcionando quando o resto da partida está barulhento.

## Elevator ou braço

| Opção | Vantagem | Atenção |
| --- | --- | --- |
| Elevator curto | movimento previsível | folga, sincronismo e cabo |
| Braço pivotante | poucas peças lineares | torque muda com o ângulo |
| Four-bar | orientação do bucket | mais juntas e tolerâncias |

Adicione batentes físicos. O limite de extensão não pode depender só de software. Se usar motor, inclua encoder e homing. Se usar servo, garanta que ele não fique forçando contra um batente durante toda a partida.

## Sequência de estado

```text
STOW
> PREP_FLOWER
> ALIGNED
> SCORE
> STOW
```

Cada transição precisa de condição. O elevador não sobe se a saída estiver bloqueada. O bucket não abre antes da altura. O mecanismo não recolhe enquanto o elemento ainda pode cair dentro do robô.

## Teste

Pontue vinte vezes de frente, dez deslocado para cada lado e dez após uma colisão leve controlada. O mecanismo está pronto quando o piloto não precisa olhar para ele para saber se terminou.

