# TeleOp e controle do drivetrain

O controle do piloto precisa ser previsível. Ele pode ser rápido, suave e cheio de recursos, mas o mesmo movimento do joystick deve produzir a mesma intenção.

## Deadband e curva

```java
public static double applyDeadband(double value, double deadband) {
    if (Math.abs(value) <= deadband) return 0.0;
    return Math.copySign(
        (Math.abs(value) - deadband) / (1.0 - deadband),
        value
    );
}

public static double shape(double value) {
    return value * value * value;
}
```

A deadband remove ruído perto do centro. A curva cúbica preserva o alcance máximo e oferece precisão nos pequenos comandos.

## Mecanum robot-centric

```java
double y = -shape(applyDeadband(gamepad1.left_stick_y, 0.05));
double x =  shape(applyDeadband(gamepad1.left_stick_x, 0.05));
double rx = shape(applyDeadband(gamepad1.right_stick_x, 0.05));

double fl = y + x + rx;
double fr = y - x - rx;
double bl = y - x + rx;
double br = y + x - rx;

double max = Math.max(1.0,
    Math.max(Math.abs(fl), Math.max(Math.abs(fr),
    Math.max(Math.abs(bl), Math.abs(br)))));

frontLeft.setPower(fl / max);
frontRight.setPower(fr / max);
backLeft.setPower(bl / max);
backRight.setPower(br / max);
```

Se o strafe estiver errado, confira primeiro orientação e direção das rodas. Não tente esconder montagem incorreta dentro da equação.

## Field-centric

Transforme o vetor do campo para o referencial do robô:

```java
double heading = imu.getRobotYawPitchRollAngles()
    .getYaw(AngleUnit.RADIANS);

double rotX = x * Math.cos(-heading) - y * Math.sin(-heading);
double rotY = x * Math.sin(-heading) + y * Math.cos(-heading);
```

Use `rotX` e `rotY` na cinemática mecanum. Configure corretamente a orientação física do Control Hub e ofereça ao piloto um botão claro para zerar o heading.

## Slow mode

```java
double scale = gamepad1.right_bumper ? 0.35 : 1.0;
drive(rotX * scale, rotY * scale, rx * scale);
```

Teste se reduzir rotação e translação pela mesma escala é o melhor para o piloto. Perto do HIVE, uma rotação ainda menor pode ajudar.

## Heading hold

Quando o stick de rotação volta ao centro, guarde o último heading solicitado e use PID para mantê-lo. Assim o robô não perde mira enquanto faz strafe.

```java
if (Math.abs(rx) > 0.05) {
    targetHeading = heading;
    rotationCommand = rx;
} else {
    rotationCommand = headingPid.calculate(heading, targetHeading);
}
```

O erro angular precisa fazer wrap em `-pi` a `pi`. Sem isso, ir de 179° para -179° pode virar uma volta quase inteira.

## Botões por intenção

Mapeie controles para estados, não para peças:

```text
RT: coletar
LT: mirar no HIVE
A: disparar
Y: pontuar FLOWER
B: recolher tudo
RB: modo lento
```

O piloto deveria pensar na arena. A máquina cuida da própria sequência.

