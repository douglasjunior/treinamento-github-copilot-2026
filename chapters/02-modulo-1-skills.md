## O que são Skills?

**Skills** são instruções estruturadas que ensinam ao agente de IA como realizar tarefas específicas e recorrentes no seu projeto.

- Uma skill é um arquivo com padrões, exemplos e regras
- O agente consulta a skill quando precisa fazer algo similiar
- Evita que o agente "reinvente a roda" ou gere código inconsistente
- Aumenta a qualidade e a velocidade das respostas

**Exemplo**: ao invés de o agente gerar um service diferente cada vez, ele consulta a skill "Como implementar um service" e segue o padrão.

---

## Por que Usar Skills?

<div :class="{ 'dynamic-hidden': $slidev.nav.clicks >= 5 }" class="dynamic-section">

<v-clicks>

**Padronização**
- Todo o time escreve services da mesma forma
- interfaces, tratamento de erro, nomes — tudo consistente

**Reuso**
- Skills criadas uma vez, usadas em muitos projetos
- Economiza tempo de escrita e evita duplicação

</v-clicks>

</div>

<div :class="{ 'dynamic-hidden': $slidev.nav.clicks < 5 }" class="dynamic-section">

<v-clicks>

**Golden Path**
- Estabelece o "caminho certo" para fazer as coisas
- Menos decisões, mais execução

**Controle de Qualidade**
- Garante que geração de código segue boas práticas
- Reduz necessidade de code review detalhado

</v-clicks>

</div>

---

## Estrutura de uma Skill

<div :class="{ 'dynamic-hidden': $slidev.nav.clicks >= 1 }" class="dynamic-section">

**Estrutura de pastas**

```
./.agents/skills/skill-nome/
├── SKILL.md            # Obrigatório: instruções + metadados
├── scripts/            # Opcional: código executável (.ts, .py, etc)
├── references/         # Opcional: documentação adicional
└── assets/             # Opcional: templates, exemplos
```

> Referência: https://agentskills.io/ (padrão aberto)

</div>

<div :class="{ 'dynamic-hidden': $slidev.nav.clicks < 1 }" class="dynamic-section">
<v-clicks>
<div :class="{ 'dynamic-hidden': $slidev.nav.clicks > 1 }" class="dynamic-section">

**Conteúdo do SKILL.md**

```markdown
---
name: skill-implement-service
description: Criar services TypeScript seguindo padrões do projeto
---

# Implementar Service

## Quando usar esta skill
Use quando precisar criar um novo service que:
- Acessa dados (Web SQL, API)
- Encapsula lógica de negócio
- Será reutilizado em múltiplos componentes

## Como implementar
1. Criar arquivo em src/services/[NomeService].ts
2. Seguir padrão de métodos CRUD
3. ...

## Exemplo
[código]
```
</div>

**Scripts**
- Código executável que a skill pode usar durante a execução
- Ex.: scripts TypeScript, Python ou shell para automações pontuais
- Use quando a skill precisar fazer mais do que só orientar em texto

**References**
- Materiais de apoio que o agente pode consultar sob demanda
- Ex.: documentação interna, RFCs, regras de negócio, especificações
- Ideal para conhecimento longo demais para ficar inteiro no `SKILL.md`

**Assets**
- Arquivos auxiliares reutilizáveis pela skill
- Ex.: templates, exemplos-base, trechos de configuração, arquivos modelo
- Útil quando a skill precisa gerar artefatos com formato padronizado
</v-clicks>
</div>

---

## Como o Copilot Usa uma Skill

<div :class="{ 'dynamic-hidden': $slidev.nav.clicks >= 1 }" class="dynamic-section">

**Descoberta**

1. Você cria a skill em `./.agents/skills/skill-nome/SKILL.md` com `name` e `description`
2. O agente **autodescobre** as skills na pasta `./.agents/skills/` ao iniciar
3. Quando a tarefa combina com o `description`, o agente ativa a skill automaticamente
4. Você pede ao Copilot Agent:
    > "Crie um novo service chamado `ContactService`"
5. Copilot detecta a skill de service, lê as regras e gera código consistente

</div>

<v-clicks>
<div :class="{ 'dynamic-hidden': $slidev.nav.clicks < 1 }" class="dynamic-section">

**Uso estratégico de tokens**
- No startup, o agente lê só metadados (ex.: `name` e `description`)
- O campo `description` é o gatilho: ele diz ao agente quando usar a skill.
- O conteúdo completo do `SKILL.md` entra no contexto apenas quando a skill é ativada
- Isso reduz consumo de contexto desnecessário e melhora eficiência

**Resultado**

Sem skill, Copilot gera variações inconsistentes; com skill, gera sempre igual.

</div>
</v-clicks>

---

## Exemplo Básico: Skill de Service

Arquivo: `./.agents/skills/typescript-service/SKILL.md`

- Skill em formato oficial (`SKILL.md`)
- Regras que o Agent deve seguir em toda geração

<div style="transform: scale(0.34); transform-origin: top left; width: 1024px;">

