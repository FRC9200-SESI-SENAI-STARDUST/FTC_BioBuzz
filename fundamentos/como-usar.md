# Como usar este guia

Este material não é uma receita fechada. Um robô não nasce de uma sequência perfeita de páginas, ele nasce de tentativas que vão diminuindo o espaço do erro. A função do guia é encurtar esse caminho e dar nome ao que precisa ser observado.

## Para quem está começando

Leia uma página e teste uma ideia. Não tente aprender PID, odometria, AprilTag e trajetória na mesma tarde. Faça um motor responder, entenda o encoder, feche uma malha simples, registre o que aconteceu e só depois avance.

## Para quem já programa

Use as páginas como padrão de arquitetura e revisão. O objetivo não é provar que o código funciona uma vez. O objetivo é entender como ele falha, como se recupera e como alguém novo consegue mexer nele sem depender da pessoa que o escreveu.

## Para a mecânica

Cada mecanismo deve responder a quatro perguntas:

1. O que ele precisa fazer?
2. Qual variação do objeto ele precisa aceitar?
3. Como ele será regulado e mantido?
4. Como saberemos que ficou pronto?

Se trocar um motor exige desmontar metade do robô, o projeto ainda não terminou. Se uma posição depende de apertar um parafuso “mais ou menos aqui”, falta referência física. Se funciona parado, mas solta após uma colisão, falta estrutura.

## Como usar os exemplos

Os exemplos usam Java e os nomes mais comuns do FTC SDK. Eles mostram responsabilidades pequenas: ler um sensor, limitar um valor, calcular um erro. Um exemplo não conhece a redução real, a orientação do Hub, o diâmetro da roda ou o sentido dos motores da equipe.

Sempre confira:

* nomes do `hardwareMap`;
* direção dos motores;
* unidade usada em cada cálculo;
* limites mecânicos;
* comportamento quando um sensor falha;
* regra atual da temporada.

## Definição de pronto

“Funcionou” significa pouco. Um mecanismo está pronto quando repete o resultado, suporta uma bateria mais fraca, pode ser operado sob pressão e possui uma forma clara de recuperação. A arena não pergunta se a ideia era boa. Ela só mostra aquilo que o robô consegue repetir.

