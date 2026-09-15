# Sensores e BallManager

Sensores transformam “acho que tem uma bola” em estado observável. Eles também piscam, atrasam, saem de posição e mentem quando a luz muda. Um sistema bom não confia cegamente nem ignora tudo. Ele procura confirmação.

## Debounce

Só aceite uma mudança depois que ela permanecer estável:

```java
public final class DebouncedBoolean {
    private final ElapsedTime timer = new ElapsedTime();
    private final double debounceSeconds;
    private boolean rawPrevious;
    private boolean value;

    public DebouncedBoolean(double debounceSeconds) {
        this.debounceSeconds = debounceSeconds;
    }

    public boolean update(boolean raw) {
        if (raw != rawPrevious) {
            rawPrevious = raw;
            timer.reset();
        }
        if (timer.seconds() >= debounceSeconds) value = raw;
        return value;
    }
}
```

Trinta milissegundos é um começo, não uma verdade. Meça o sensor real.

## Contagem por eventos

O contador deve mudar em bordas confirmadas, não enquanto o sensor continua ocupado.

```java
if (entryDetected && !previousEntryDetected) {
    ballCount = Math.min(4, ballCount + 1);
}

if (exitDetected && !previousExitDetected) {
    ballCount = Math.max(0, ballCount - 1);
}
```

Isso ainda precisa conhecer o sentido do mecanismo. Ao ejetar pela entrada, a mesma borda representa saída, não entrada.

## BallManager

```java
public final class BallManager {
    private int count;

    public boolean canIntake() {
        return count < 4;
    }

    public boolean hasBall() {
        return count > 0;
    }

    public void registerIntake() {
        count = Math.min(4, count + 1);
    }

    public void registerShot() {
        count = Math.max(0, count - 1);
    }

    public void resetToKnownState(int knownCount) {
        count = Math.max(0, Math.min(4, knownCount));
    }
}
```

O método de correção é importante. Se uma bola for retirada manualmente no pit ou um sensor falhar, a equipe precisa recuperar o estado sem reiniciar todo o código.

## Sensor plausível

Crie verificações:

* entrada e saída não podem indicar uma sequência fisicamente impossível;
* distância negativa ou além do alcance deve ser inválida;
* encoder não deve saltar milhares de ticks em um ciclo;
* corrente alta com velocidade zero sugere travamento;
* contador e sensores discordando por muito tempo exigem aviso.

Quando houver incerteza, pare o intake antes de aceitar um quinto elemento. A regra é mais importante que a vontade do software de continuar parecendo inteligente.

