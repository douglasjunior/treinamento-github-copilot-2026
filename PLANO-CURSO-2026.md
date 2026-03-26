# Plano do Curso - Dominando o GitHub Copilot 2026

## Contexto

Atualização do curso para focar em **abordagens modernas de trabalho com agentes de geração de código**.

- **Ferramenta principal**: GitHub Copilot (uso institucional)
- **Foco**: Técnicas genéricas, aplicáveis além do Copilot
- **Público-alvo**: Desenvolvedores seniores e tech leads que já usam GitHub Copilot no dia a dia, mas de forma básica
- **Duração total**: ~3 horas (3 módulos de ~1 hora cada)

---

## Fio Condutor do Curso

Os 3 módulos se conectam em torno de **um único projeto prático** que evolui ao longo do curso:

1. **Módulo 1 (Skills)**: o time cria skills para padronizar fluxos comuns do projeto
2. **Módulo 2 (Instruções)**: o time escreve o `AGENTS.md` do projeto, incorporando as skills criadas e as regras do contexto
3. **Módulo 3 (Planos)**: com as skills e o `AGENTS.md` prontos, o time usa planos para implementar uma feature do projeto de forma guiada

O participante sai do curso com um setup completo e funcional para uso no dia a dia.

---

## Projeto Prático do Curso

**CRM B2B Simplificado** — aplicação frontend com persistência via Web SQL no browser (sem backend externo).

### Por que esse projeto?

- Todo dev sênior já trabalhou ou vai trabalhar com algo parecido
- Entidades claras e relacionadas: `Empresa` → `Contato` → `Interação`
- CNPJ é o identificador central de `Empresa` — uso 100% natural
- A ausência intencional de validação e máscara de CNPJ cria o problema visível que o módulo 3 resolve
- Complexidade suficiente para justificar skills, `AGENTS.md` e planos sem distrair do aprendizado

### Funcionalidades da aplicação

- Listagem de empresas (com CNPJ exibido sem máscara — problema visível)
- Cadastro e edição de empresa (razão social, CNPJ em input comum, segmento, status)
- Lista de contatos vinculados a uma empresa (nome, cargo, e-mail, telefone)
- Registro de interações por empresa (tipo: reunião/ligação/e-mail, data, descrição)

### Stack

- **Frontend**: React + TypeScript + Tailwind CSS (gerado via Lovable)
- **Persistência**: Web SQL / IndexedDB no browser (sem backend)
- **Skills pré-instaladas**: sobre React, TypeScript e padrões do projeto

### Papel de cada módulo no projeto

| Módulo | O que será feito no projeto |
|--------|----------------------------|
| 1 - Skills | Criar skill de implementação de service e skill com algoritmo de validação de CNPJ |
| 2 - Instruções | Pedir à IA para gerar o `AGENTS.md` do projeto e refiná-lo |
| 3 - Planos | Criar plano para implementar validação de CNPJ + input com máscara; refinar o plano; autorizar implementação |

### Skills do projeto prático

- [x] Skills pré-instaladas (sobre React, TypeScript, padrões do projeto) — instaladas antes do curso
- [ ] **Skill: implementar um service** — criada no módulo 1 como demonstração
- [ ] **Skill: algoritmo de validação de CNPJ** — criada no módulo 1 como demonstração

---

## Estrutura dos Módulos

### Modulo 1 - Skills (~1 hora)

**Objetivo**: entender o que são skills, por que usá-las e criar as primeiras skills do projeto prático.

| # | Tópico | Tempo estimado |
|---|--------|----------------|
| 1 | O que são skills de agentes de IA | 10 min |
| 2 | Por que usar: padronização, reuso, golden path do time | 10 min |
| 3 | Como criar uma skill manualmente e com https://agentskills.io | 15 min |
| 4 | Reuso de skills: como compartilhar e reaproveitar — exemplo com `skills.sh` | 10 min |
| 5 | Demonstração: criando skills para o projeto prático do curso | 10 min |
| 6 | Exercício: participantes criam suas próprias skills | 15 min |

**Skills que serão criadas no projeto prático:**

- [ ] Skill: como implementar um service no projeto (padrões, estrutura, onde colocar)
- [ ] Skill: algoritmo de validação de CNPJ (lógica passo a passo para a IA reproduzir corretamente)

---

### Modulo 2 - Instruções aos Agentes (~1 hora)

**Objetivo**: entender o que são instruções de repositório, como escrevê-las bem e criar o `AGENTS.md` do projeto prático.

| # | Tópico | Tempo estimado |
|---|--------|----------------|
| 1 | O que são instruções de repositório/agente | 10 min |
| 2 | Por que usar: economiza tokens, otimiza contexto, melhora consistência | 10 min |
| 3 | Como criar: `AGENTS.md` e `.github/copilot-instructions.md` | 10 min |
| 4 | Boas práticas: o que incluir, o que evitar, como referenciar skills | 10 min |
| 5 | Demonstração: criando o `AGENTS.md` do projeto prático | 5 min |
| 6 | Exercício: participantes criam/melhoram o `AGENTS.md` | 15 min |

**Conteúdo do `AGENTS.md` do projeto prático:**

- [ ] Gerado pela própria IA a partir do código do projeto usando o prompt abaixo (demonstração ao vivo)
- [ ] Refinado pelos participantes: stack, padrões de código, skills disponíveis, convenções do time

**Prompt para geração dos `AGENTS.md`:**

> Prompt genérico — funciona em qualquer projeto e qualquer estrutura.

