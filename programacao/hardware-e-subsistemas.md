# Hardware e subsistemas

O `hardwareMap` liga o nome do código ao dispositivo configurado no Robot Controller. Quando esses nomes não seguem um padrão, o primeiro erro da partida acontece antes mesmo do robô se mover.

## Padrão de nomes

Use nomes curtos e explícitos:

```text
drive_fl
drive_fr
drive_bl
drive_br
intake
indexer
shooter_left
shooter_right
flower_lift
hood
beam_entry
beam_exit
```

Mantenha a mesma lista na configuração do Hub, no código e na documentação elétrica.

## Subsistema de intake

```java
public final class Intake {
    public enum Mode { STOPPED, INTAKE, EJECT }

    private final DcMotorEx motor;
    private Mode mode = Mode.STOPPED;

    public Intake(HardwareMap hardwareMap) {
        motor = hardwareMap.get(DcMotorEx.class, "intake");
        motor.setZeroPowerBehavior(DcMotor.ZeroPowerBehavior.BRAKE);
    }

    public void setMode(Mode mode) {
        this.mode = mode;
    }

    public void periodic() {
        switch (mode) {
            case INTAKE: motor.setPower(0.85); break;
            case EJECT: motor.setPower(-0.45); break;
            default: motor.setPower(0.0);
        }
    }
}
```

O subsistema guarda o estado e escreve a saída em um ponto conhecido. Mais tarde, corrente, sensores e anti-jam podem entrar sem mudar todos os OpModes.

## Sentido e zero power

Defina a direção ao inicializar:

```java
leftMotor.setDirection(DcMotorSimple.Direction.REVERSE);
rightMotor.setDirection(DcMotorSimple.Direction.FORWARD);
```

Nunca conserte motor invertido colocando sinais negativos aleatórios em vários lugares.

Escolha `BRAKE` quando o mecanismo precisa resistir ao movimento e `FLOAT` quando deve girar livre. Teste temperatura e impacto mecânico. Segurar um braço pesado somente com `BRAKE` não substitui redução, mola ou feedforward.

## Encoders e unidades

Converta ticks para uma unidade física perto do subsistema:

```java
private static final double TICKS_PER_MOTOR_REV = 537.7;
private static final double GEAR_RATIO = 2.0;
private static final double SPOOL_DIAMETER_M = 0.030;

public double getHeightMeters() {
    double motorRevs = lift.getCurrentPosition() / TICKS_PER_MOTOR_REV;
    double spoolRevs = motorRevs / GEAR_RATIO;
    return spoolRevs * Math.PI * SPOOL_DIAMETER_M;
}
```

Não deixe ticks vazarem pelo código inteiro. Um target de `1840` não explica nada. Um target de `0.42 m` pode ser medido no robô.

## Falha segura

Todo subsistema precisa saber parar:

```java
public void stop() {
    motor.setPower(0.0);
    mode = Mode.STOPPED;
}
```

Se um sensor retornar valor impossível, escolha um estado seguro e mostre o erro na telemetria. Continuar agindo com confiança diante de uma leitura absurda é como seguir uma linha no chão depois que a linha acabou.

