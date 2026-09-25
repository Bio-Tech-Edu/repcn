# Raio-X Estratégico — Decodificando o 2º Dia do ENEM (Ciências da Natureza)

Ecossistema digital interativo para aula preparatória do ENEM, baseado no plano de aula **"Raio-X Estratégico"**. Aplicação web 100% front-end (single-file), sem backend, pronta para execução local ou hospedagem no **GitHub Pages**.

![Stack](https://img.shields.io/badge/HTML5-Tailwind%20CSS%20%C2%B7%20Chart.js%20%C2%B7%20Lucide-3159C9)

> **Nota de versão:** esta é a Sprint 6 do projeto — uma reconstrução crítica e visual sobre o código legado. Veja [`SPRINTS.md`](SPRINTS.md) para o histórico completo e o backlog.

---

## Estrutura do repositório

```
├── index.html       → Aplicação web interativa (dashboard + estudo de caso + Think-Pair-Share + distratores/TRI)
├── checklist.html   → Guia de estudos da reta final (otimizado para impressão/PDF via @media print)
├── mapa_calor.csv   → Base de dados: frequência relativa de temas ENEM 2015–2025 (fonte do mapa de calor)
├── docs/            → Documentos de planejamento da aula
├── SPRINTS.md       → Histórico de sprints, auditoria do código legado e backlog
└── README.md        → Este arquivo
```

## Como executar

**Local:** basta abrir `index.html` em qualquer navegador moderno (não requer servidor).

**GitHub Pages:**
1. Faça push deste repositório para o GitHub;
2. Em **Settings → Pages**, selecione a branch `main` e a pasta `/ (root)`;
3. Acesse `https://<seu-usuário>.github.io/<repo>/`.

> As dependências (Tailwind CSS, Chart.js, Lucide Icons, fontes Space Grotesk/IBM Plex) são carregadas via CDN — é necessária conexão com a internet.

## Módulos da aplicação

| Aba | Conteúdo |
|---|---|
| **Dashboard analítico** | Gráfico de rosca (Biologia/Química/Física, 33,3% cada), matriz Dificuldade × TRI e mapa de calor temático (23 subtemas do CSV, com filtro por disciplina e modal de competências BNCC/ENEM) |
| **Estudo de caso: água** | Infográfico da Estação de Tratamento de Água integrando as três ciências — coagulação/floculação (Química), decantação (Física), desinfecção/cloração (Biologia) — e a cadeia interativa da eutrofização |
| **Think-Pair-Share** | Cronômetro por fase (Think 2 min / Pair 3 min / Share 2 min) e 2 questões estilo ENEM com duplo feedback: gabarito comentado + análise técnica dos distratores |
| **Distratores e TRI** | Tabela filtrável dos 3 perfis de distratores (falsa verdade, inversor de causa-efeito, generalista absoluto) e protocolo prático do 2º dia em 4 passos |

## Sistema de design

O visual foi reconstruído em torno do conceito de **raio-x/diagnóstico**: painel escuro com textura de grade no cabeçalho (referência a negatoscópio), tipografia técnica e dados em fonte monoespaçada, evitando o padrão genérico de cards arredondados com sombra. Detalhes em [`SPRINTS.md`](SPRINTS.md).

- **Tipografia:** Space Grotesk (títulos), IBM Plex Sans (texto), IBM Plex Mono (dados, percentuais, códigos de competência e cronômetro).
- **Cor:** paleta neutra (`--paper`/`--ink`) com cores fixas por disciplina (Biologia, Química, Física) e por nível de risco na TRI (fácil/médio/difícil), consistentes em todos os gráficos e cartões.
- **Modo claro/escuro:** via `prefers-color-scheme` com alternância manual persistida em `localStorage`, controlada por variáveis CSS (`--paper`, `--ink`, etc.).
- **Acessibilidade:** abas com `role="tablist"`/`aria-selected`, link de pular para o conteúdo, `aria-label` nos gráficos, contraste revisado, `prefers-reduced-motion` respeitado e foco visível em todos os elementos interativos.

## Contexto pedagógico

- **Trilha:** Ampliação do Repertório em Ciências da Natureza e suas Tecnologias
- **Público-alvo:** Ensino Médio (2º e 3º anos) · Curso preparatório comunitário
- **Duração da aula:** 50 minutos · **Metodologia:** Estudo de Caso Integrado + Think-Pair-Share
- **Competências BNCC:** Específicas 1 e 3 de Ciências da Natureza
