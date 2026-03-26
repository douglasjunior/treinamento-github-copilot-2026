## Introdução ao Modo Agent

- O Modo Agent permite que o Copilot atue como um "agente" autônomo, que entende objetivos maiores e executa passos para atingi-los.
- O agente pode, por exemplo: analisar um problema, propor mudanças, criar ou editar múltiplos arquivos, gerar pull requests, rodar testes, revisar código e até sugerir melhorias de arquitetura.
- Ele funciona realizando ações no projeto, muitas vezes de forma iterativa: ele sugere, executa, valida e ajusta até completar a tarefa solicitada.

---

## Como o Modo Agent se diferencia dos outros recursos do Copilot?

- **Autocomplete**:

Sugere automaticamente linhas ou blocos de código enquanto você digita, de forma passiva, sem executar ações diretas no projeto.

- **Modo Ask**:

Permite conversar com o Copilot, fazendo perguntas e recebendo respostas, exemplos ou explicações. Atua como um assistente de dúvidas e aprendizado.

- **Modo Agent**:

Atua de forma proativa e autônoma, executando tarefas completas, como refatorar código, corrigir bugs, implementar funcionalidades ou automatizar etapas do fluxo de trabalho.

---

## Exemplo de Refatoração

**Antes**:

::code-group

```java [Java]
public class ExemploMalEscrito {
    public static void main(String[] args) {
        int[] numeros = new int[10];
        for (int i = 0; i < 10; i++) {
            numeros[i] = i + 1;
        }
        for (int i = 0; i < 10; i++) {
            if (numeros[i] % 2 == 0) {
                System.out.println("O número " + numeros[i] + " é par");
            } else {
                System.out.println("O número " + numeros[i] + " não é par");
            }
        }
        int soma = 0;
        for (int i = 0; i < 10; i++) {
            soma = soma + numeros[i];
        }
        System.out.println("A soma é " + soma);
    }
}
```

```typescript [TypeScript]
function exemploMalEscrito() {
  let numeros = [];
  for (let i = 0; i < 10; i++) {
    numeros[i] = i + 1;
  }
  for (let i = 0; i < 10; i++) {
    if (numeros[i] % 2 === 0) {
      console.log("O número " + numeros[i] + " é par");
    } else {
      console.log("O número " + numeros[i] + " não é par");
    }
  }
  let soma = 0;
  for (let i = 0; i < 10; i++) {
    soma = soma + numeros[i];
  }
  console.log("A soma é " + soma);
}

exemploMalEscrito();
```

::

---
layout: center
---

## Exemplo de Refatoração

<br>

> **Prompt**: Refatore este código para torná-lo mais limpo, legível e eficiente.

> Use boas práticas da linguagem, evite repetições, quebre em funções menores quando possível e utilize recursos modernos disponíveis.

---

## Exemplo de Refatoração

**Depois**:

::code-group

```java [Java]
public class ExemploRefatorado {
    public static void main(String[] args) {
        int[] numeros = criarArraySequencial(1, 10);
        imprimirParidade(numeros);
        int soma = Arrays.stream(numeros).sum();
        System.out.println("A soma é " + soma);
    }

    private static int[] criarArraySequencial(int inicio, int tamanho) {
        return java.util.stream.IntStream.range(inicio, inicio + tamanho).toArray();
    }

    private static void imprimirParidade(int[] numeros) {
        for (int numero : numeros) {
            String paridade = (numero % 2 == 0) ? "par" : "não é par";
            System.out.println("O número " + numero + " " + paridade);
        }
    }
}
```

```typescript [TypeScript]
function criarArraySequencial(inicio: number, tamanho: number): number[] {
    return Array.from({ length: tamanho }, (_, i) => inicio + i);
}

function imprimirParidade(numeros: number[]): void {
    numeros.forEach(numero => {
        const paridade = numero % 2 === 0 ? "par" : "não é par";
        console.log(`O número ${numero} ${paridade}`);
    });
}

function exemploRefatorado(): void {
    const numeros = criarArraySequencial(1, 10);
    imprimirParidade(numeros);
    const soma = numeros.reduce((acc, curr) => acc + curr, 0);
    console.log(`A soma é ${soma}`);
}

exemploRefatorado();
```

::

---

## Melhores Práticas para o Modo Agent

- Forneça instruções detalhadas ao agente.
- Revise e teste o código gerado.
- Use para tarefas maiores, não apenas *completions*.
- Combine com o Modo Ask para esclarecer dúvidas durante o processo.
- Use o Modo Agent para tarefas complexas, como refatoração de código legado, implementação de novas funcionalidades ou integração de sistemas.
