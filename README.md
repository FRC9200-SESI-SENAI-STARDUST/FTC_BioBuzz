# FTC BIOBUZZ

Este guia existe para uma coisa simples: ajudar a equipe a transformar uma ideia de robô em um robô que entra na arena, repete ciclos e continua funcionando quando a partida deixa de ser bonita.

BIOBUZZ mistura coleta, armazenamento, lançamento, posicionamento e decisão. Parece muita coisa, e realmente é, mas o caminho não precisa nascer complicado. Primeiro fazemos o robô se mover. Depois fazemos ele coletar. Depois ele guarda, aponta e pontua. Só então começamos a juntar tudo. A máquina cresce por camadas, como se cada mecanismo ensinasse o próximo a existir.

Aqui você encontrará mecânica, programação, visão, controle, autonomia e testes. Há exemplos em Java para o FTC SDK, mas eles não foram escritos para serem copiados sem pensar. Use cada trecho como ponto de partida, adapte nomes, portas, sentidos e constantes ao robô real.

## Por onde começar

Se você acabou de entrar na equipe, siga esta ordem:

1. [Entenda o jogo e as prioridades](fundamentos/jogo-e-estrategia.md).
2. [Escolha uma arquitetura de robô](fundamentos/arquitetura-do-robo.md).
3. [Monte uma estrutura de programação](programacao/estrutura-do-projeto.md).
4. [Faça o drivetrain funcionar](mecanica/drivetrain.md).
5. [Adicione intake e magazine](mecanica/intake-e-magazine.md).
6. [Controle o shooter de verdade](mecanica/shooter.md).
7. [Construa o autônomo em camadas](autonomo/construindo-o-auto.md).
8. [Meça, teste e registre](testes/tuning-e-telemetria.md).

## A ideia central

O piloto escolhe o que quer fazer. O software decide como coordenar. A mecânica garante que o resultado possa acontecer de novo, de novo e de novo.

Isso muda a forma de projetar. O operador não deveria pensar em ligar um motor, mover um servo e esperar meio segundo. Ele deveria pedir `COLETAR`, `MIRAR`, `DISPARAR`, `PONTUAR_FLOWER` ou `RECOLHER`. O restante pertence ao robô.

## Antes de usar este guia

O manual oficial e os Team Updates sempre têm prioridade. BIOBUZZ está no começo de sua temporada e uma interpretação pode mudar. Quando uma regra afetar geometria, limite de elementos, eletrônica ou estratégia, confirme a versão mais recente antes de fabricar.
