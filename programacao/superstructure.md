# Superstructure e segurança

A Superstructure é onde os mecanismos deixam de ser peças separadas e passam a agir como um robô. Ela recebe uma intenção e coordena intake, magazine, shooter, hood e FLOWER.

## Estados

```java
public enum RobotState {
    IDLE,
    INTAKING,
    AIMING_HIVE,
    SHOOTING,
    FLOWER_PREP,
    FLOWER_SCORE,
    STOW,
    FAULT
}
```

## Coordenação

```java
public void periodic() {
    switch (state) {
        case INTAKING:
            shooter.stop();
            flower.stow();
            intake.setEnabled(ballManager.canIntake());
            break;

        case AIMING_HIVE:
            intake.stop();
            shooter.setTargetFromDistance(vision.getRangeMeters());
            drive.alignToHive(vision.getTarget());
            break;

        case SHOOTING:
            if (canFeed()) indexer.feedOne();
            break;

        case FAULT:
            stopAll();
            break;

        default:
            holdSafeState();
    }
}
```

## Interlocks

Um interlock impede uma ação válida no momento errado:

```java
private boolean canFeed() {
    return shooter.isReady()
        && hood.isReady()
        && vision.isAligned()
        && ballManager.hasBall()
        && !flower.isInTheWay();
}
```

Outros exemplos:

* não subir FLOWER se o shooter ocupa o mesmo volume;
* não recolher braço enquanto o bucket está aberto;
* não ligar intake com quatro elementos;
* não disparar sem alinhamento, exceto em modo manual consciente;
* não continuar perfil se o limit switch esperado nunca chegar.

## Timeout

Nenhuma etapa deve esperar para sempre:

```java
if (!flower.atTarget() && stateTimer.seconds() > 1.5) {
    fault = "FLOWER_TIMEOUT";
    state = RobotState.FAULT;
}
```

Timeout não corrige falha. Ele impede que a falha ocupe o resto da partida.

## Modo manual

Tenha recuperação manual limitada para o pit e para situações inesperadas. Ela precisa exigir uma combinação intencional de botões e respeitar limites físicos críticos. “Manual” não pode significar “sem segurança”.

## Estado visível

Mostre na telemetria:

```text
requested_state
active_state
transition_time
interlock_blocking
fault_code
```

Quando o robô se recusa a disparar, o operador precisa saber se faltou RPM, alinhamento, hood ou elemento. Sem isso, toda trava parece o mesmo silêncio.

