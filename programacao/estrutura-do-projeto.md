# Estrutura do projeto

Colocar o robô inteiro dentro de um `LinearOpMode` funciona até o momento em que intake, shooter, câmera e piloto precisam agir juntos. A partir daí, cada correção puxa outra, o arquivo cresce e ninguém sabe exatamente qual parte é dona de qual motor.

## Organização sugerida

```text
TeamCode/
└── src/main/java/.../teamcode/
    ├── opmodes/
    │   ├── MainTeleOp.java
    │   └── AutoBlue.java
    ├── subsystems/
    │   ├── Drive.java
    │   ├── Intake.java
    │   ├── Shooter.java
    │   ├── Flower.java
    │   └── Vision.java
    ├── superstructure/
    │   ├── RobotState.java
    │   └── Superstructure.java
    ├── control/
    │   ├── SimplePid.java
    │   └── Feedforward.java
    ├── constants/
    │   └── RobotConstants.java
    └── util/
        ├── MathUtil.java
        └── Debouncer.java
```

O nome das pastas importa menos que a fronteira entre responsabilidades.

## Responsabilidade de cada camada

| Camada | Decide |
| --- | --- |
| OpMode | lê o piloto e escolhe objetivos |
| Superstructure | coordena estados do robô |
| Subsistema | controla um mecanismo |
| Control | executa matemática reutilizável |
| Constants | guarda números ajustáveis |
| Util | resolve problemas pequenos e genéricos |

O `MainTeleOp` não deve descobrir como o shooter chega à RPM. Ele pede uma RPM. A `Superstructure` não deve escrever diretamente em uma porta de motor. Ela pede ao subsistema um estado.

## Loop principal

```java
@TeleOp(name = "Main TeleOp")
public final class MainTeleOp extends OpMode {
    private Robot robot;

    @Override
    public void init() {
        robot = new Robot(hardwareMap, telemetry);
    }

    @Override
    public void loop() {
        robot.readSensors();
        robot.handleDriverInput(gamepad1, gamepad2);
        robot.update();
        robot.writeTelemetry();
    }
}
```

Separar leitura, decisão e saída deixa o ciclo compreensível. Evite espalhar `hardwareMap.get()` por vários arquivos. A configuração acontece uma vez, e cada subsistema recebe apenas o hardware que controla.

## Constantes

```java
public final class RobotConstants {
    private RobotConstants() {}

    public static final class Shooter {
        public static final double RPM_TOLERANCE = 80.0;
        public static final double STABLE_TIME_S = 0.15;
    }

    public static final class Drive {
        public static final double SLOW_SCALE = 0.35;
        public static final double STICK_DEADBAND = 0.05;
    }
}
```

Uma constante deve possuir nome, unidade e motivo. `0.37` escondido no meio do loop é só um número. `SLOW_SCALE` mostra o que o número faz.

## Versão mínima primeiro

Comece com interfaces pequenas. Não crie uma arquitetura tão abstrata que seja impossível ligar um motor. A estrutura deve diminuir o peso do projeto, não virar outro mecanismo para carregar.

