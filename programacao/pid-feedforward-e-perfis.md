# PID, feedforward e perfis

PID não é um número mágico que faz o mecanismo obedecer. É uma forma de olhar para o erro no presente, lembrar o que ele acumulou e observar a velocidade com que está mudando.

## As três partes

```text
erro = alvo - medição
saída = kP * erro + kI * integral + kD * derivada
```

* `P` reage ao erro atual.
* `I` acumula erro persistente.
* `D` reage à mudança do erro.

## Controlador simples

```java
public final class SimplePid {
    private final double kP, kI, kD;
    private double integral;
    private double previousError;

    public SimplePid(double kP, double kI, double kD) {
        this.kP = kP;
        this.kI = kI;
        this.kD = kD;
    }

    public double calculate(double measurement, double target, double dt) {
        double error = target - measurement;
        integral += error * dt;
        double derivative = (error - previousError) / dt;
        previousError = error;
        return kP * error + kI * integral + kD * derivative;
    }

    public void reset() {
        integral = 0.0;
        previousError = 0.0;
    }
}
```

Em produção, limite integral, proteja `dt` e trate erro angular. Bibliotecas maduras já resolvem boa parte disso, mas entender o cálculo evita ajustar constantes no escuro.

## Procedimento de tuning

1. Defina `I = 0` e `D = 0`.
2. Aumente `P` até a resposta ficar rápida e próxima da oscilação.
3. Recue `P`.
4. Adicione pouco `D` se houver overshoot.
5. Use `I` apenas para um erro estático que outras soluções não removeram.
6. Repita com bateria forte e fraca.

Mude uma constante por vez e registre gráfico de alvo, medição e saída.

## Feedforward

PID corrige aquilo que aconteceu. Feedforward estima o esforço antes do erro aparecer.

Para velocidade:

```text
saída = kS * sinal(v) + kV * v + kA * a
```

Para um braço:

```text
saída = kS * sinal(v) + kG * cos(ângulo) + kV * v + kA * a
```

O `kG` compensa gravidade. Sem ele, o PID passa boa parte do tempo carregando o peso que já sabíamos que existia.

## Perfil trapezoidal

Não peça para um mecanismo pesado saltar de 0 para 2500 ticks. Gere alvos intermediários de posição e velocidade respeitando aceleração máxima.

```text
acelerar > velocidade constante > desacelerar
```

Isso reduz pico de corrente, overshoot e impacto. É especialmente útil em elevador, braço, heading e trajetórias.

## Condição de término

```java
boolean atTarget = Math.abs(positionError) < 0.01;
boolean nearlyStopped = Math.abs(velocity) < 0.03;
boolean settled = atTarget && nearlyStopped && stableFor(0.15);
```

Nunca compare medição de sensor com igualdade exata. O mundo real vibra. O software precisa saber quanto erro ainda é aceitável.

