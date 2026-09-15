# AutoAim

AutoAim não é um botão que entrega precisão sozinho. Ele é um acordo entre localização, câmera, drivetrain, shooter e feeder. Se qualquer um ainda estiver se movendo fora da tolerância, o disparo deve esperar.

## Fluxo

```text
detectar cluster
> validar frame
> calcular erro lateral, yaw e distância
> comandar strafe e rotação
> consultar mapa de RPM e hood
> aguardar estabilidade
> liberar feeder
```

## Controle relativo

Pseudocódigo, pois os campos exatos do cluster devem seguir o SDK 12 instalado:

```java
TargetObservation target = vision.getBestHiveTarget();

if (target.isFresh()) {
    double strafe = lateralPid.calculate(target.lateralMeters(), 0.0);
    double rotation = yawPid.calculate(target.yawRadians(), 0.0);

    drive.commandRobotRelative(0.0, strafe, rotation);
    shooter.setTargetFromDistance(target.rangeMeters());
} else {
    drive.stopAutoAlignment();
}
```

Limite saída e aceleração. Uma correção agressiva perto do zero pode fazer o robô atravessar o alvo de novo, de novo, de novo, enquanto o piloto segura um botão e vê a mira nunca sossegar.

## Interpolação do shooter

```java
public static double lerp(double x, double x0, double y0,
                          double x1, double y1) {
    double t = (x - x0) / (x1 - x0);
    t = Math.max(0.0, Math.min(1.0, t));
    return y0 + t * (y1 - y0);
}
```

Encontre os dois pontos de distância que cercam a medição e interpole RPM e ângulo. Se a distância estiver fora do mapa validado, bloqueie o tiro automático ou use uma configuração segura conhecida.

## Gatilho de disparo

```java
boolean canShoot = vision.hasFreshTarget()
    && Math.abs(vision.getLateralErrorMeters()) < 0.025
    && Math.abs(vision.getYawErrorDegrees()) < 2.0
    && drive.isNearlyStopped()
    && shooter.isReady()
    && hood.isReady()
    && ballManager.hasBall();
```

Os valores são iniciais. A tolerância correta depende da abertura, distância, dispersão do shooter e latência.

## Perda de alvo

Ao perder a tag:

1. pare de atualizar o alvo com números inválidos;
2. mantenha por poucos milissegundos o último setpoint, se isso tiver sido testado;
3. bloqueie o feeder;
4. devolva controle de movimento ao piloto de forma previsível;
5. mostre `TARGET_LOST`.

## Ordem de desenvolvimento

Primeiro alinhe rotação. Depois lateral. Depois distância para o shooter. Por último, permita disparo automático. Cada camada precisa de teste próprio, porque juntar três PIDs mal ajustados cria um movimento difícil de explicar e ainda mais difícil de consertar.

