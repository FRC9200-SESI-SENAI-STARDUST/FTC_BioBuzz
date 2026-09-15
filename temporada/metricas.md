# Métricas e critérios de pronto

Uma meta transforma “melhorar o intake” em uma pergunta que pode ser respondida. Ela não precisa nascer perfeita. Precisa nascer mensurável.

## Metas iniciais

| Métrica | Meta inicial |
| --- | ---: |
| Coleta sem intervenção | maior que 95% |
| Acerto parado no HIVE | maior que 90% |
| Pontuação no FLOWER | maior que 95% |
| Sucesso do auto conservador | maior que 90% |
| Aquisição do cluster na zona prevista | maior que 95% |
| Elementos controlados | nunca acima de 4 |
| Recuperação de mecanismo | sem reiniciar o robô |
| Inicialização completa | menor que 30 s |

Esses valores devem ser revistos quando a equipe conhecer o robô e o nível da competição.

## Cycle time

Meça por etapas:

```text
coleta
+ deslocamento até o alvo
+ alinhamento
+ disparos
+ retorno
= cycle time
```

Registre média, melhor, pior e desvio. O melhor ciclo mostra potencial. O pior mostra o que a partida provavelmente encontrará quando houver tráfego.

## Taxa de acerto

Não misture condições:

| Cenário | Tentativas |
| --- | ---: |
| Parado e alinhado | 20 |
| Após aceleração | 20 |
| Bateria forte | 20 |
| Bateria fraca | 20 |
| Elementos misturados | 20 |

## Critério por mecanismo

Um mecanismo está pronto quando:

* cumpre a função dentro da meta;
* não invade envelope;
* possui proteção e batente;
* pode ser mantido rapidamente;
* informa falha;
* possui recuperação;
* foi testado com variação real;
* tem documentação e responsável.

## Pirâmide de prioridade

```text
AutoAim e trajetórias avançadas
Visão e alinhamento relativo
Odometria e controle fechado
Superstructure e sensores
Shooter e FLOWER repetíveis
Intake, magazine e drivetrain
Confiabilidade e treino de piloto
```

A base não é a parte menos importante. É a parte que segura todo o peso. Quando intake, shooter e piloto repetem bem, a visão passa a multiplicar algo que já existe. Antes disso, ela só esconde por alguns minutos o problema que continua embaixo.

