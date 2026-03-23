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

> A definir — ver seção "Projeto e Tecnologias" ao final deste documento.

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

- [ ] A definir junto com o projeto (ex: skill de criação de endpoint, skill de escrita de teste, skill de geração de migration)

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

- [ ] A definir junto com o projeto (stack, padrões de código, skills disponíveis, convenções do time)

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

- [ ] A definir junto com o projeto (deve ser complexa o suficiente para justificar o uso de planos)

---

## Pendências Técnicas

- [ ] Remover slide de intervalo com contador regressivo (`chapters/04-intervalo-contador-regressivo.md`)
- [ ] Atualizar slide de capa com novo título/repositório
- [ ] Revisar/atualizar ou remover capítulos antigos que não se encaixam na nova proposta
- [ ] Criar novos capítulos para cada módulo acima
- [ ] Atualizar referências e materiais de estudo

---

## Projeto e Tecnologias

> Pendente de decisão.

**Critérios para escolha do projeto:**

- Familiar para o público (devs seniores e leads)
- Simples o suficiente para não distrair do aprendizado
- Complexo o suficiente para justificar o uso de skills, `AGENTS.md` e planos
- Deve permitir criar pelo menos 2-3 skills relevantes
- A feature do módulo 3 deve ter múltiplas etapas (ideal para demonstrar planos)

**Opções de stack a considerar:**

- Backend Java (Spring Boot) + testes (JUnit/Mockito) — familiar para a maioria do público DB1
- Backend Node.js (NestJS) — alternativa mais leve
- Full stack com Angular no front — aumenta complexidade, mas amplia exemplos

**Decisões pendentes:**

- [ ] Definir o domínio/contexto do projeto (ex: API de gestão de tarefas, sistema de pedidos, etc.)
- [ ] Definir a stack tecnológica
- [ ] Definir as skills que serão criadas
- [ ] Definir a feature do módulo 3

---

## Notas e Decisões

- Os exemplos devem usar GitHub Copilot como referência, mas as técnicas ensinadas devem ser apresentadas como agnósticas de ferramenta
- Priorizar exemplos práticos e exercícios hands-on
- Foco em ganhos de produtividade mensuráveis (tokens economizados, tempo de implementação, consistência de padrões)
- O projeto prático deve ser o mesmo do início ao fim — isso reforça a narrativa de evolução do setup
