## Introdução ao Autocomplete

- À medida que você digita, o Copilot analisa o contexto do seu código e exibe sugestões inline, geralmente em cinza claro.
- Você pode aceitar a sugestão pressionando Tab ou uma tecla específica do seu editor.
O Copilot pode sugerir desde nomes de variáveis até funções completas, loops, estruturas condicionais e até testes unitários.
- O Autocomplete do Copilot vai além do autocomplete tradicional dos editores, pois usa inteligência artificial treinada em bilhões de linhas de código, tornando as sugestões mais inteligentes e adaptadas ao contexto.

---

## Usando o Autocomplete no VSCode

- Ative a extensão do Copilot.
- Comece a digitar e aceite sugestões com a tecla Tab.

<br>

## Usando o Autocomplete no IntelliJ

- Instale o plugin do Copilot.
- Utilize as sugestões enquanto codifica.

---

## Exemplo em Java - Endpoint REST

> Digite na ordem sugerida para ver o Copilot em ação.

<style>
.small {
  transform: scale(0.6);
  margin-bottom: -50px;
  margin-top: -50px;
  transition: transform,margin 0.3s ease;
}
</style>

<div :class="{ small: $slidev.nav.clicks >= 7 }">

```java {3,16|1-2|5|7-9|11|12-14|all}
@RestController
@RequestMapping("/users")
public class UserController {

    private final UserService userService;

    public UserController(UserService userService) {
        this.userService = userService;
    }

    @GetMapping()
    public ResponseEntity<List<User>> getAllUsers() {
        return ResponseEntity.ok(userService.getAllUsers());
    }
}
```
</div>

<div v-click="7">

**Passos Práticos**:
1. Crie `UserController.java`
1. Implemente a rota de listagem de usuários usando sugestões do Copilot
1. Rode com `./gradlew :bootRun` e teste via curl ou postman.

</div>

---

## Exemplo em Angular - Componente

<style>
.small {
  transform: scale(0.5);
  margin-bottom: -70px;
  margin-top: -70px;
  transition: transform,margin 0.3s ease;
}
</style>

<div :class="{ small: $slidev.nav.clicks >= 5 }">

> Digite na ordem sugerida para ver o Copilot em ação.

```typescript {1,4,5,12,13,19|2,6|7-11|14-18|all}
import { Component } from '@angular/core';
import { CommonModule } from '@angular/common';

@Component({
  selector: 'app-user-list',
  imports: [CommonModule],
  template: `
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

</div>

<div v-click="5">

**Passos Práticos**:
1. Gere componente com `ng generate component user-list`
1. Implemente uma lista de usuários usando sugestões do Copilot
1. Adicione o componente ao módulo principal (`app.component.ts` e `app.component.html`)
1. Rode com `ng serve`

</div>

---

## Dicas para Uso Eficaz do Autocomplete

**Dicas**

- Escreva comentários claros para orientar as sugestões.
- Use nomes de variáveis e funções significativos.
- Aceite sugestões seletivamente, verificando a lógica.


<v-click>

<br>

**Limitações**

- Pode sugerir código incorreto ou inseguro.
- Não substitui o entendimento do código.
- Requer verificação e testes adicionais.

</v-click>