````markdown
---
name: typescript-service
description: Criar services TypeScript funcionais para encapsular acesso externos a aplicação, como chamadas HTTP e IndexedDB.
---

# Implementar Service em TypeScript

## O que é
Um service é um módulo TypeScript com funções que encapsulam acesso externo, normalmente:
- chamadas HTTP
- acesso a IndexedDB
- adaptação de payload entre UI e persistência

## Quando usar
- Quando um componente React precisa salvar ou buscar dados fora dele
- Quando houver integração com API HTTP
- Quando houver persistência local via IndexedDB

## Estrutura

```ts
export async function listCompanies(): Promise<Company[]> {
  // implementação
}

export async function getCompanyById(id: string): Promise<Company | null> {
  // implementação
}

export async function createCompany(data: CompanyInput): Promise<Company> {
  // implementação
}

export async function updateCompany(
  id: string,
  data: CompanyInput,
): Promise<Company> {
  // implementação
}
```

## Regras
- Preferir funções exportadas em vez de classes
- Arquivo nomeado por responsabilidade (ex.: companyService.ts)
- Funções retornam Promise
- Concentrar transformação de payload e tratamento básico de erro no service
- Componente React não acessa HTTP ou IndexedDB diretamente e não deve misturar regra de renderização com persistência

## Exemplo Completo
Arquivo: src/services/companyService.ts
````

</div>

---

## Prompting com a Skill: Exemplo Prático

<div :class="{ 'dynamic-hidden': $slidev.nav.clicks >= 1 }" class="dynamic-section">

Agora vamos **pedir ao Agent** para criar outro service usando a skill de service em TypeScript.

**O que vamos fazer**:

Criar um service que forneça buscas e filtros reutilizáveis:
- buscar empresas por segmento
- listar empresas por status
- histórico de interações recentes

</div>

<v-clicks>

<div :class="{ 'dynamic-hidden': $slidev.nav.clicks != 1 }" class="dynamic-section">

**O Prompt**

```md
Crie um novo service para consultas filtradas, que forneça:

Para empresas:
1. getCompaniesBySegment(segmento: string): retorna empresas filtradas por segmento
2. getCompaniesByStatus(status: string): retorna empresas ativas ou inativas

Para contatos e interações:
3. getRecentInteractions(empresaId: number, limit?: number): retorna últimas interações da empresa
```

</div>

<div :class="{ 'dynamic-hidden': $slidev.nav.clicks != 2 }" class="dynamic-section">

**Resultado esperado**:


<img src="/skill-example.png" alt="Exemplo de uso da skill" style="height: 50vh; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.1);" />

</div>

</v-clicks>

---

## Reuso de Skills

<div :class="{ 'dynamic-hidden': $slidev.nav.clicks >= 5 }" class="dynamic-section">

<v-clicks>

**Skills podem ser tratadas como dependências instaláveis**

- Você mantém skills em um repositório central
- Cada projeto instala apenas as skills necessárias
- Atualizações ficam controladas por versão (sem copiar/colar manual)

**Fluxo recomendado**

1. Publicar skills em um repositório central do time
2. Instalar no projeto com ferramenta de distribuição (ex.: `skills.sh`)
3. Atualizar versão quando quiser adotar melhorias

</v-clicks>

</div>

<div :class="{ 'dynamic-hidden': $slidev.nav.clicks < 5 }" class="dynamic-section">

<v-clicks>

**Por que isso é importante**

- Consistência entre múltiplos projetos
- Governança de qualidade (skills auditáveis e revisáveis)
- Evolução gradual sem quebrar times que ainda usam versões anteriores

**Ecossistema open source**

Ferramentas como `skills.sh` também ajudam a descobrir e instalar uma biblioteca grande de skills open source, acelerando bootstrap de novos projetos.

</v-clicks>

</div>

---

## Demonstração: Criando a Skill de Service

<div :class="{ 'dynamic-hidden': $slidev.nav.clicks >= 1 }" class="dynamic-section">

Vamos criar juntos a skill que será referenciada no projeto CRM:

**Arquivo**: `./agents/skills/skill-typescript-service/SKILL.md`

</div>

<div :class="{ 'dynamic-hidden': $slidev.nav.clicks < 1 }" class="dynamic-section">

