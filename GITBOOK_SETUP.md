# Configuração visual do GitBook

O GitBook atual não aceita CSS ou JavaScript personalizado dentro do site. A aparência precisa ser definida no painel de Customization depois que este repositório for conectado pelo Git Sync.

Use estas configurações para manter o visual preto, roxo e simples:

| Opção | Valor |
| --- | --- |
| Theme | Clean |
| Default mode | Dark |
| Light/dark toggle | Desativado |
| Primary color | `#8B5CF6` |
| Tint / background | `#09090B` |
| Header background | `#09090B` |
| Header links | `#F5F3FF` |
| Link color | `#A78BFA` |
| Corners | mínimo disponível |
| Shadows | desativadas ou mínimas |
| Font | padrão do sistema |
| Code theme | um tema escuro simples |

Não use gradiente, capa ilustrada, animação, cards em excesso ou muitos ícones. A navegação lateral, títulos, texto, tabela e código já são suficientes.

## Git Sync

1. Crie ou abra o Space no GitBook.
2. Conecte o repositório `FRC9200-SESI-SENAI-STARDUST/FTC_BioBuzz`.
3. Selecione a branch desejada.
4. Confirme que `.gitbook.yaml` aponta para `README.md` e `SUMMARY.md`.
5. Abra Customization e aplique a tabela acima.
6. Revise a versão publicada em desktop e celular.

O arquivo `.gitbook.yaml` controla a estrutura do conteúdo. Cores e modo escuro ficam no painel, conforme a documentação atual do GitBook.

Referência: [customização oficial de sites no GitBook](https://gitbook.com/docs/manage-your-site/customization).

