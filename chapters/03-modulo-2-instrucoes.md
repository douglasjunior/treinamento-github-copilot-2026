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

<v-clicks>

<div :class="{ 'dynamic-hidden': $slidev.nav.clicks < 1 }" class="dynamic-section">

**Padrões mais usados**

- `AGENTS.md`: formato aberto e agnóstico de ferramenta. [Ver mais](https://agents.md)
- `.github/copilot-instructions.md`: formato específico do GitHub Copilot. [Ver mais](https://docs.github.com/pt/copilot/how-tos/configure-custom-instructions)
- `CLAUDE.md`: formato específico do Anthropic Claude. [Ver mais](https://code.claude.com/docs/en/memory)


**Resultado**

Sem instruções, o agente tende a improvisar, **realizando repetitivos escaneamentos** para entender a base de código. Com instruções, ele **segue diretrizes claras**, economizando tempo e entregando resultados mais alinhados.

</div>

</v-clicks>

---

## Por que Usar Instruções?

<div :class="{ 'dynamic-hidden': $slidev.nav.clicks >= 4 }" class="dynamic-section">

**Economize contexto e tempo**

<v-clicks>

- Sem instruções, o agente reinicia do zero a cada tarefa — varrendo arquivos para entender a arquitetura
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

É apenas **Markdown**. Sem campos obrigatórios — use os títulos que fizerem sentido.

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

A maioria dos agentes consegue scaffoldar um para você — basta pedir.

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

## Demonstração: Gerando o AGENTS.md com Agent

**Prompt base da demonstração**

```md
Analise este repositório e crie um AGENTS.md na raiz.

Objetivo:
- refletir a arquitetura real do projeto
- documentar convenções técnicas de implementação
- listar skills disponíveis e quando usar
- incluir checklist de qualidade antes de encerrar tarefas

Escreva de forma direta para um agente de código.
```

<v-click>

**Passos Práticos**

1. Abrir o chat no modo Agent dentro do projeto.
2. Executar o prompt acima sem detalhar a estrutura manualmente.
3. Revisar se o resultado bate com pastas reais e padrão do time.
4. Salvar AGENTS.md e commitar junto do módulo.

</v-click>

---

## Refinamento do AGENTS.md (Checklist)

<div :class="{ 'dynamic-hidden': $slidev.nav.clicks >= 1 }" class="dynamic-section">

**Primeira revisão**

- O documento descreve as pastas corretas?
- Fala dos tipos e de onde vem os dados?
- Explica como criar service no padrão do projeto?
- Menciona skills e critério de uso?

</div>

<div :class="{ 'dynamic-hidden': $slidev.nav.clicks < 1 }" class="dynamic-section">

**Segunda revisão (qualidade)**

- Tem regras objetivas e acionáveis?
- Evita texto genérico e redundante?
- Inclui checklist de validação final?
- Está claro para quem nunca viu o projeto?

**Meta**: AGENTS.md curto, útil e operacional.

</div>

---

## Exemplo: copilot-instructions.md

Arquivo: `.github/copilot-instructions.md`

```md
---
applyTo: '**'
---

- Responda em portugues brasileiro.
- Responda em português brasileiro.
- Priorize exemplos em TypeScript.
- Em alterações de código, preserve padrões do projeto.
- Antes de concluir, verifique erros de lint/build quando possível.
```

<v-click>

**Passos Práticos**

1. Criar o arquivo .github/copilot-instructions.md.
2. Definir 4-6 regras curtas e objetivas.
3. Validar com um prompt simples se as regras foram aplicadas.

</v-click>

---

## Exercício Final do Módulo 2

Objetivo: sair com instruções do projeto prontas para suportar o módulo 3.

**Entregáveis**
- AGENTS.md inicial gerado e refinado
- .github/copilot-instructions.md com regras objetivas

**Critérios de aceite**
- [ ] AGENTS.md com contexto, convenções e skills
- [ ] Regras acionáveis para services e componentes
- [ ] Checklist de qualidade no fim do AGENTS.md
- [ ] Instruções de resposta no copilot-instructions.md

**Conexão com o Módulo 3**: essas instruções serão a base para criar e executar planos com menos retrabalho.
