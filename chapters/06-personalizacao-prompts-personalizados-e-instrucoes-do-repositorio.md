## Personalizando o Copilot

> No momento, só há suporte às prompts personalizadas de repositório para o Copilot Chat no Visual Studio, VS Code e no site do GitHub. Já instruões personalizadas de repositório estão disponíveis para o Copilot Chat no JetBrains IDEs, Visual Studio, VS Code, Xcode, e no site do GitHub.

- Como adaptar o Copilot para seus projetos.
- Configuração de prompts personalizados.

---

## Criando Prompts Personalizados

<style>
.small {
  transform: scale(0.25);
  margin: -130px 0;
  transition: transform,margin 0.3s ease;
}
</style>

<div :class="{ small: $slidev.nav.clicks >= 3 }">

Prompts personalizados permitem reutilizar comandos comuns para gerar código ou respostas específicas, adaptando o Copilot ao seu fluxo de trabalho.

```markdown {1-4|5-15|all}
---
mode: 'agent'
description: 'Gerar novo controller utilizando Spring Boot'
---
Seu objetivo é gerar um novo controller Spring Boot com base nos templates deste repositório.

Peça o nome do controller e os endpoints relevantes, caso não sejam informados.

Requisitos para o controller:
* Utilize anotações do Spring Web para definir os endpoints
* Sempre defina DTOs de request e response
* Prefira injeção de dependências via construtor
* Use anotações de validação nos parâmetros das requisições
* Crie testes unitários para o controller
* Crie esquemas de validação reutilizáveis em arquivos separados
```

</div>

<div v-click="3">

**Passos Práticos**:

1. Abra o VSCode e acesse as configurações: Pressione `Ctrl + ,` (ou `Cmd + ,` no Mac).
1. Busque por `Chat: Prompt Files` e verifique se está habilitado.
1. Crie o arquivo: Pressione `Ctrl + Shift + P` (ou `Cmd + Shift + P` no Mac), busque por "Chat: New Prompt File" e dê um nome (ex.: "generate-controller"). O arquivo será criado com o nome `generate-controller.prompt.md` na pasta `.github/prompts`.
1. Escreva o prompt no arquivo Markdown, incluindo instruções, referências a arquivos usando Markdown ou a sintaxe `#file:../../web/index.ts`.
1. No Chat, digite `/` seguido do nome do prompt (ex.: `/generate-controller`) para usar o prompt personalizado.

</div>

---

## Configurando Instruções Personalizadas

<style>
.small {
  transform: scale(0.7);
  margin: -10px 0;
  transition: transform,margin 0.3s ease;
}
</style>

<div :class="{ small: $slidev.nav.clicks >= 3 }">

As instruções personalizadas permitem adaptar o comportamento do Copilot Chat ao contexto do seu projeto ou equipe, tornando as respostas mais alinhadas às suas necessidades.

```markdown {1-3|4-|all}
---
applyTo: '**'
---
- Sempre explique as sugestões de código de forma didática.
- Priorize exemplos em Java e Angular.
- Considere as convenções de código deste projeto.
- Responda em português.
- Sugira boas práticas e links para documentação oficial quando possível.
```

</div>

<div v-click="3">

**Passos Práticos**:

1. Crie o arquivo `.github/copilot-instructions.md`.
1. Escreva as instruções no arquivo Markdown, detalhando preferências, padrões e exemplos.
1. As instruções estarão disponíveis para o Chat assim que o arquivo for salvo.
1. O Copilot Chat passará a considerar essas instruções em todas as respostas dentro do repositório.

</div>
