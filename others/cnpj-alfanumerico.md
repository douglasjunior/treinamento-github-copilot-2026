# Objetivo

Gerar um algoritmo de validação de **CNPJ alfanumérico**.

O identificador tem:

- 12 caracteres base alfanuméricos (0–9, A–Z)
- 2 dígitos verificadores numéricos finais (0–9)

A validação deve seguir **módulo 11**, em **duas etapas**, com pesos e mapeamento de caracteres definidos nestas instruções.

---

## Normalização da entrada

1. A função deve receber uma string que representa o CNPJ alfanumérico, possivelmente formatada (por exemplo, com pontos, barra e hífen).
2. Remover qualquer caractere que **não** seja letra (`A–Z` ou `a–z`) ou dígito (`0–9`), preservando apenas letras e dígitos.
3. Converter letras para maiúsculas.
4. Após a normalização, o valor deve ter **exatamente 14 caracteres**:
   - os 12 primeiros são a **base alfanumérica**
   - os 2 últimos são os **dígitos verificadores informados** (que devem ser dígitos de 0 a 9).

Se, após essa etapa, a string não tiver 14 caracteres, a validação deve falhar.

---

## Regras estruturais

Após a normalização:

1. Posições 0 a 11 (12 primeiros caracteres): podem ser letras (`A–Z`) ou dígitos (`0–9`).
2. Posições 12 e 13 (2 últimos caracteres): **devem** ser dígitos (`0–9`), pois são os dígitos verificadores informados.
3. Se algum dos dois últimos caracteres não for dígito, a validação deve falhar.

---

## Mapeamento de caracteres para valor numérico

Para cada caractere que participará do cálculo (tanto na base de 12 caracteres quanto quando o primeiro DV calculado for usado no cálculo do segundo DV), usar a seguinte regra de conversão:

1. Se for um dígito `'0'` a `'9'`:
   - valor numérico = 0 a 9, respectivamente.

2. Se for uma letra maiúscula `'A'` a `'Z'`:
   - `'A'` → 17
   - `'B'` → 18
   - `'C'` → 19
   - ...
   - `'Z'` → 42

   Ou seja, a sequência continua de forma incremental:
   - `'A'` vale 17, `'B'` 18, ..., `'Z'` 42.

3. Uma forma equivalente de implementar isso é:
   - obter o código numérico do caractere (por exemplo, código ASCII)
   - subtrair 48 desse código
   - o resultado é o valor a ser usado no cálculo.

Essa mesma regra é usada tanto para os 12 caracteres base quanto para o primeiro dígito verificador quando ele entra no cálculo do segundo dígito.

---

## Cálculo do primeiro dígito verificador (DV1)

Considere apenas os 12 primeiros caracteres normalizados.

1. Converter cada um dos 12 caracteres para o valor numérico, conforme a regra de mapeamento acima.
2. Associar a cada posição um **peso**, aplicando a sequência de 2 a 9 **da direita para a esquerda**, reiniciando em 2 depois de 9.

   Para 12 caracteres, os pesos, **da esquerda para a direita**, devem ser **exatamente**:

   - `[5, 4, 3, 2, 9, 8, 7, 6, 5, 4, 3, 2]`

3. Multiplicar o valor numérico de cada posição pelo respectivo peso.
4. Somar todos os produtos, obtendo um somatório `S1`.
5. Calcular o resto `R1` da divisão de `S1` por 11 (ou seja, `R1 = S1 mod 11`).
6. Determinar o primeiro dígito verificador (DV1) como:

   - se `R1` for 0 ou 1, então `DV1 = 0`
   - caso contrário, `DV1 = 11 - R1`

---

## Cálculo do segundo dígito verificador (DV2)

Agora, considere os 12 caracteres base **mais** o primeiro dígito verificador calculado (DV1), totalizando 13 posições.

1. Formar uma nova sequência de 13 caracteres:
   - as 12 posições originais da base
   - seguidas do primeiro dígito verificador calculado (DV1), convertido para caractere dígito.

2. Converter cada uma das 13 posições para valor numérico, usando a mesma regra de mapeamento de caracteres descrita acima.

3. Associar a cada posição um **peso**, aplicando a sequência de 2 a 9 da direita para a esquerda, reiniciando em 2 depois de 9.

   Para 13 posições, os pesos, **da esquerda para a direita**, devem ser **exatamente**:

   - `[6, 5, 4, 3, 2, 9, 8, 7, 6, 5, 4, 3, 2]`

4. Multiplicar o valor numérico de cada posição pelo respectivo peso.
5. Somar todos os produtos, obtendo um somatório `S2`.
6. Calcular o resto `R2` da divisão de `S2` por 11 (ou seja, `R2 = S2 mod 11`).
7. Determinar o segundo dígito verificador (DV2) como:

   - se `R2` for 0 ou 1, então `DV2 = 0`
   - caso contrário, `DV2 = 11 - R2`

---

## Regra final de validação

1. A partir da string normalizada de 14 caracteres:
   - base = posições 0 a 11 (12 caracteres)
   - DV informado 1 (DV1_informado) = posição 12
   - DV informado 2 (DV2_informado) = posição 13

2. Calcular `DV1_calculado` usando o método de cálculo do primeiro dígito descrito acima.
3. Calcular `DV2_calculado` usando o método de cálculo do segundo dígito descrito acima.
4. Comparar:

   - `DV1_calculado` deve ser igual ao `DV1_informado`;
   - `DV2_calculado` deve ser igual ao `DV2_informado`.

5. O CNPJ alfanumérico é considerado **válido** somente se **ambos** os dígitos calculados coincidirem com os dígitos informados.

---

## Exemplo completo que deve bater com a implementação

