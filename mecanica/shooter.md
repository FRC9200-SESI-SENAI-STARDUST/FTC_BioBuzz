# Shooter

O shooter não precisa produzir o lançamento mais bonito da arena. Ele precisa produzir o mesmo lançamento quando a bateria muda, quando uma bola chega um pouco deformada e quando o robô acabou de atravessar o campo.

## Arquiteturas iniciais

Comece comparando duas opções:

* flywheel único com hood;
* dois flywheels opostos.

O primeiro costuma ser mais simples e permite controlar o arco com o hood. O segundo pode reduzir o spin, mas usa mais espaço e exige sincronismo entre rodas.

Na versão inicial do campo, a abertura do CELL mede aproximadamente 20 por 14 polegadas e possui cerca de 12 polegadas de profundidade. Use o CAD oficial para projetar trajetória e margem. Abertura grande não elimina a necessidade de repetibilidade, porque o HIVE se move e o elemento precisa permanecer no CELL até a avaliação.

## Variáveis importantes

* diâmetro e massa do flywheel;
* compressão do elemento;
* material da roda;
* RPM;
* ângulo de saída;
* tempo de recuperação entre disparos;
* rigidez do hood;
* consistência do feeder.

Não altere todas ao mesmo tempo. Se o tiro mudou, você precisa saber qual decisão causou a mudança.

## Controle de velocidade

Não controle o shooter apenas com `setPower(0.75)`. Potência igual não significa velocidade igual quando a tensão da bateria cai. Use `DcMotorEx`, encoder e controle de velocidade.

```java
private static final double TICKS_PER_REV = 28.0;

public double rpmToTicksPerSecond(double rpm) {
    return rpm * TICKS_PER_REV / 60.0;
}

public void setTargetRpm(double rpm) {
    shooterMotor.setVelocity(rpmToTicksPerSecond(rpm));
}
```

Confirme `TICKS_PER_REV` para o encoder e a redução reais. Se existe uma correia 2:1 entre motor e flywheel, a rotação do motor não é a rotação da roda.

## Mapa de disparo

Construa a tabela com testes, nunca com valores inventados:

| Distância | RPM | Ângulo | Acertos em 20 |
| ---: | ---: | ---: | ---: |
| 1,0 m | a medir | a medir | a medir |
| 1,5 m | a medir | a medir | a medir |
| 2,0 m | a medir | a medir | a medir |

Depois interpole entre pontos próximos. Não extrapole longe demais, porque o comportamento do elemento não é perfeitamente linear.

## Condição de pronto

Velocidade dentro da tolerância não basta. Também verifique se ela parou de variar:

```java
boolean speedReady = Math.abs(targetRpm - actualRpm) < 80.0;
boolean accelerationReady = Math.abs(rpmDerivative) < 200.0;
boolean readyToFeed = speedReady && accelerationReady && stableTimer.seconds() > 0.15;
```

O feeder só deve agir quando shooter, hood, alinhamento e presença do elemento estiverem válidos.

## Protótipo

Faça uma bancada protegida, grave em câmera lenta e marque a saída do elemento. Teste vinte disparos por configuração. O primeiro tiro depois de alguns segundos parado merece uma coluna própria, porque ele frequentemente revela uma recuperação que a média esconde.
