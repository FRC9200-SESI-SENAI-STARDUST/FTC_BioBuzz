# Intake e magazine

O intake deve fazer o elemento querer entrar. Se o piloto precisa alinhar com precisão, reduzir velocidade e tentar de novo, o mecanismo transferiu sua dificuldade para a pessoa que dirige.

## Dois tamanhos, um caminho

POLLEN e NECTAR possuem diâmetros diferentes. Evite um canal rígido dimensionado apenas para o menor. Use flexibilidade controlada:

* compliant wheels;
* tubo de silicone;
* surgical tubing;
* polycord;
* roletes em braço tensionado;
* peças em TPU onde a deformação for previsível.

A compressão deve ser suficiente para dominar o objeto menor sem esmagar ou travar o maior. Prototipe com laterais transparentes. Ver o local exato em que a bola para vale mais que imaginar o problema por trás de uma chapa.

## Intake largo

Busque uma boca maior que o caminho interno. Guias laterais podem puxar o elemento para o centro, mas precisam evitar quinas onde duas bolas se prendem juntas. Teste aproximação central, lateral e em ângulo.

## Magazine de quatro elementos

O magazine precisa saber onde cada elemento está. Algumas opções:

| Conceito | Vantagem | Risco |
| --- | --- | --- |
| Canal linear | simples e leve | pressão entre bolas |
| Carrossel | posições definidas | mais peças e inércia |
| Indexador por correia | fluxo contínuo | exige sensores e tensão correta |

Não confie apenas no contador de software. A geometria física deve dificultar a entrada de um quinto elemento. O software é uma segunda proteção.

## Sensores

Uma distribuição útil é:

```text
entrada > sensor 1 > magazine > sensor 2 > feeder > sensor 3 > shooter
```

Beam break costuma produzir uma leitura clara. ToF ajuda quando não existe espaço para emissor e receptor, mas precisa ser testado com cor, ângulo e luz reais. Sensor de cor só deve decidir tipo de elemento depois de uma calibração séria.

## Anti-jam

O mecanismo deve conseguir reconhecer e tentar resolver uma obstrução. Um exemplo simples:

```text
motor comandado para frente
+ corrente alta
+ sensor não muda por 300 ms
= possível travamento
```

Resposta:

```text
parar > inverter por 150 ms > tentar novamente
```

Limite o número de tentativas. Um robô que insiste para sempre só transforma uma bola presa em motor queimado.

## Critério de pronto

Faça pelo menos 50 coletas misturando tamanhos e posições. A meta inicial é superar 95% sem intervenção manual e nunca controlar um quinto elemento.

