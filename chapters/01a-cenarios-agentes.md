## Cenários de Aplicação de Agentes de código

<div :class="{ 'dynamic-hidden': $slidev.nav.clicks >= 4 }" class="dynamic-section">

**Exploração & Análise**

<v-clicks>

- Entender a base de código: padrões, tecnologias, convenções
- Medir esforço de implementação: pontos de impacto (ex: multi-tenant)
- Validar solução técnica: comparar opções, prós/contras e custo-benefício

**Código & Qualidade**
- Pagar dívida técnica: sonar issues, refatoração, atualização
- Gerar testes: TDD (antes) ou cobertura (depois)
- Análise de segurança: vulnerabilidades, padrões inseguros
- Otimização de performance: gargalos, melhorias

</v-clicks>

</div>

<div :class="{ 'dynamic-hidden': $slidev.nav.clicks < 4 }" class="dynamic-section">

<v-clicks>

**Documentação & Onboarding**
- Gerar e atualizar documentação: sincronizar com código
- Onboarding: guias, exemplos, documentação contextualizada
- Code review: revisar PRs, sugerir padrões

> 🎁 Copie [este prompt](https://gist.githubusercontent.com/douglasjunior/26d717084811869e593215b8312876e8/raw/86a57d8080bb79543b454c9bb95c1ad036265038/code-review-prompt.md) no seu agente para revisão de PRs.

**Automação & Manutenção**
- Gerar arquivos de instruções e skills
- Migração de código: atualizar dependências, padrões
- Geração de tipos/interfaces: TypeScript, GraphQL, a partir de exemplos de código e JSON existentes
- Debugging: investigação colaborativa de bugs

</v-clicks>

</div>
