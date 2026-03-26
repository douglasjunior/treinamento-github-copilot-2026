## Introdução ao Modo Ask

- Permite que você faça perguntas em linguagem natural diretamente ao Copilot (por exemplo: "Explique essa função", "Como usar o useEffect do React?", "Como corrigir esse erro?").
- Funciona como uma janela de chat ou caixa de diálogo dentro do editor.
O Copilot responde com explicações, exemplos, sugestões de boas práticas, links e orientações detalhadas.
- Pode ser usado para dúvidas sobre o código atual, conceitos de programação, frameworks, bibliotecas, erros e até dúvidas sobre o próprio GitHub.
- Ideal para aprender, tirar dúvidas rápidas ou aprofundar o entendimento sem sair do editor de código.

---

## Criando Prompts Eficazes

- Seja específico e claro ao fazer perguntas.
- Forneça contexto quando necessário.
- Exemplo: "Como validar um email em Spring Boot?".

<v-click>

**Curso Uni421:** [Conceitos Fundamentais de GenAI, LLMs e Prompt Engineering](https://db1.uni421.com.br/lms/#/aprendizagem/catalogo/infos_gerais/?idmatricula=0&secao=213&idcatalogo=2&idcurso=202)

</v-click>

---

## Exemplo em Java - Validação de Entrada

<style>
.small {
  transform: scale(0.1);
  margin: -190px 0;
  transition: transform,margin 0.3s ease;
}
</style>

<div :class="{ small: $slidev.nav.clicks >= 6 }">

> **Prompt**: Implementar validação de email para a entidade User

```java {1-2,6-7|4-5|all}
public class User {
    private String name;

    @Email
    private String email;

    // Construtor, getters e setters
}
```

<br />

> **Prompt**: Implemente no UserController uma rota para cadastro de User com validação

```java {0|1-2,9|4-8|all}
public class UserController {
    // Injeção do service e construtor omitidos

    @PostMapping()
    public ResponseEntity<User> createUser(@Valid @RequestBody User user) {
        userService.save(user);
        return ResponseEntity.status(HttpStatus.CREATED).body(user);
    }
}
```

</div>

<div v-click="6">

**Passos Práticos**:
1. Navege até a classe `User.java` no seu editor
1. Use o Modo Ask para solicitar a implementação de uma validação de email
    > **Prompt**: Implementar validação de email para a entidade User
1. Esperamos que seja adicionado a propriedade `email` na classe `User`, bem como a anotação `@Email`, atualização do construtor e métodos `get` e `set`
1. Navegue até a classe `UserController.java`
1. Use o Modo Ask para solicitar a implementação de uma rota de cadastro de `User` com validação
    > **Prompt**: Implemente no UserController uma rota para cadastro de User com validação
1. Esperamos que seja adicionado o método `createUser` na classe `UserController`, bem como a anotação `@PostMapping` e o uso do `UserService` para salvar o usuário

</div>

---

## Exemplo em Angular - Serviço para API

<style>
.small {
  transform: scale(0.4);
  margin: -90px 0;
  transition: transform,margin 0.3s ease;
}
</style>

<div :class="{ small: $slidev.nav.clicks >= 3 }">

> **Prompt**: Criar um serviço para buscar usuários de uma API no endereço "https://jsonplaceholder.typicode.com/users"

```typescript {1,5-8,15|2-3,10-14|all}
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';

@Injectable({
  providedIn: 'root'
})
export class UserService {

  constructor(private http: HttpClient) { }

  getUsers(): Observable<any> {
    return this.http.get('https://jsonplaceholder.typicode.com/users');
  }
}
```

</div>

<div v-click="3">

**Passos Práticos**:
1. Gere service com `ng generate service user`
1. Navegue até o arquivo `user.service.ts`
1. Use o Modo Ask para solicitar a criação de um serviço que busque usuários de uma API
    > **Prompt**: Criar um serviço para buscar usuários de uma API no endereço "https://jsonplaceholder.typicode.com/users"
1. Esperamos que seja adicionado o método `getUsers` no serviço, utilizando o `HttpClient` do Angular para fazer uma requisição GET para `https://jsonplaceholder.typicode.com/users`
1. Copie o código gerado para o arquivo `user.service.ts`

</div>

---

## Exemplo em Angular - Consumindo o Serviço no Componente

<style>
.small {
  transform: scale(0.3);
  margin: -155px 0;
  transition: transform,margin 0.3s ease;
}
</style>

<div :class="{ small: $slidev.nav.clicks >= 3 }">

> **Prompt**: Consuma no UserListComponent o UserService para listar os usuários

````md magic-move

```typescript {*}
import { CommonModule } from '@angular/common';
import { Component } from '@angular/core';

@Component({
  imports: [CommonModule],
  selector: 'app-user-list',
  template:  `
  <ul>
    <li *ngFor="let user of users">{{ user.name }}</li>
  </ul>
  `,
})
export class UserListComponent {
  users = [
    { name: 'Alice' },
    { name: 'Bob' },
    { name: 'Charlie' }
  ];
}
```

```typescript {3,15-21|all}
import { CommonModule } from '@angular/common';
import { Component, OnInit } from '@angular/core';
import { UserService } from '../user.service';

@Component({
  imports: [CommonModule],
  selector: 'app-user-list',
  template:  `
  <ul>
    <li *ngFor="let user of users">{{ user.name }}</li>
  </ul>
  `,
})
export class UserListComponent implements OnInit {
  users: any[] = [];
  constructor(private userService: UserService) {}
  ngOnInit() {
    this.userService.getUsers().subscribe((data: any[]) => {
      this.users = data;
    });
  }
}
```
````

</div>

<div v-click="3">

**Passos Práticos**:
1. Navegue até o arquivo `user-list.component.ts`
1. Use o Modo Ask para solicitar a modificação do `UserListComponent` para que consuma o `UserService` para listar os usuários
    > **Prompt**: Consuma no UserListComponent o UserService para listar os usuários
1. Esperamos que seja adicionado o método `ngOnInit` no componente, que chama o `UserService` para buscar os usuários
1. Copie o código gerado para o arquivo `user-list.component.ts`

</div>

---

## Casos de Uso para o Modo Ask

- Pedir explicações de trechos de código desconhecidos ou complexos ("O que essa função faz?").

<v-clicks>

- Solicitar exemplos de uso de bibliotecas, funções ou APIs ("Como uso fetch para fazer uma requisição GET?").
- Obter sugestões de melhores práticas de programação para determinado contexto ("Qual a melhor forma de tratar erros em JavaScript?").
- Tirar dúvidas sobre sintaxe ou recursos de uma linguagem ("Como funciona o destructuring em JavaScript?", "Como criar uma classe em Python?").
- Pedir ajuda para entender mensagens de erro ("O que significa esse erro TypeError: undefined is not a function?").

</v-clicks>

---

## Mais Casos de Uso para o Modo Ask

- Buscar explicações sobre padrões de projeto ("Explique o padrão Singleton.").

<v-clicks>

- Obter referências para documentação oficial ou materiais de estudo ("Onde encontro a documentação do React Router?").
- Solicitar dicas para otimização de código ou refatoração ("Como posso melhorar a performance desse código?").
- Pedir ajuda na configuração de ferramentas ou ambientes ("Como configuro ESLint para um projeto React?").
- Perguntar sobre integração entre tecnologias ("Como conectar meu backend Node.js a um banco MongoDB?").

</v-clicks>
