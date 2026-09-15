# Cronograma de desenvolvimento

Este cronograma não tenta prever cada dia. Ele define uma ordem. Quando alguma etapa atrasa, a equipe sabe o que está sendo empurrado e pode escolher conscientemente, em vez de descobrir no fim que construiu durante semanas e pilotou durante dois dias.

## Semana 1: entender e provar conceitos

* ler manual e Team Updates;
* montar tabela de pontos e riscos;
* criar envelopes no CAD;
* deixar drivetrain operacional;
* prototipar intake com os dois tamanhos;
* prototipar shooter com proteção;
* definir arquitetura do código.

Entrega: drivetrain repetível e vídeos com dados dos protótipos.

## Semana 2: fluxo do elemento

* integrar intake;
* escolher magazine;
* medir velocidade do shooter;
* configurar IMU e field-centric;
* criar subsistemas;
* iniciar contador de elementos;
* começar treino de pilotagem.

Entrega: elemento entra, é detectado, armazenado e chega ao shooter.

## Semana 3: pontuação completa

* fechar shooter com PIDF;
* construir mapa inicial de tiro;
* integrar FLOWER;
* criar Superstructure e interlocks;
* iniciar odometria;
* validar manutenção e elétrica.

Entrega: robô pontua nos dois destinos em comando do operador.

## Semana 4: visão e autônomo básico

* calibrar câmera;
* detectar AprilTag Cluster;
* alinhar rotação e lateral;
* fazer AUTO 0 e AUTO 1;
* registrar telemetria e logs;
* iniciar teste de dez repetições.

Entrega: autônomo conservador acima de 90% de sucesso.

## Semana 5: ciclos

* medir cycle time;
* melhorar recuperação de travamento;
* fazer AUTO 2;
* testar bateria fraca;
* testar colisão e deslocamento de sensores;
* treinar piloto e operador juntos.

Entrega: partida simulada completa, com checklist e registro.

## Depois: escolher, não acumular

Possíveis avanços:

* interpolação do shooter;
* trajetórias mais agressivas;
* segundo ciclo no auto;
* recuperação automática;
* sensor fusion;
* disparo em movimento.

Escolha pelo ganho medido. Uma melhoria que economiza meio segundo em todos os ciclos pode valer mais que uma função impressionante usada uma vez.

## Ritmo semanal

Reserve treino de piloto desde cedo. Separe uma janela em que o robô não será desmontado, salvo falha crítica. Mecânica, programação e drive team precisam compartilhar uma lista única de prioridades e registrar qual versão está no robô.

