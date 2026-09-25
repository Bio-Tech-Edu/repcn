# Sprints — Raio-X Estratégico (repcn)

Este documento reorganiza o processo de desenvolvimento em sprints curtas e verificáveis, cada uma com escopo, entregáveis e critério de "pronto". Substitui o pedido original de "gerar tudo de uma vez" por um fluxo auditável, alinhado ao padrão de trabalho já usado em outros projetos da organização (clone limpo → análise de estado → entrega por sprint).

## Sprint 0 — Auditoria do código legado

**Objetivo:** entender por que o dashboard publicado (`bio-tech-edu.github.io/repcn`) renderizava o cabeçalho e o texto estático, mas nenhum gráfico, cartão de mapa de calor, quiz ou ícone aparecia.

**Causa raiz encontrada:** em `index.html`, dentro do `options.plugins.tooltip.callbacks.label` do gráfico `chartTRI`, havia um colchete extra fechando o array de rótulos:
```js
label:c=>[' Garantia absoluta...', ...][c.dataIndex]]   // <- colchete sobrando
```
Isso é um **erro de sintaxe**, não um erro de execução: o navegador falha ao interpretar o `<script>` inteiro, então nada dentro dele roda — nem os gráficos, nem o mapa de calor, nem o quiz, nem `lucide.createIcons()` (por isso os ícones da navegação também não apareciam nas capturas de tela). O HTML estático (cabeçalho, abas, textos fixos) continuava visível porque não depende do script.

**Verificação:** `node --check` no bloco de script confirmou `SyntaxError: Unexpected token ')'`.

**Achado secundário:** os dados de `mapa_calor.csv` (23 subtemas) e o array `HEAT` embutido no script estavam consistentes entre si — não havia problema de dados, só de sintaxe.

## Sprint 1 — Correção crítica e restauração funcional

- Corrigido o colchete extra; todos os módulos voltam a renderizar (gráficos, mapa de calor, quiz, cronômetro, distratores, protocolo, ícones, alternância clara/escura).
- Conteúdo pedagógico (enunciados, gabaritos, distratores, competências BNCC, protocolo do 2º dia) mantido fiel ao plano de aula e ao CSV — nenhum dado foi alterado, só a camada visual e a estrutura do código.

**Critério de pronto:** `node --check` sem erros no script principal; todos os `id` referenciados em JavaScript existem no HTML (checado por script).

## Sprint 2 — Sistema de design

O visual anterior seguia o padrão genérico de "kit de cards SaaS" (cantos muito arredondados, sombra suave uniforme, gradiente azul decorativo, rótulos em caixa alta). Foi substituído por uma identidade própria, construída a partir do conceito da aula — um "raio-x"/diagnóstico da prova:

- **Cor:** paleta neutra clara/escura (`--paper`/`--ink`), com cores fixas e funcionais por disciplina (Biologia, Química, Física) e por faixa de risco na TRI (fácil/médio/difícil) — as mesmas cores aparecem no gráfico, nos cartões da ETA e no quiz, reforçando a leitura dos dados em vez de decorar a interface.
- **Tipografia:** Space Grotesk para títulos, IBM Plex Sans para texto corrido, IBM Plex Mono para números, percentuais, códigos de competência (`C3-H8`) e o cronômetro — reforça a leitura de "painel de dados/leitura técnica".
- **Cabeçalho:** substituído o degradê azul genérico por um painel escuro com textura de grade sutil (referência a negatoscópio de raio-x) e uma faixa de indicadores em estilo "ficha técnica" (números em mono, divisórias finas) no lugar de caixas arredondadas com sombra.
- **Navegação por abas:** trocada de botões-pílula preenchidos para um indicador de sublinhado fino — mais parecido com um índice de caderno de prova do que com um menu de aplicativo genérico.
- **Cartões:** bordas finas em vez de sombra pesada uniforme; cor por disciplina usada com intenção (borda superior nas etapas da ETA, que é de fato uma sequência).

## Sprint 3 — Acessibilidade e interações

- Abas com `role="tablist"`, `role="tab"`, `aria-selected` e `role="tabpanel"` associados corretamente.
- Link "pular para o conteúdo" para navegação por teclado.
- `aria-label` descritivo nos dois gráficos (rosca e barras), já que Chart.js renderiza em `<canvas>`, opaco a leitores de tela.
- Modal de competências fechável por tecla Esc, com `role="dialog"` e `aria-modal`.
- Estados de foco visíveis (`:focus-visible`) em todos os botões, links e alternativas do quiz.
- `prefers-reduced-motion` respeitado (desativa a animação de entrada dos painéis).
- Modo escuro detectado por `prefers-color-scheme` na primeira visita, com alternância manual persistida.

## Sprint 4 — QA e documentação

- `checklist.html` realinhado à mesma paleta e tipografia, preservando 100% da otimização de impressão (`@media print`) que já funcionava bem.
- `README.md` atualizado com o novo sistema de design e a estrutura de sprints.
- Este arquivo (`SPRINTS.md`) criado como registro vivo do processo.

**Critério de pronto:** abrir `index.html` localmente em um navegador, testar as 4 abas, o filtro do mapa de calor, o quiz, o cronômetro e a alternância de tema; abrir `checklist.html` e testar `Ctrl/Cmd+P`.

---

## Backlog para próximas sprints

- [ ] Tabela de dados alternativa (`<table>` oculta visualmente) para os dois gráficos, garantindo acesso total via leitor de tela ao conteúdo dos canvases.
- [ ] Navegação das abas por teclado (setas esquerda/direita), hoje só por Tab/Enter.
- [ ] Testes manuais em pelo menos um leitor de tela (NVDA ou VoiceOver) antes da próxima aula.
- [ ] Avaliar mover os arrays de dados (`HEAT`, `QUIZ`, `DIST`, `PROT`) para `mapa_calor.csv`/JSON externos, reduzindo duplicação entre o CSV e o script.
- [ ] Métricas simples de uso (ex.: quantos alunos abriram o checklist) caso o material passe a ser usado por outras turmas/professores da rede.