```yaml
---
name: skill-typescript-service
description: Criar services TypeScript seguindo padrões do projeto CRM
---

# Implementar Service no Projeto CRM

## O que é
Um service encapsula acesso a dados (Web SQL) ou chamadas remotas de forma consistente.

## Quando usar
- Implementar metodos CRUD
- Consultar dados que múltiplos componentes precisam
- Centralizasr transformações de dados

## Estrutura padrão

export class [NomeService] {
  private db: Database;

  constructor() {
    this.db = getDatabase();
  }

  async getAll(): Promise<[Entity][]> {
    return this.db.query('SELECT * FROM [table]');
  }

  async getById(id: string): Promise<[Entity] | null> {
    const result = await this.db.query(
      'SELECT * FROM [table] WHERE id = ?',
      [id]
    );
    return result[0] || null;
  }

  async create(data: Partial<[Entity]>): Promise<[Entity]> {
    const id = crypto.randomUUID();
    await this.db.execute(
      'INSERT INTO [table] (id, ...) VALUES (?, ...)',
      [id, ...]
    );
    return this.getById(id);
  }

  async update(id: string, data: Partial<[Entity]>): Promise<[Entity]> {
    await this.db.execute(
      'UPDATE [table] SET ... WHERE id = ?',
      [..., id]
    );
    return this.getById(id);
  }

  async delete(id: string): Promise<void> {
    await this.db.execute('DELETE FROM [table] WHERE id = ?', [id]);
  }
}

## Regras
1. Sempre usar async/await
2. Métodos retornam entidade ou array de entidades
3. Usar prepared statements com ?
4. getById retorna null se não encontrar
5. Nome do arquivo: [PalavraService].ts em src/services/
6. Tratar erros com try/catch nos componentes que chamam o service
```

</div>

---

## Exercício 1: Criar Primeira Skill

**Tarefa**: Criar um arquivo `skills/skill-[seu-nome].md` seguindo o template.

**Opções**:
- Skill: Como criar um componente React
- Skill: Como escrever um hook customizado
- Skill: Padrão de tratamento de erros

**Critério de aceite**:
- [ ] Arquivo criado em `skills/`
- [ ] Tem os 4 seções: O que é, Quando usar, Estrutura, Regras
- [ ] Inclui exemplo de código TypeScript
- [ ] Pode ser referenciado em um `AGENTS.md`

**Dica**: mostre a skill para colega; se ele entender o padrão, está bom!

---

## Skill: Validação e Máscara de CNPJ

<div :class="{ 'dynamic-hidden': $slidev.nav.clicks >= 1 }" class="dynamic-section">

Arquivo: `./agents/skills/skill-cnpj-validation/SKILL.md`

- Padrão para validação e máscara reutilizável
- Base para o exercício final e para o módulo de planos

</div>

<div :class="{ 'dynamic-hidden': $slidev.nav.clicks < 1 }" class="dynamic-section">

```yaml
---
name: skill-cnpj-validation
description: Validar CNPJ com algoritmo oficial e aplicar máscara XX.XXX.XXX/XXXX-XX
---

# Validação e Máscara de CNPJ

## O que é
Dois utilitários para trabalhar com CNPJ:
1. `isValidCNPJ()` — valida usando algoritmo dos dígitos verificadores
2. `maskCNPJ()` — formata com máscara XX.XXX.XXX/XXXX-XX

## Quando usar
- Cadastro/edição de empresas
- Validação antes de submeter formulário
- Formatação para exibição na tela

## Função de Validação

export function isValidCNPJ(cnpj: string): boolean {
  const digits = cnpj.replace(/\D/g, '');

  if (digits.length !== 14) return false;
  if (/^(\d)\1{13}$/.test(digits)) return false; // rejeita "11111111111111"

  let sum = 0;
  let multiplier = 5;

  for (let i = 0; i < 12; i++) {
    sum += parseInt(digits[i]) * multiplier;
    multiplier = multiplier === 2 ? 9 : multiplier - 1;
  }

  const firstDigit = sum % 11 < 2 ? 0 : 11 - (sum % 11);
  if (parseInt(digits[12]) !== firstDigit) return false;

  sum = 0;
  multiplier = 6;

  for (let i = 0; i < 13; i++) {
    sum += parseInt(digits[i]) * multiplier;
    multiplier = multiplier === 2 ? 9 : multiplier - 1;
  }

  const secondDigit = sum % 11 < 2 ? 0 : 11 - (sum % 11);
  return parseInt(digits[13]) === secondDigit;
}

## Função de Máscara

export function maskCNPJ(cnpj: string): string {
  const digits = cnpj.replace(/\D/g, '');
  if (digits.length !== 14) return cnpj;

  return digits.replace(
    /(\d{2})(\d{3})(\d{3})(\d{4})(\d{2})/,
    '$1.$2.$3/$4-$5'
  );
}

## Regras
- Sempre retornar false para CNPJ inválido
- Máscara aplica-se após validação bem-sucedida
- Input pode aceitar com ou sem máscara
- Mostrar erro claro se inválido ("CNPJ inválido")
- Rejeitar sequências repetidas ("11111111111111")
```

</div>

---

## Exercício 2: Criar Skill de CNPJ

**Tarefa**: Refinar a skill de CNPJ ou criar uma versão melhorada.

**Que tal adicionar**:
- [ ] Função para extrair apenas os dígitos
- [ ] Função para remover máscara
- [ ] Casos de teste (CNPJs válidos/inválidos)
- [ ] Tratamento especial (regex, edge cases)

**Critério de aceite**:
- [ ] Skill completa em `skills/skill-cnpj-validation.md`
- [ ] Pronta para ser referenciada em `AGENTS.md`
- [ ] Será usada no Módulo 3 (plano de implementação)

**Próximo passo**: Usar esta skill com Copilot Agent para implementar a feature no projeto!