```
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
- Skills disponíveis no projeto e quando usá-las (se houver arquivo skills.sh ou similar)
- Mapa dos demais AGENTS.md existentes e o que cada um cobre

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

### Diretório de serviços/lógica de negócio (ex: services/, usecases/, domain/)
- Como criar um novo service: estrutura, nomenclatura, responsabilidades
- Padrões de tratamento de erro e retorno
- Como os services se conectam à camada de persistência

### Outros diretórios relevantes encontrados
- Analise e documente conforme o contexto (ex: hooks/, store/, utils/, types/, api/)

## Ao finalizar
Liste todos os arquivos AGENTS.md criados ou modificados e um resumo de uma linha sobre o que cada um cobre.
```

---

### Modulo 3 - Trabalhando com Planos (~1 hora)

**Objetivo**: usar planos para implementar uma feature no projeto prático, aproveitando as skills e o `AGENTS.md` criados nos módulos anteriores.

| # | Tópico | Tempo estimado |
|---|--------|----------------|
| 1 | O que são planos no contexto de agentes de IA | 10 min |
| 2 | Como criar um plano eficaz: especificidade, decomposição, critérios de aceite | 10 min |
| 3 | Refinamento de plano (rápido) vs. refinamento de código (lento e custoso) | 10 min |
| 4 | Demonstração: criando e executando um plano para o projeto prático | 15 min |
| 5 | Exercício: participantes criam e executam seus próprios planos | 15 min |

**Feature a ser implementada via plano:**

- [ ] Validação de CNPJ com algoritmo correto + input com máscara no cadastro de empresas
  - Etapas: criar service de validação → aplicar skill de algoritmo → criar componente de input com máscara → integrar no formulário → tratar erros de validação

---

## Pendências Técnicas

1. [x] **Preservar histórico do curso 2025**
  - Renomear `./chapters` para `./chapters-2025` (ou similar).
  - Critério de aceite: conteúdo antigo preservado e acessível para consulta/reuso.
  - Status: concluído em 2026-03-25 (`./chapters` -> `./chapters-2025`).

2. [x] **Criar a base do novo deck 2026**
  - Criar nova pasta `./chapters` para os capítulos 2026.
  - Atualizar `slides.md` com novo título/repositório e apontamento para os novos capítulos.
  - Critério de aceite: deck abre com capa 2026 e sem dependência do conteúdo antigo.
  - Status: concluído em 2026-03-26. Pasta `./chapters` criada vazia. Imports antigos comentados em `slides.md` e preparados para receber os novos capítulos 2026.

3. [x] **Inserir o slide de introdução após a capa**
  - Criar novo arquivo `chapters/01-introducao-ask-plan-agent.md` com slide de diferenças entre Ask, Plan e Agent.
  - Ativar import deste capítulo em `slides.md` descomentando a linha correspondente.
  - Incluir exemplos rápidos de quando usar cada modo.
  - Critério de aceite: slide de introdução aparece imediatamente após a capa no fluxo da apresentação.
  - Status: concluído em 2026-03-26. Arquivo criado e import ativado em slides.md.

4. [ ] **Construir capítulo do Módulo 1 (Skills)**
  - Criar slides do módulo focando em criação, reuso e compartilhamento de skills.
  - Incluir demonstração das 2 skills do projeto prático (service e validação de CNPJ).
  - Critério de aceite: módulo completo e executável no workshop sem depender dos módulos 2 e 3.

5. [ ] **Construir capítulo do Módulo 2 (Instruções)**
  - Criar slides do módulo focando em `AGENTS.md` e `.github/copilot-instructions.md`.
  - Incluir demonstração de geração e refinamento do `AGENTS.md` do projeto prático.
  - Critério de aceite: módulo completo com roteiro claro de escrita e revisão de instruções.

6. [ ] **Construir capítulo do Módulo 3 (Planos)**
  - Criar slides do módulo focando em criação/refino/execução de planos.
  - Usar como caso principal a feature de validação e máscara de CNPJ.
  - Critério de aceite: módulo completo com fluxo fim a fim do plano até a implementação.

7. [ ] **Remover conteúdo que não se encaixa na proposta 2026**
  - Excluir/omitir o slide de intervalo com contador regressivo (`chapters/04-intervalo-contador-regressivo.md`).
  - Revisar sobras de capítulos antigos que não forem reaproveitados.
  - Critério de aceite: deck final sem quebras de ritmo e sem seções fora do novo objetivo.

8. [ ] **Fechar materiais de apoio**
  - Atualizar referências e materiais de estudo para 2026.
  - Critério de aceite: links e materiais alinhados com os tópicos e ferramentas do novo curso.

---

## Execução Incremental (Slide a Slide)

Para reduzir risco e manter qualidade, a migração 2026 será feita em ciclos curtos:

1. Definir objetivo do slide.
2. Definir conteúdo exato do slide.
3. Definir prática/exercício associado no curso.
4. Validar aderência ao padrão visual e estrutural do curso 2025.
5. Só então avançar para o próximo slide.


---

## Notas e Decisões

- Os exemplos devem usar GitHub Copilot como referência, mas as técnicas ensinadas devem ser apresentadas como agnósticas de ferramenta
- Priorizar exemplos práticos e exercícios hands-on
- Foco em ganhos de produtividade mensuráveis (tokens economizados, tempo de implementação, consistência de padrões)
- O projeto prático deve ser o mesmo do início ao fim — isso reforça a narrativa de evolução do setup
- Atualize o AGENTS.md sempre que os slides mudarem
- Mantenha esse plano atualizado e referencie-o durante a construção dos slides para garantir alinhamento com os objetivos do curso
