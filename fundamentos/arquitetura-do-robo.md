# Arquitetura do robô

Uma arquitetura boa não é a que coloca mais mecanismos dentro do volume. É a que cria um caminho claro para o elemento e deixa poucas oportunidades para ele escolher o caminho errado.

## Conceito inicial

Para uma equipe buscando desempenho sem inventar dificuldade cedo demais:

* drivetrain mecanum;
* intake frontal largo e flexível;
* magazine com quatro posições controladas;
* shooter com velocidade fechada e ângulo regulável;
* mecanismo curto e independente para FLOWER;
* câmera frontal alinhada ao sistema de pontuação;
* odometria independente das rodas mecanum, quando possível.

O fluxo principal deve ser simples:

```text
INTAKE > INDEXADOR > MAGAZINE > SELETOR > SHOOTER
                                      > FLOWER
```

Quanto mais o elemento troca de direção, mais lugares existem para travar. Quanto mais mecanismos tentam segurá-lo ao mesmo tempo, mais difícil fica saber quem está realmente no controle.

## Distribuição inicial de atuadores

Um exemplo dentro do limite de oito motores:

| Função | Motores |
| --- | ---: |
| Drivetrain | 4 |
| Intake | 1 |
| Shooter | 2 |
| Elevator ou indexador | 1 |

Servos podem cuidar do hood, gate, bucket do FLOWER e deploy do intake. Isso é apenas um ponto de partida. Se um mecanismo puder ser passivo e continuar confiável, ele devolve peso, energia e tempo de programação para o restante do robô.

## Envelope

No início da partida, o robô deve caber em aproximadamente `18 x 18 x 18 pol.`. Depois, a expansão física continua limitada e não pode depender apenas de software. Crie dois corpos de referência no CAD:

* envelope inicial;
* envelope expandido.

Deixe os dois visíveis durante o projeto. A peça que invade o envelope por dois milímetros continua invadindo, mesmo que tenha levado três semanas para ser desenhada.

## Centro de massa e manutenção

Mantenha bateria e componentes pesados baixos. Evite concentrar todo o peso na frente junto do intake. Reserve acesso direto para:

* bateria e chave principal;
* Control Hub e Expansion Hub;
* conectores USB;
* parafusos de roda;
* correias e correntes;
* motores do intake e shooter;
* sensores que podem sair de posição.

## Revisão antes de fabricar

Pergunte para o modelo CAD:

1. O elemento consegue atravessar o robô sem cantos mortos?
2. Uma peça flexionando pode encostar em outra?
3. Há ajuste suficiente para correia, compressão e alinhamento?
4. O mecanismo possui batente físico?
5. O motor pode ser removido com ferramentas comuns?
6. A fiação acompanha o movimento sem ser esmagada?
7. A estrutura continua rígida após uma colisão?

O CAD não é um armário onde cada peça precisa caber de qualquer jeito. Ele é o primeiro teste do robô. Se o caminho já parece apertado na tela, ele será ainda pior quando existirem parafusos, cabos, folgas e poeira.

