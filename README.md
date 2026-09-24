# 🎯 Raio-X Estratégico — Decodificando o 2º Dia do ENEM (Ciências da Natureza)

Ecossistema digital interativo para aula preparatória do ENEM, baseado no plano de aula **"Raio-X Estratégico"**. Aplicação web 100% front-end (single-file), sem backend, pronta para execução local ou hospedagem no **GitHub Pages**.

![Stack](https://img.shields.io/badge/HTML5-Tailwind%20CSS%20%C2%B7%20Chart.js%20%C2%B7%20Lucide-1d4ed8)

---

## 📦 Estrutura do Repositório

```
├── index.html       → Aplicação web interativa (dashboard + estudo de caso + simulação + checklist TRI)
├── checklist.html   → Guia de Estudos da Reta Final (otimizado para impressão/PDF via @media print)
├── mapa_calor.csv   → Base de dados: frequência relativa de temas ENEM 2015–2025 (fonte do heatmap)
└── README.md        → Este arquivo
```

## 🚀 Como Executar

**Local:** basta abrir o `index.html` em qualquer navegador moderno (não requer servidor).

**GitHub Pages:**
1. Faça push deste repositório para o GitHub;
2. Em **Settings → Pages**, selecione a branch `main` e a pasta `/ (root)`;
3. Acesse `https://<seu-usuario>.github.io/<repo>/`.

> As dependências (Tailwind CSS, Chart.js, Lucide Icons, fonte Inter) são carregadas via CDN — é necessária conexão com a internet.

## 🧩 Módulos da Aplicação

| Aba | Conteúdo |
|---|---|
| 📊 **Dashboard Analítico** | Gráfico de rosca (Biologia 33,3% / Química 33,3% / Física 33,3%), Mapa de Calor Temático interativo (23 subtemas do CSV com filtro por disciplina e modal de competências BNCC/ENEM) e Matriz Dificuldade × TRI |
| 💧 **Estudo de Caso: Tratamento de Água** | Infográfico da ETA integrando as 3 ciências: Coagulação/Floculação (Química), Decantação (Física), Desinfecção/Cloração (Biologia) + cadeia interativa da eutrofização |
| 🧩 **Desafio Think-Pair-Share** | Cronômetro por fase (Think 2 min / Pair 3 min / Share 2 min), 2 questões estilo ENEM com duplo feedback: gabarito comentado + análise técnica dos distratores |
| 📋 **Checklist & Dicas TRI** | Tabela filtrável dos 3 perfis de distratores (Falsa Verdade, Inversor de Causa-Efeito, Generalista Absoluto) e Protocolo Prático do 2º Dia em 4 passos |

## 🎨 UI/UX

- Design executivo estilo Tailwind/Shadcn, totalmente **responsivo**;
- **Modo claro/escuro** com persistência em `localStorage`;
- Cores do mapa de calor fiéis ao CSV: `#D9534F` (muito alta), `#F0AD4E` (alta), `#FFD166` (média), `#5CB85C` (baixa).

## 🗺️ Contexto Pedagógico

- **Trilha:** Ampliação do Repertório em Ciências da Natureza e suas Tecnologias
- **Público-alvo:** Ensino Médio (2º e 3º anos) · Curso Preparatório Comunitário
- **Duração da aula:** 50 minutos · **Metodologia:** Estudo de Caso Integrado + Think-Pair-Share
- **Competências BNCC:** Específicas 1 e 3 de Ciências da Natureza
