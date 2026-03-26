## Modo Agent com Código Legado

- Uso do Modo Agent para melhorar código antigo.
- Geração de documentação e refatoração de componentes complexos.

---

## Trabalhando com Código Legado - Exemplos

<style>
.small {
  transform: scale(0.7);
  margin: -10px 0;
  transition: transform,margin 0.3s ease;
}
</style>

<div :class="{ small: $slidev.nav.clicks >= 1 }">

**Passos Práticos**:

1. Abra um projeto real em que você trabalhe.
1. Navegue até uma classe ou componente complexo.
1. Use o prompt para solicitar uma explicação detalhada sobre a classe e suas dependências.

</div>

<div v-click="1">

**Prompts**:

- "Explique o funcionamento desta classe como se fosse para um desenvolvedor júnior"
- "Quais são as dependências desta classe e como elas interagem?"
- "Gere um diagrama de sequência para o fluxo ABCD da classe XYZ"
- "Refatore a classe XYZ para dividir a responsabilidade A e B em múltiplos serviços e implemente o padrão port and adapter para acesso ao banco de dados"
- "Refatore o componente XYZ para melhorar o modo `standalone` do Angular"
- "Modifique as propriedades do componente ABC para trabalhar com `input()` em vez de `@Input`
- "Refatore a classe/componente para tornar o código testável, em seguida, gere testes unitários para a classe/componente"

</div>

---

## Boas Práticas

**✅ Sempre faça:**
- Revise cuidadosamente o código gerado antes de usar.
- Teste todas as funcionalidades implementadas.
- Avalie possíveis riscos de segurança no código sugerido.
- **Certifique-se de compreender o código antes de integrá-lo.**

**❌ Evite:**
- Aceitar código sem revisão crítica.
- Utilizar IA para processar dados sensíveis ou confidenciais.
- Depender exclusivamente das sugestões da IA.
- Ignorar padrões e práticas recomendadas do projeto.
