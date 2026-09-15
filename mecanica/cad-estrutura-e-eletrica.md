# CAD, estrutura e elétrica

Um robô de competição precisa ser montado, inspecionado, consertado e novamente colocado em campo. O desenho não termina quando as peças cabem. Ele termina quando alguém cansado consegue trocar uma delas sem criar três problemas novos.

## Regras de CAD

1. Modele envelopes inicial e expandido.
2. Modele o caminho dos elementos com tolerância.
3. Inclua cabeça de parafuso, espaçador, conector e cabo.
4. Deixe ajuste para correias e correntes.
5. Use referências físicas para posições repetíveis.
6. Evite parafuso inacessível atrás de chapa fechada.
7. Exporte desenho de fabricação com revisão identificada.

## Rigidez e impacto

Contato entre robôs faz parte da FTC. Chapas finas precisam de dobra, espaçador ou travamento. Eixos longos precisam de apoio. Mecanismos altos precisam recolher para dentro de uma estrutura protegida.

Procure folga em cadeia:

```text
rolamento > eixo > polia > correia > braço > hood
```

Um pouco em cada junta pode virar vários graus na saída do shooter.

## Elétrica organizada

O caminho básico é bateria, chave principal, Control Hub e, se necessário, um Expansion Hub. Monte pensando na inspeção:

* chave principal visível e alcançável;
* LEDs dos Hubs visíveis;
* USB protegido contra impacto e tração;
* cabos identificados nas duas pontas;
* conectores presos, sem fio sustentando peso;
* fusíveis acessíveis;
* folga controlada em partes móveis;
* bateria contida em todas as orientações.

Se houver Expansion Hub, verifique na documentação oficial a possibilidade de redundância RS485 e a escolha dos ports de encoder de alta contagem. Não trate uma dica elétrica antiga como regra eterna.

## Revisão antes de ligar

```text
bateria correta e carregada
polaridade conferida
chave desligada durante conexão
nenhum fio descascado
nenhum cabo perto de corrente ou engrenagem
rodas suspensas no primeiro teste
botão de parada acessível
```

## Manutenção entre partidas

Crie uma volta fixa pelo robô. Comece na bateria e siga sempre o mesmo sentido, conferindo conectores, parafusos marcados, tensão de correias, rodas, sensores e peças impressas. A rotina precisa ser simples porque, no pit, a pressa tenta convencer todo mundo de que “depois a gente olha”.

