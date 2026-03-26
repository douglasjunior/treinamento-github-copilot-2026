## Cenários de Aplicação de Agentes

<style>
.section {
  transition: opacity 0.3s ease;
}
.hidden {
  opacity: 0;
  pointer-events: none;
  height: 0;
}
</style>

<div :class="{ hidden: $slidev.nav.clicks >= 5 }" class="section">

<v-clicks>

**Exploração & Análise**
- Entender a base de código: padrões, tecnologias, convenções
- Medir esforço de implementação: pontos de impacto (ex: multi-tenant)
- Validar solução técnica: comparar opções, prós/contras

**Código & Qualidade**
- Pagar dívida técnica: sonar issues, refatoração, atualização
- Gerar testes: TDD (antes) ou cobertura (depois)
- Análise de segurança: vulnerabilidades, padrões inseguros
- Otimização de performance: gargalos, melhorias

</v-clicks>

</div>

<div :class="{ hidden: $slidev.nav.clicks < 5 }" class="section">

<v-clicks>

**Documentação & Onboarding**
- Gerar e atualizar documentação: sincronizar com código
- Onboarding: guias, exemplos, documentação contextualizada
- Code review: revisar PRs, sugerir padrões

**Automação & Manutenção**
- Gerar arquivos de instruções e skills
- Migração de código: atualizar dependências, padrões
- Geração de tipos/interfaces: TypeScript, GraphQL
- Debugging: investigação colaborativa de bugs

</v-clicks>

</div>
