# Como contribuir

Esta documentação deve mudar junto do robô. Quando uma relação de transmissão muda, quando um sensor troca de porta ou quando a equipe descobre que uma hipótese estava errada, o guia precisa acompanhar.

## Antes de editar

* confirme a regra na fonte oficial;
* teste código no hardware correspondente;
* use unidade em nomes e tabelas;
* separe valor medido de valor sugerido;
* não publique credencial, chave ou dado pessoal.

## Commits

Prefira commits pequenos e reconhecíveis:

```text
docs: corrige orientação física da IMU
docs: adiciona teste de recuperação do intake
docs: atualiza mapa medido do shooter
```

Não misture uma correção de regra com vinte mudanças de estilo. O histórico precisa explicar a evolução, não apenas provar que arquivos mudaram.

## Revisão técnica

Toda mudança importante deve responder:

1. Foi testada?
2. Em qual versão do SDK ou manual?
3. Qual risco resolve?
4. Qual comportamento apresenta quando falha?
5. Outra pessoa da equipe consegue reproduzir?

## Escrita

Use português correto, direto e humano. Explique o motivo antes de empilhar termos. Metáforas podem ajudar quando iluminam uma ideia, mas não devem esconder número, unidade ou condição.

Evite afirmar que uma solução é obrigatória quando ela é apenas recomendada. Em engenharia, contexto muda. O texto deve ter convicção suficiente para orientar e honestidade suficiente para mostrar onde ainda existe dúvida.

