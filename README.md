# Fortes AC Integrador — Sistema Financeiro Offline

Sistema financeiro completo 100% offline em um único arquivo HTML, desenvolvido para integração com o **Fortes Contábil**. Sem instalação, sem servidor, sem dependências externas — basta abrir no navegador.

---

## Acesso rápido

Após ativar o GitHub Pages, o sistema estará disponível em:

```
https://<seu-usuario>.github.io/<nome-do-repositorio>/FortesAC_Financeiro.html
```

Os dados são armazenados no **localStorage** do próprio navegador — nada é enviado para servidores.

---

## Funcionalidades

### Financeiro
- **Contabilizações** — lançamentos de entradas e saídas com histórico completo de edições
- **Contas a Pagar e a Receber** — cadastro de títulos com parcelamento (até 24x), condição de pagamento, forma de pagamento por parcela e percentual
- **Baixa de títulos** — modal completo com data, banco, valor pago e geração automática da contabilização
- **Lançamentos Recorrentes** — semanal, quinzenal, mensal e anual, com prévia e confirmação antes de criar

### Plano de Contas
- Estrutura em dois níveis: **grupos sintéticos** (não lançáveis) e **contas analíticas** (lançáveis)
- 8 grupos de saída: Administrativas, Colaboradores, Imóvel, Veículos, Diretoria, Impostos, Fornecedores, Financeiro
- 4 grupos de entrada: Receitas Operacionais, Receitas Financeiras, Outras Receitas, Transferências
- **Cód. Fortes** por operação — código de integração para exportação CSV ao Fortes Contábil
- Importação do plano sugerido em um clique

### Exportação para o Fortes Contábil
- Exporta CSV no formato `ide;data;d;c;vl;hist`
- **Validação bloqueante**: exportação é impedida se qualquer operação não tiver o Cód. Fortes preenchido, com listagem detalhada das contas não mapeadas
- Bancos usam o código cadastrado diretamente (já é o código Fortes)

### Conciliação Bancária
- Importa extrato **OFX** (padrão bancos brasileiros), CSV e XLSX
- Digitação manual de itens
- Sugestão automática por valor + data de vencimento + similaridade de texto
- Vinculação manual: clique no item do extrato → clique no título
- **Itens sem correspondência**: abre modal de classificação completo (tipo, operação, banco, valor, descrição) — cria o título já baixado e gera a contabilização em um passo
- "Confirmar e dar baixa": processa todos os pares de uma vez — baixa os títulos e gera contabilizações
- Exporta resultado em XLSX

### Relatórios
- **DRE** — agrupado por grupos sintéticos do plano de contas, com subtotais por grupo, margem e resultado
- **Fluxo de Caixa Projetado** — período livre com atalhos (hoje, 1 semana, 15 dias, 1 mês até 1 ano), filtro por banco, gráfico de linha com pontos negativos destacados, tabela de movimentações

### Cadastros
- Bancos (código = código Fortes)
- Plano de contas (grupos + analíticas com Cód. Fortes)
- Usuários com perfis: Admin, Operador, Visualizador

### Outros
- **Dashboard** com KPIs, gráfico de 7 dias, saldo por banco e top operações
- **Travamento de período** — admin bloqueia meses para edição
- **Backup e Restore** — exporta e importa JSON completo (v3.1)
- **Log de auditoria** completo com exportação CSV
- **Tema escuro/claro** — alternado com `Ctrl+\`
- **Busca global** — `Ctrl+K` busca em lançamentos, operações, bancos e contas
- **Atalhos de teclado** — `?` exibe cheatsheet completo

---

## Como usar

### Opção 1 — GitHub Pages (recomendado)
1. Faça upload do `FortesAC_Financeiro.html` neste repositório
2. Acesse **Settings → Pages → Source: main → / (root) → Save**
3. Aguarde ~1 minuto e acesse a URL gerada

### Opção 2 — Local
1. Baixe o arquivo `FortesAC_Financeiro.html`
2. Abra no **Google Chrome** ou **Microsoft Edge**
3. O sistema abre direto — sem instalação

> **Nota:** Abrir via `file://` (direto do disco) funciona no Chrome e Edge. Firefox pode bloquear algumas APIs. Para melhor experiência, use o GitHub Pages.

---

## Estrutura de dados (localStorage)

| Chave | Conteúdo |
|---|---|
| `fac3_users` | Usuários e perfis |
| `fac3_grupos` | Grupos sintéticos do plano de contas |
| `fac3_ops` | Operações analíticas com Cód. Fortes |
| `fac3_banks` | Bancos com código Fortes |
| `fac3_lancs` | Contabilizações (lançamentos) |
| `fac3_contas` | Títulos a pagar e a receber |
| `fac3_recorr` | Lançamentos recorrentes |
| `fac3_audit` | Log de auditoria |
| `fac3_periods` | Períodos travados |
| `fac3_settings` | Preferências (tema, timeout) |

---

## Formato de exportação CSV (Fortes Contábil)

```
ide;data;d;c;vl;hist
1;22/03/2026;111;361;1.250,00;Energia Elétrica março
```

| Campo | Descrição |
|---|---|
| `ide` | Sequencial |
| `data` | DD/MM/AAAA |
| `d` | Débito — Cód. Fortes da operação (Saída) ou código do banco (Entrada) |
| `c` | Crédito — código do banco (Saída) ou Cód. Fortes da operação (Entrada) |
| `vl` | Valor em formato `1.250,00` |
| `hist` | Histórico do lançamento |

---

## Requisitos

- Navegador moderno com suporte a ES2020+ (Chrome 88+, Edge 88+, Firefox 85+)
- JavaScript habilitado
- localStorage disponível (~5MB por domínio — suficiente para milhares de lançamentos)

---

## Versão

**v3.1** — Março 2026

Desenvolvido com Claude (Anthropic) — sistema 100% gerado por IA, sem frameworks externos, dependências CDN apenas para Chart.js, SheetJS e Font Awesome.
