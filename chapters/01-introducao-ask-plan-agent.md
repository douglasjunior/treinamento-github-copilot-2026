---
layout: center
---

# Introdução e nivelamento

---

## Modos de Interação com Agentes de Código

- **Ask**: explorar ideias, entender código existente e levantar alternativas antes de decidir o que fazer.
  - Exemplo: "Explique este trecho e sugira melhorias de legibilidade."
  - Exemplo: "Quais são os riscos de refatorar este service agora?"
  - Exemplo: "Compare esta abordagem com uma implementação usando interceptor."

<v-clicks>

- **Plan**: estruturar a implementação em etapas, dependências e critérios de aceite antes de escrever código.
  - Exemplo: "Crie um plano para adicionar validação e máscara de CNPJ sem quebrar o formulário."
  - Exemplo: "Divida a migração para autenticação OAuth em entregas pequenas e seguras."
  - Exemplo: "Monte um plano de refatoração com foco em reduzir risco e preservar cobertura de testes."

- **Agent**: executar alterações no repositório, editar arquivos, ajustar testes e validar o resultado.
  - Exemplo: "Implemente o plano aprovado e atualize os testes afetados."
  - Exemplo: "Crie o service, o controller e os testes seguindo o padrão deste repositório."
  - Exemplo: "Aplique a refatoração combinada e rode a suíte relevante para validar."

</v-clicks>
