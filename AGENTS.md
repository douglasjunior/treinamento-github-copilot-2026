# AGENTS.md

Este documento descreve a estrutura, padrões e tecnologias dos slides do workshop **"Dominando o GitHub Copilot"**, facilitando a navegação e edição por agentes de IA.

---

## Estrutura de Arquivos

O arquivo principal é `slides.md`. Ele contém apenas o slide de capa e importa os capítulos via diretiva `src:` do Slidev. Todo o conteúdo dos slides está nos arquivos da pasta `chapters/`.

---

## Índice de Capítulos

| Arquivo | Slides | Conteúdo resumido |
|---|---|---|
| `slides.md` | Capa | Slide de abertura do workshop com título, autor e repositório. |
| `chapters/01-introducao-ask-plan-agent.md` | 1 | Introdução aos modos Ask, Plan e Agent com diferenças de uso. |
| `chapters/01a-cenarios-agentes.md` | 1 | Cenários de aplicação de agentes com revelação progressiva. |
| `chapters/02-modulo-1-skills.md` | 10+ | Módulo 1: conceito de skills, estrutura, uso no Copilot, prompting, reuso e demo de skill CNPJ. |
| `chapters/03-modulo-2-instrucoes.md` | 7+ | Módulo 2: AGENTS.md, benefícios, seções, boas práticas e demo de geração com prompt completo. |
| `chapters/04-modulo-3-planos.md` | 7+ | Módulo 3: modo Plan, vantagens, cenários, criação e refinamento de plano para a feature de CNPJ. |
| `chapters/05-referencias.md` | 1 | Referências oficiais e materiais de apoio para continuidade após o workshop. |

---

## Tecnologias e Framework

- **Slidev** (`@slidev/cli`) — framework de slides baseado em Markdown e Vue 3.
- **Tema**: `dracula` — paleta escura com roxo (`#bd93f9`) e rosa (`#ff79c6`) como cores de destaque.
- **Vue 3** com `<script setup>` — usado para lógica interativa nos slides (ex.: contador regressivo).
- **MDC (Markdown Components)** — habilitado via `mdc: true` no frontmatter, permite uso de componentes Vue inline no Markdown.

---

## Padrões dos Slides

### Frontmatter do arquivo principal (`slides.md`)
```yaml
theme: dracula
background: ./public/mohammad-rahmani-*.jpg
title: Dominando o GitHub Copilot - Workshop Prático
layout: cover
transition: slide-left
lineNumbers: true
mdc: true
selectable: true
```

### Separador entre slides
Use `---` para separar slides dentro de um arquivo de capítulo. Slides com layout especial usam:
```md
---
layout: center
---
```

### Estilos locais por slide
Blocos `<style>` dentro de um slide aplicam estilos com escopo local (apenas àquele slide). O padrão usado para animar zoom de código é:
```html
<style>
.small {
  transform: scale(0.X);
  margin: -Xpx 0;
  transition: transform, margin 0.3s ease;
}
</style>
```

### Classe `.btn-default`
Definida globalmente em `slides.md`. Use em botões interativos:
```html
<button class="btn-default" @click="handler">Label</button>
```

### Animações com cliques
- `<v-click>` — exibe o conteúdo no próximo clique.
- `<v-clicks>` — exibe cada item filho em cliques sucessivos.
- `v-click="N"` — exibe no N-ésimo clique do slide.
- `:class="{ small: $slidev.nav.clicks >= N }"` — aplica classe a partir do N-ésimo clique.

### Exemplos de código
- Use highlight de linhas com `{linha|linha|all}` para guiar o apresentador passo a passo.
- Use `::code-group` para mostrar o mesmo exemplo em múltiplas linguagens (Java e TypeScript).
- Use ` ````md magic-move ` para animar a transição entre dois blocos de código.

### Linguagens de exemplo usadas nos slides
Os exemplos práticos são sempre apresentados em **Java** (backend Spring Boot) e **TypeScript/Angular** (frontend), refletindo o stack da DB1.

### Passos Práticos
Todo slide com exemplo de código deve ter uma seção `**Passos Práticos**` com instruções numeradas para o participante executar durante o workshop. Esses passos aparecem via `v-click` após a demonstração do código.

---

## Idioma

Todo o conteúdo dos slides deve ser escrito em **português brasileiro**.

---

Mantenha este guia atualizado conforme o workshop evolui, garantindo que os agentes de IA possam navegar e editar os slides de forma consistente e eficiente.
