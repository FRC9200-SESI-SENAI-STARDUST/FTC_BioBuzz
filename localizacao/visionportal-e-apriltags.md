# VisionPortal e AprilTags

Visão deve responder a uma pergunta concreta. “Existe um alvo?” “Qual é o erro lateral?” “A que distância aproximada estamos?” Quando uma câmera tenta resolver tudo ao mesmo tempo, ela costuma entregar muitos números e pouca confiança.

## Começo recomendado

Use uma webcam frontal, `VisionPortal` e o processador oficial de AprilTags. Só adicione processamento de cor ou segunda câmera depois de medir CPU, FPS, latência e necessidade real.

```java
AprilTagProcessor aprilTag = new AprilTagProcessor.Builder()
    .build();

VisionPortal portal = new VisionPortal.Builder()
    .setCamera(hardwareMap.get(WebcamName.class, "Webcam 1"))
    .addProcessor(aprilTag)
    .build();
```

Consulte os Samples da versão exata do SDK instalada. BIOBUZZ usa SDK 12 e adiciona suporte a AprilTag Clusters. Não misture exemplo antigo de detecção individual com a API de cluster sem revisar tipos e metadados.

## Dados úteis

Para alinhamento relativo ao CELL, procure:

* erro lateral;
* distância;
* yaw do alvo;
* quantidade e qualidade das detecções;
* idade do frame;
* pose da câmera em relação ao robô.

Um frame antigo pode possuir números perfeitos para uma posição que já passou. Registre timestamp e descarte medições atrasadas além do limite definido.

## Câmera no robô

Monte em uma peça rígida. Meça posição e rotação em relação ao centro do robô. Proteja o conector USB e evite que o hood entre no campo de visão.

Se a câmera mexer dois graus após uma colisão, toda a matemática continuará rodando e entregará uma resposta errada com aparência de precisão.

## Calibração

Pose por tag depende dos intrínsecos da câmera e da resolução:

```text
fx, fy
cx, cy
coeficientes de distorção
```

Use calibração correspondente ao modelo e à resolução. Quando possível, trave exposição, ganho e foco depois de testar sob iluminação semelhante à arena.

## Filtro de alvo

Não escolha cegamente a primeira detecção da lista. Valide:

```java
boolean usable = detection.metadata != null
    && detection.ftcPose != null
    && detection.decisionMargin > MIN_DECISION_MARGIN;
```

O campo exato disponível varia com a versão da API. O princípio permanece: tag conhecida, qualidade suficiente, pose presente e frame recente.

## HIVE não é landmark fixo

O cluster do HIVE acompanha um elemento móvel do campo. Use-o assim:

```text
cluster > pose relativa > alinhamento fino > disparo
```

Não use assim:

```text
cluster > reset global de x, y e heading
```

Odometria e IMU navegam. A câmera corrige o último trecho até o alvo.

