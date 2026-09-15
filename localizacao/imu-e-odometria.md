# IMU e odometria

Localização é a memória de movimento do robô. Ela não enxerga a arena inteira. Ela soma pequenos deslocamentos e tenta não esquecer onde começou. Cada roda que escorrega deixa um rasgo nessa memória, pequeno no início e enorme depois de vários ciclos.

## IMU

Configure a orientação física do Control Hub:

```java
RevHubOrientationOnRobot orientation = new RevHubOrientationOnRobot(
    RevHubOrientationOnRobot.LogoFacingDirection.UP,
    RevHubOrientationOnRobot.UsbFacingDirection.FORWARD
);

IMU.Parameters parameters = new IMU.Parameters(orientation);
imu.initialize(parameters);
```

Troque as direções pelo robô real. Um Hub montado de lado com configuração deitado produz heading coerente apenas por acidente.

Leia yaw na unidade escolhida:

```java
double headingRad = imu.getRobotYawPitchRollAngles()
    .getYaw(AngleUnit.RADIANS);
```

Padronize radianos dentro dos cálculos e converta para graus apenas na interface.

## Três níveis de localização

### Encoder do drivetrain e IMU

É o começo. Funciona para deslocamentos simples, mas mecanum escorrega justamente para criar movimento lateral. Colisão e aceleração alteram a relação entre rotação da roda e movimento no chão.

### Dead wheels e IMU

Duas rodas paralelas e uma perpendicular medem deslocamento sem participar da tração. Ainda existe deslizamento, folga e erro de geometria, mas a leitura costuma ser muito mais estável.

### Módulo dedicado

Um módulo como goBILDA Pinpoint concentra leitura e cálculo. Ele reduz trabalho de integração, não elimina calibração. Offsets, direção dos encoders e escala continuam pertencendo ao robô.

## Pose

```java
public record Pose2d(double xMeters, double yMeters, double headingRad) {}
```

A cada ciclo:

```text
ler deslocamentos locais
> remover parte causada pela rotação
> transformar para o campo usando heading
> somar à pose anterior
```

## Calibração

Meça em testes separados:

1. andar 1, 2 e 4 metros em linha reta;
2. strafe para os dois lados;
3. girar 90°, 180° e várias voltas;
4. fazer arco combinando translação e rotação;
5. repetir com aceleração baixa e alta.

Calibre escala linear antes do offset rotacional. Se mudar diâmetro efetivo da roda, pressão ou posição do pod, repita.

## Reset e referência

Defina quando a pose pode ser zerada. No início do autônomo, use uma pose conhecida no campo. Durante TeleOp, zerar apenas o heading pode ajudar o field-centric, mas não deve apagar silenciosamente `x` e `y`.

Os AprilTags do HIVE se movem com o HIVE. Eles servem para alinhamento relativo, não como verdade absoluta da pose de campo. O alvo pode dizer “você está 12 cm à esquerda de mim”, mas não pode garantir onde os dois estão na arena.