Considere a base (12 caracteres):

- `1 2 A B C 3 4 5 0 1 D E`

1. Converta para valores numéricos:

   - `1 → 1`
   - `2 → 2`
   - `A → 17`
   - `B → 18`
   - `C → 19`
   - `3 → 3`
   - `4 → 4`
   - `5 → 5`
   - `0 → 0`
   - `1 → 1`
   - `D → 20`
   - `E → 21`

   Fica: `[1, 2, 17, 18, 19, 3, 4, 5, 0, 1, 20, 21]`

2. Pesos para o primeiro dígito (da esquerda para a direita):

   - `[5, 4, 3, 2, 9, 8, 7, 6, 5, 4, 3, 2]`

3. Produtos e somatório para o primeiro dígito:

   - `1 * 5  = 5`
   - `2 * 4  = 8`
   - `17 * 3 = 51`
   - `18 * 2 = 36`
   - `19 * 9 = 171`
   - `3 * 8  = 24`
   - `4 * 7  = 28`
   - `5 * 6  = 30`
   - `0 * 5  = 0`
   - `1 * 4  = 4`
   - `20 * 3 = 60`
   - `21 * 2 = 42`

   Somatório `S1 = 5 + 8 + 51 + 36 + 171 + 24 + 28 + 30 + 0 + 4 + 60 + 42 = 459`

4. Resto e DV1:

   - `R1 = 459 mod 11 = 8`
   - `DV1 = 11 - 8 = 3` (como `R1` não é 0 nem 1)

5. Sequência de 13 caracteres para o segundo dígito:

   - `1 2 A B C 3 4 5 0 1 D E 3`

6. Valores numéricos correspondentes:

   - `1 → 1`
   - `2 → 2`
   - `A → 17`
   - `B → 18`
   - `C → 19`
   - `3 → 3`
   - `4 → 4`
   - `5 → 5`
   - `0 → 0`
   - `1 → 1`
   - `D → 20`
   - `E → 21`
   - `3 → 3`

   Fica: `[1, 2, 17, 18, 19, 3, 4, 5, 0, 1, 20, 21, 3]`

7. Pesos para o segundo dígito (da esquerda para a direita):

   - `[6, 5, 4, 3, 2, 9, 8, 7, 6, 5, 4, 3, 2]`

8. Produtos e somatório para o segundo dígito:

   - `1 * 6  = 6`
   - `2 * 5  = 10`
   - `17 * 4 = 68`
   - `18 * 3 = 54`
   - `19 * 2 = 38`
   - `3 * 9  = 27`
   - `4 * 8  = 32`
   - `5 * 7  = 35`
   - `0 * 6  = 0`
   - `1 * 5  = 5`
   - `20 * 4 = 80`
   - `21 * 3 = 63`
   - `3 * 2  = 6`

   Somatório `S2 = 6 + 10 + 68 + 54 + 38 + 27 + 32 + 35 + 0 + 5 + 80 + 63 + 6 = 424`

9. Resto e DV2:

   - `R2 = 424 mod 11 = 6`
   - `DV2 = 11 - 6 = 5` (como `R2` não é 0 nem 1)

10. Assim, o CNPJ alfanumérico com base `12ABC34501DE` e dígitos verificadores `3` e `5` é **válido**.
    Um formato possível para exibição é `12.ABC.345/01DE-35`, mas a validação deve ser feita sobre a forma normalizada sem pontuação.

## Máscara de formatação recomendada

Use estas máscaras apenas para **exibição**; a validação deve sempre trabalhar com a string normalizada (somente letras e dígitos, sem pontuação).

1. **Entrada livre com formatação opcional**

   - Permitir o usuário digitar livremente letras (`A–Z`, `a–z`) e dígitos (`0–9`), ignorando (ou inserindo automaticamente) os caracteres de máscara.
   - Ao exibir, aplicar a máscara padrão abaixo.

2. **Máscara padrão (14 caracteres, incluindo DV)**

   Considerando a sequência normalizada `BBBBBBBBBBBBDD` (B = base alfanumérica, D = dígito verificador numérico):

   - Padrão visual recomendado:
     - `BB.BBB.BBB/BBBD-DD`
   - Mapeamento de posições (índices da string normalizada de 0 a 13):
     - posição 0  → B0
     - posição 1  → B1
     - ponto `.`
     - posição 2  → B2
     - posição 3  → B3
     - posição 4  → B4
     - ponto `.`
     - posição 5  → B5
     - posição 6  → B6
     - posição 7  → B7
     - barra `/`
     - posição 8  → B8
     - posição 9  → B9
     - posição 10 → B10
     - posição 11 → B11
     - hífen `-`
     - posição 12 → D0
     - posição 13 → D1

   Exemplo com base alfanumérica e DV:

   - Normalizado: `12ABC34501DE35`
   - Exibido: `12.ABC.345/01DE-35`

3. **Comportamento em campos de digitação**

   - Pode-se aplicar a máscara progressivamente conforme o usuário digita:
     - insere automaticamente `.` após o 2º e 5º caracteres base
     - insere `/` após o 8º caractere base
     - insere `-` após o 12º caractere (quando iniciar os DVs)
   - Internamente, remover todos os caracteres não alfanuméricos antes de enviar para a função de validação.

4. **Validação da máscara (opcional, além da validação dos DVs)**

   - Aceitar:
     - string já formatada na forma `BB.BBB.BBB/BBBD-DD`
     - ou string sem máscara, com 14 caracteres alfanuméricos
   - Rejeitar:
     - strings com caracteres inválidos (que não sejam letras ou dígitos, desconsiderando os separadores `.`, `/`, `-`)
     - strings cuja forma formatada não respeite as posições dos separadores indicadas acima.
