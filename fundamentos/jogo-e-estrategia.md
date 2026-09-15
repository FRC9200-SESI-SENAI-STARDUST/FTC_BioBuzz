# Jogo e estratégia

Antes do CAD e antes do primeiro `motor.setPower`, existe uma pergunta que costuma ser ignorada: qual trabalho realmente vence a partida?

BIOBUZZ é um jogo de ciclos. O robô coleta, armazena, atravessa o campo, alinha e pontua. Cada segundo perdido aparece em algum ponto dessa linha. Às vezes a equipe procura uma solução avançada para o lançamento, mas perde mais tempo mirando o intake. Às vezes o autônomo é ambicioso, mas o magazine trava uma bola a cada três ciclos. O jogo inteiro é uma máquina, e a engrenagem mais fraca sempre acaba aparecendo.

## Estrutura da partida

| Período | Duração |
| --- | ---: |
| Autônomo | 30 s |
| Transição | 8 s |
| Controle por pilotos | 120 s |

O robô começa com quatro POLLEN e não pode controlar mais de quatro elementos ao mesmo tempo. Isso já cria uma decisão de projeto: o armazenamento deve ter quatro posições conhecidas e o software precisa impedir uma quinta entrada.

| Elemento | Diâmetro aproximado |
| --- | ---: |
| POLLEN | 71 mm |
| NECTAR | 91 mm |

Vinte milímetros parecem pouco no papel, mas são suficientes para transformar um canal rígido em uma fonte constante de travamentos. Intake, indexador e shooter precisam aceitar a variação sem depender de uma regulagem delicada.

## Prioridade competitiva

O HIVE deve orientar a arquitetura principal. FLOWER é uma segunda capacidade importante, mas não deve destruir a confiabilidade do ciclo principal. A ordem inicial recomendada é:

1. sair e estacionar de forma confiável;
2. pontuar os elementos iniciais;
3. repetir um ciclo de coleta e HIVE;
4. pontuar no FLOWER com alta taxa de sucesso;
5. reduzir tempo de alinhamento;
6. aumentar a agressividade do autônomo.

Uma rotina simples com mais de 90% de sucesso vale mais que uma rotina enorme que só funciona quando tudo está perfeito.

## Como analisar uma estratégia

Para cada ação, meça:

| Pergunta | Exemplo de medida |
| --- | --- |
| Quanto vale? | pontos e possível RP |
| Quanto demora? | tempo médio e pior caso |
| Quanto falha? | sucessos em 20 tentativas |
| Como recupera? | tempo para destravar ou reposicionar |
| O que impede? | espaço, tráfego, bateria, visão |

O ciclo deve ser cronometrado por partes: coleta, deslocamento, mira, disparo e retorno. Sem isso, a equipe discute sensação. Com isso, a equipe escolhe onde trabalhar.

## Regras que precisam ficar abertas durante o projeto

Mantenha atenção especial a:

* limite de quatro elementos controlados;
* envelope inicial e expansão;
* interação permitida com FLOWER e HIVE;
* dispositivos de controle e visão permitidos;
* acessibilidade da elétrica para inspeção;
* alterações publicadas em Team Updates e Q&A.

Não desenhe uma peça importante a partir de uma lembrança do manual. Abra a regra, leia o contexto e registre a versão usada na decisão.

