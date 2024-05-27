
#### Seleção

`σ<Condição>(Tabela)`
#### Projeção
`π<Lista de Atributos>(Tabela)`

#### Produto cartesiano

`Tabela1 × Tabela2`

- Combina todos os valores (Evitar utilização)

#### Atribuição e Otimização

- `variávelNome := expressão`
    - Filtragens o mais cedo possível
    - Identificar expressões comuns que podem ser utilizadas múltiplas vezes

#### Renomeação

`ρ(B, C) (Tabela) => Tabela x pz (Tabela)`

#### União, diferença e interseção

- Somente para duas tabelas compatíveis (mesmo grau e colunas com mesmo tipo)
    - União: `Tabela1 ∪ Tabela2` => Junta tabelas
    - Diferença: `Tabela1 - Tabela2` => Tabela1 sem itens da Tabela2
    - Interseção: `Tabela1 ∩ Tabela2` => O que tem em comum

### Junção

`Tabela1 ⋈<condição> Tabela2`

- **Natural Join:** ⋈ considera todos os atributos
- **Left Join:** ⟕ Tudo em comum e da Tabela da esquerda
- **Right Join:** ⟖ Tudo em comum e da Tabela da direita
- **Full Join:** ⟗ Tudo em comum e dos dois lados

### Divisão

`Tabela1 ÷ Tabela2`

Traz os campos remanescentes de Tabela1 quando há match com os campos de Tabela2.

Tabela 1

| x   | y   | z   |
| --- | --- | --- |
| 1   | 1   | 1   |
| 1   | 2   | 2   |
| 2   | 1   | 1   |
| 3   | 1   | 3   |
| 3   | 3   | 1   |
Tabela 2
z
1

Resultado
x y
1 1
2 1
3 3
### Atualização de Tabelas

`δ[Atributo := Expressão](Tabela)`