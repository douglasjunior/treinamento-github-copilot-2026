---
layout: center
---

# Planos

---

## O que é o modo Plan?

O **Plan** é um agente focado em criar um plano de implementação estruturado **antes de escrever código**.

- Quebra uma tarefa complexa em etapas menores
- Faz perguntas de esclarecimento quando faltar contexto
- Propõe passos de implementação e verificação
- Permite revisar o plano antes de partir para execução

> No VS Code, você pode iniciar pelo seletor de agente ou com `/plan` no chat.

---

## Por que usar Plan antes de codar?

<div :class="{ 'dynamic-hidden': $slidev.nav.clicks >= 4 }" class="dynamic-section">

**Custo menor de ajuste**

<v-clicks>

- Alterar um item de plano leva segundos
- Alterar código espalhado em vários arquivos custa muito mais

**Economia de contexto e tokens**
- Você discute arquitetura e critérios uma vez no plano
- Evita loops longos de "muda isso", "desfaz aquilo"

</v-clicks>

</div>

<div :class="{ 'dynamic-hidden': $slidev.nav.clicks < 4 }" class="dynamic-section">

<v-clicks>

**Menos retrabalho**
- Plano bem definido reduz mudanças tardias
- Critérios de aceite claros evitam ambiguidades

**Melhor previsibilidade**
- Time consegue revisar escopo antes de implementar
- Facilita handoff para execução com mais segurança

</v-clicks>

</div>

---

## Cenários Ideais para Planos

**Use Plano quando**

<v-clicks>

- Features que mexem em múltiplas camadas (UI + service + validação)
- Refatorações com risco de regressão
- Demandas com critérios de aceite detalhados
- Tarefas com dependências entre etapas

**Evite Plano quando**

- A mudança é pontual e de baixo impacto
- Você já sabe exatamente o arquivo e a linha a alterar

</v-clicks>

---

## Como Pedir um Bom Plano

**Inclua no prompt**

<v-clicks>

1. **Objetivo funcional** (o que precisa acontecer)
2. **Restrições técnicas** (onde implementar, o que não quebrar)
3. **Fontes já existentes** (services/utilitários já prontos)
4. **Critérios de aceite** (como validar que deu certo)

**Checklist rápido do plano gerado**

- Está decomposto em etapas sequenciais?
- Cobre implementação + testes/verificação?
- Usa estruturas já existentes do projeto?
- Evita criar soluções paralelas desnecessárias?

</v-clicks>

---

## Demonstração: Criando o Plano de CNPJ

**Pedir ao agente um plano para**

<v-clicks>

- Criar um Input em `src/components` para uso de CNPJ com máscara (máscara já implementada em um service que criamos)
- Aplicar o algoritmo de validação de CNPJ (validação já implementada em um service que criamos) no form de cadastro de empresas
- Aplicar máscara em todas as telas em que o CNPJ for exibido

<div style="transform: scale(0.65); transform-origin: top left; width: 800px;">

```md
Crie um plano de implementação

Objetivo:
- Criar um Input reutilizável para uso de CNPJ com máscara.
- Aplicar a validação de CNPJ no formulário de cadastro de empresas.
- Exibir CNPJ com máscara em todas as telas em que ele aparece.

Contexto importante:
- A lógica de máscara já existe implementada em um service do projeto.
- O algoritmo de validação de CNPJ já existe implementado em um service do projeto.
- Input de texto genérico já existe, utilize-o como base para criar o Input de CNPJ.
- Reaproveite o que já existe; não crie uma segunda implementação paralela.

O plano deve conter:
1. Mapeamento dos arquivos/pontos de alteração.
2. Etapas em ordem de execução.
3. Critérios de aceite por etapa.
4. Riscos e verificações (incluindo regressão visual e funcional).
5. Estratégia de validação final (fluxo feliz e fluxo de erro).
```

</div>

</v-clicks>

---

## Passos Práticos no Projeto

**Vamos praticar o fluxo completo de Plan -> Agent**

<v-clicks>

1. Abrir chat no modo `Plan` (ou usar `/plan`).
2. Executar o prompt do slide anterior.
3. Responder perguntas de esclarecimento do agente.
4. Refinar o plano até ficar objetivo, sequencial e verificável.
5. Só depois aprovar handoff para implementação.

</v-clicks>
