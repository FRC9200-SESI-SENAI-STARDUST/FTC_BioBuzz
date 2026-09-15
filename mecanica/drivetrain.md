# Drivetrain

O drivetrain é o chão sobre o qual todo o resto tenta existir. Um shooter excelente montado em uma base que escorrega, desalinha ou quebra transforma precisão em sorte.

## Por que mecanum

BIOBUZZ possui tráfego, HIVE central, zonas de coleta e alvos que pedem alinhamento lateral. O mecanum permite corrigir posição sem girar o robô inteiro, o que ajuda tanto o piloto quanto o AutoAim.

Ele também cobra seu preço:

* perde tração com facilidade;
* depende de distribuição de peso equilibrada;
* precisa de rodas na orientação correta;
* sofre mais com folgas e estrutura torta;
* não deve ser a única fonte de odometria em um robô avançado.

## Montagem

Vendo o robô por cima, os roletes devem formar um `X`. Confira o desenho do fabricante, porque uma roda invertida ainda gira e isso costuma esconder o erro durante alguns minutos.

Use uma estrutura rígida e confira as diagonais. Se o chassi parece retangular, mas as diagonais são diferentes, as rodas não dividem carga igualmente. Aperte e marque parafusos, use trava química quando apropriado e deixe as rodas removíveis sem desmontar os mecanismos superiores.

## Relação e velocidade

Não escolha a redução só pela velocidade livre. A velocidade útil depende de aceleração, massa e espaço de frenagem. Um robô rápido que passa do ponto e precisa voltar perde o mesmo tempo que tentou ganhar.

Calcule uma estimativa:

```text
velocidade linear = RPM_motor / redução * circunferência_da_roda / 60
```

Depois meça no chão. A diferença entre cálculo e realidade mostra perdas, escorregamento e limitação por bateria.

## Teste mínimo

Antes de adicionar outros mecanismos, o drivetrain deve:

1. andar para frente sem corrigir com o joystick;
2. fazer strafe para os dois lados;
3. girar sem puxar para uma direção;
4. parar sem soltar cabo ou deslocar componente;
5. repetir um quadrado dez vezes;
6. manter temperatura e corrente aceitáveis.

Registre tensão da bateria, tempo e erro final. Um teste sem registro vira apenas uma lembrança de que “parecia bom”.

## Onde sensores devem entrar

Encoders dos motores são suficientes para controle inicial das rodas. A IMU fornece heading. Para localização consistente, prefira dead wheels ou um módulo dedicado, porque a roda mecanum foi criada para deslizar lateralmente e depois pedimos que ela conte exatamente quanto deslizou. Existe uma contradição mecânica aí, e o software não consegue apagar completamente essa sombra.

