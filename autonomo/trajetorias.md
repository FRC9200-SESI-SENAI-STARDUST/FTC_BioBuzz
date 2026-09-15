# Trajetórias e path following

Uma trajetória descreve onde o robô deveria estar, com que velocidade deveria passar e para onde deveria apontar. Um follower compara esse desejo com a pose medida e produz `vx`, `vy` e `omega`.

## Fluxo do controle

```text
trajetória
> pose e velocidade desejadas
> erro contra a odometria
> controlador de pose
> vx, vy, omega
> cinemática mecanum
> comandos das quatro rodas
```

## Bibliotecas

Road Runner e Pedro Pathing podem acelerar o desenvolvimento. Escolha uma, siga a versão compatível com o FTC SDK instalado e documente todas as constantes. Não misture exemplos de versões diferentes.

Usar uma biblioteca não remove a necessidade de entender:

* `Pose2d`;
* referencial do campo e do robô;
* heading em graus ou radianos;
* velocidade e aceleração máximas;
* erro final;
* reset de pose;
* tolerância e timeout.

## Tuning por etapas

1. Calibre distância por volta da roda ou dead wheel.
2. Calibre rotação e track width efetivo.
3. Teste avanço e strafe separados.
4. Teste heading constante durante translação.
5. Faça uma curva simples.
6. Faça retorno à pose inicial.
7. Só então ligue mecanismos durante o caminho.

## Marcadores e ações

Dispare ações por posição ou progresso quando a biblioteca oferecer isso, mas preserve interlocks. Iniciar o shooter durante o caminho é válido. Alimentar a bola antes de alinhamento e RPM continua inválido.

```text
saída da coleta: ligar shooter
aproximação do HIVE: reduzir velocidade
alvo alcançado: trocar odometria global por alinhamento relativo
pronto: alimentar
```

## Restrições

Use aceleração menor perto de elementos e alvos. Um único limite global costuma ser conservador demais em reta e agressivo demais perto do HIVE.

## Recuperação

Se erro de pose passar de um limite ou houver colisão:

* pare o follower;
* reavalie a pose e o alvo;
* tente uma rota curta de recuperação;
* abandone o ciclo e estacione se o tempo restante for pequeno.

Autonomia não é seguir uma linha como se nada pudesse tocá-la. É saber qual caminho ainda existe depois que a partida empurra o robô para fora do plano.

