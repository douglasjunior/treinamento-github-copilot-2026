---
layout: center
---

# Instruções de Repositório

---

## O que são Instruções de Repositório?

<div :class="{ 'dynamic-hidden': $slidev.nav.clicks >= 1 }" class="dynamic-section">

Instruções de repositório são arquivos versionados que orientam como o agente deve atuar dentro daquele projeto.

- Explicam contexto técnico e de negócio
- Definem convenções e limites
- Reduzem respostas genéricas
- Melhoram consistência entre sessões

**Exemplo**: um arquivo `AGENTS.md` na raiz do projeto que descreve a arquitetura, stack, convenções de código e aponta para documentação adicional. O agente consulta esse arquivo para seguir as diretrizes específicas do projeto, ao invés de improvisar a cada tarefa.

</div>

<div :class="{ 'dynamic-hidden': $slidev.nav.clicks < 1 }" class="dynamic-section">
<v-clicks>


**Padrões mais usados**

- `AGENTS.md`: formato aberto e agnóstico de ferramenta. [Ver mais](https://agents.md)
- `.github/copilot-instructions.md`: formato específico do GitHub Copilot. [Ver mais](https://docs.github.com/pt/copilot/how-tos/configure-custom-instructions)
- `CLAUDE.md`: formato específico do Claude Code. [Ver mais](https://code.claude.com/docs/en/memory)


**Resultado**

Sem instruções o agente tende a improvisar, **realizando repetitivos escaneamentos** para entender a base de código. Com instruções, ele **segue diretrizes claras**, economizando tempo e entregando resultados mais alinhados.

</v-clicks>

</div>

---

## Por que Usar Instruções?

<div :class="{ 'dynamic-hidden': $slidev.nav.clicks >= 4 }" class="dynamic-section">

**Economize contexto e tempo**

<v-clicks>

- Sem instruções, o agente reinicia do zero a cada tarefa, varrendo arquivos para entender a arquitetura
- Com instruções, já inicia com o contexto certo: stack, convenções, comandos de build e teste

**Respostas consistentes e previsíveis**
- Instruções específicas funcionam melhor: *"use 2 espaços de indentação"* supera *"formate bem o código"*
- Menos variação entre sessões e entre diferentes agentes do mesmo time

</v-clicks>

</div>

<div :class="{ 'dynamic-hidden': $slidev.nav.clicks < 4 }" class="dynamic-section">

<v-clicks>

**Escale para o time**

- `AGENTS.md` é suportado por Copilot, Claude, Gemini CLI, JetBrains Junie, Warp, entre outros
- Uma instrução única que qualquer agente do time usa, mantida junto ao código

**Acelere o onboarding**

- Novos devs e novos agentes iniciam com o mesmo contexto que o time construiu
- Conhecimento tácito do projeto vira documento ativo, não apenas memória coletiva

**Resultado esperado**

- Menos ambiguidade → menos retrabalho
- Mais previsibilidade nas entregas com qualquer agente

</v-clicks>

</div>

---

## Seções de um AGENTS.md

<div :class="{ 'dynamic-hidden': $slidev.nav.clicks >= 1 }" class="dynamic-section">

É apenas **Markdown**. Sem campos obrigatórios, use os títulos que fizerem sentido.

- **Visão geral** — domínio do negócio, propósito da aplicação, público-alvo
- **Stack** — linguagem, frameworks, gerenciador de pacotes
- **Setup** — como instalar, rodar e testar localmente
- **Convenções** — onde ficam os arquivos, padrões de nomenclatura e organização
- **Instruções de teste** — comandos, onde ficam os testes, quando executar
- **Segurança** — dados sensíveis, restrições, gotchas importantes
- **Checklist** — o que verificar antes de encerrar uma tarefa

</div>

<div :class="{ 'dynamic-hidden': $slidev.nav.clicks < 1 }" class="dynamic-section">

**Exemplo de esqueleto**

<v-clicks>

<div style="transform: scale(0.9); transform-origin: top left;">

````md
# AGENTS.md

## Contexto
Breve descrição do produto, domínio e público-alvo.

## Stack
- Runtime, linguagem principal, frameworks
- Gerenciador de pacotes e comandos comuns

## Convenções
- Onde ficam os módulos/services/componentes
- Padrões de nomenclatura e organização

## Setup
- `<comando de instalação>`
- `<comando para rodar>`
- `<comando de testes>`

## Checklist de entrega
- Sem erros de lint e build
- Tipagem correta
- Padrões do repositório respeitados
````

</div>

</v-clicks>

</div>

---

## Como usar AGENTS.md?

<div>

**1. Crie o arquivo na raiz**

A maioria dos agentes consegue criar um para você, basta pedir.

</div>

<v-clicks>

<div>

**2. Cubra o que importa**

Visão geral do projeto, comandos de build e teste, convenções de código, instruções de testes, considerações de segurança.

</div>

<div>

**3. Adicione instruções extras**

Mensagens de commit, PR guidelines, passos de deploy — tudo que você diria a um novo colega de time.

</div>

<div>

**4. Monorepo? Projeto grande? Use arquivos aninhados**

Coloque um `AGENTS.md` dentro de cada pacote. O agente lê o mais próximo na árvore.

> Por exemplo, atualmente o repositório principal do OpenAI tem 88 arquivos `AGENTS.md`.

</div>

</v-clicks>

---

## Boas Práticas para Escrever AGENTS.md

<div :class="{ 'dynamic-hidden': $slidev.nav.clicks >= 4 }" class="dynamic-section">

**Seja específico, não genérico**

<v-clicks>

- ✅ `"Services ficam em src/services/ como funções exportadas"`
- ❌ `"Mantenha o código organizado"`

**Prefira comandos a descrições**

- ✅ `"Rode 'npm test' antes de encerrar a tarefa"`
- ❌ `"Teste as alterações antes de finalizar"`

</v-clicks>

</div>

<div :class="{ 'dynamic-hidden': $slidev.nav.clicks < 4 }" class="dynamic-section">

<v-clicks>

**Mantenha curto e versionado**

- O agente carrega tudo no contexto a cada sessão, instruções longas podem transbordar a janela de contexto e reduzir aderência
- Trate como documentação viva: commite junto do código, revise quando o padrão mudar
- Evite detalhes que mudam com frequência, foque em diretrizes estáveis

**Grandes bases de código**

- Use `AGENTS.md` aninhados por subprojeto ou pacote, o agente lê o mais próximo na árvore de diretórios
- Mantenha o `AGENTS.md` da raiz para diretrizes globais e visão geral

**Conflito de instruções**

- Caso utilize múltiplos `AGENTS.md`, o arquivo mais próximo do arquivo editado vence
- Prompt explícito do usuário pode sobrepor instruções, mas pode gerar respostas inconsistentes

</v-clicks>

</div>

---

## Gerando o AGENTS.md para nosso projeto

**Vamos usar o agente para criar os arquivos AGENTS.md**

<v-clicks>

1. Abrir o chat no modo `Agent` dentro do projeto e selecionar o modelo `Auto`
2. Executar o prompt abaixo sem detalhar a estrutura manualmente, deixe o agente descobrir.
3. Revisar se o resultado bate com pastas reais e padrão do time.

<div style="transform: scale(0.35); transform-origin: top left; width: 1300px;">

```md
Analise todo o projeto e crie (ou revise e melhore, se já existir) arquivos AGENTS.md em múltiplos níveis do repositório, seguindo as instruções abaixo.

## Regras gerais

- Escaneie toda a estrutura de diretórios e arquivos antes de começar
- Para cada diretório relevante identificado, avalie se um AGENTS.md agrega valor; crie apenas onde fizer sentido
- Se um AGENTS.md já existir em algum diretório, leia seu conteúdo, avalie se está desatualizado ou incompleto e o melhore — não o substitua cegamente
- Escreva de forma direta e objetiva; o leitor é um agente de IA, não um humano
- Evite redundância entre os arquivos: cada AGENTS.md deve conter apenas o que é relevante para aquele escopo
- O AGENTS.md raiz deve mencionar explicitamente onde encontrar os demais arquivos AGENTS.md do projeto

## O que cada nível deve conter

### / (raiz do projeto)
- Descrição do domínio de negócio e propósito da aplicação
- Stack principal (linguagens, frameworks, bibliotecas relevantes)
- Como rodar o projeto localmente
- Convenções gerais de nomenclatura e organização

### Diretórios de código-fonte (ex: src/, app/, lib/)
- Visão geral da estrutura interna de pastas e responsabilidade de cada uma
- Padrões de importação e organização de módulos
- O que pertence a este nível vs. o que deve ser delegado a subdiretórios

### Diretório de componentes (ex: components/, ui/)
- Como criar novos componentes: estrutura de arquivo, nomenclatura, onde colocar
- Padrões de props, estilização e composição
- Componentes utilitários existentes que devem ser reutilizados

### Diretório de páginas/rotas (ex: pages/, views/, routes/)
- Como criar novas páginas e registrar rotas
- Padrão de layout e estrutura esperada de uma página
- Como conectar páginas a serviços e estado

### Diretório de serviços/lógica e demais recursos (ex: services/, usecases/, domain/)
- Como criar um novo recurso: estrutura, nomenclatura, responsabilidades
- Padrões de tratamento de erro e retorno
- Como os recursos se conectam à outras camadas

### Outros diretórios relevantes encontrados
- Analise e documente conforme o contexto (ex: hooks/, store/, utils/, types/, api/)
- Ignore AGENTS.md em diretórios de dependências, skills de terceiro, etc.

## Ao finalizar
Liste todos os arquivos AGENTS.md criados ou modificados e um resumo de uma linha sobre o que cada um cobre.
```

</div>

</v-clicks>
