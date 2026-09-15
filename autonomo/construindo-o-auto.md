# Construindo o AUTO

Trinta segundos parecem curtos até o robô parar no meio deles. O autônomo deve crescer por versões que já pontuam, não por uma rotina gigante que só passa a funcionar na última semana.

## AUTO 0

```text
iniciar em pose conhecida
> sair da área inicial
> estacionar
```

Esse auto valida inicialização, direção, pose e temporização.

## AUTO 1

```text
sair
> pontuar preloads no HIVE
> estacionar
```

Agora entram shooter, alinhamento e sequência de disparo.

## AUTO 2

```text
pontuar preloads
> coletar
> voltar ao HIVE
> pontuar novamente
> estacionar
```

Só avance quando a versão anterior superar a meta de confiabilidade.

## Máquina de estados

```java
enum AutoState {
    DRIVE_TO_HIVE,
    AIM,
    SHOOT_PRELOADS,
    DRIVE_TO_COLLECTION,
    COLLECT,
    RETURN_TO_HIVE,
    PARK,
    DONE,
    FAULT
}
```

Cada estado precisa de condição de sucesso, timeout e próximo estado. Não use uma sequência enorme de `sleep()`. Tempo pode proteger uma transição pequena, mas sensor e estado físico devem decidir quando possível.

```java
case AIM:
    if (superstructure.isReadyToShoot()) {
        transitionTo(AutoState.SHOOT_PRELOADS);
    } else if (stateTimer.seconds() > 2.0) {
        transitionTo(AutoState.PARK);
    }
    break;
```

Falhar no ciclo extra e ainda estacionar é melhor que esperar para sempre.

## Seleções antes da partida

Permita escolher:

* aliança;
* lado inicial;
* rotina;
* opção conservadora;
* atraso inicial, se a estratégia pedir.

Mostre todas as escolhas durante `init` e exija confirmação. Um auto excelente do lado errado continua sendo o auto errado.

## Teste de confiabilidade

Execute dez vezes seguidas sem editar código. Depois repita com bateria menos carregada e elementos posicionados dentro das tolerâncias permitidas. Conte sucesso completo, recuperação e falha.

O objetivo não é mostrar o melhor vídeo. É conhecer o pior resultado provável antes que ele apareça na partida.

