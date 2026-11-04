# Respostas da dupla — Atividade PontoCerto

## Dupla

| Papel | Nome completo | Usuário do GitHub |

| Leticia Carvalho(dono do fork) | leticiacarvb

| Suri Savitri(colaborador) | SuriSavitri

## Explicação da solução
A ideia central é tratar a regra da campanha como um valor. Cada regra é uma função Int -> Int guardada em uma variável (pontosEmDobro, bonus50). Por isso existe uma só função de cálculo, calculaPontos, que recebe a regra como argumento e a aplica ao valor da compra. Quando o marketing pede uma campanha nova, não é preciso escrever outra função de cálculo: basta passar outra regra. As fábricas (campanhaMultiplicadora, campanhaBonus) devolvem regras prontas a partir de um número, e acumula combina duas regras aplicando a segunda ao resultado da primeira. O mesmo raciocínio foi levado para C com ponteiros para função.

Co-authored-by: Suri Savitri <ID+SuriSavitri@users.noreply.github.com>

## Desafio 2
Faz sentido usar lambda porque a Promoção Relâmpago e a Quarta Verde duram um dia e são usadas uma única vez. A regra é curta, então escrevê-la direto na chamada evita criar e nomear uma função que nunca mais será usada, e o código fica mais enxuto e fácil de ler.

Co-authored-by: Suri Savitri <ID+SuriSavitri@users.noreply.github.com>

## Desafio 3
campanhaMultiplicadora 5 devolve outra função, não um número. Ela recebeu só o fator n e devolveu uma regra que ainda espera os pontos. O :t campanhaMultiplicadora 5 mostra Int -> Int, tipo de função. Se fosse um número, o :t mostraria Int.

Co-authored-by: Suri Savitri <ID+SuriSavitri@users.noreply.github.com>

## Desafio 4

a) A ordem importa, porque multiplicar e somar não são intercambiáveis. Em acumula blackFriday aniversarioCliente 150: 150 × 5 = 750, depois + 200 = 950. Invertendo: 150 + 200 = 350, depois × 5 = 1750. O bônus entra no meio da multiplicação e acaba multiplicado também.

b) O sistema deve aplicar primeiro a multiplicação e depois o bônus (acumula blackFriday aniversarioCliente). Assim o bônus de 200 é somado no final e não é multiplicado, dando 950 pontos.


Co-authored-by: Suri Savitri <ID+SuriSavitri@users.noreply.github.com>

## Desafio 5 — revisão de código

| Erro | Função | O que estava errado | Como o GHC avisou (resumo da mensagem) | Como corrigimos |

| 1 | aplicaRegraDuasVezes | A assinatura dizia Int -> Int -> Int, mas o primeiro argumento é uma função. Faltaram os parênteses. |Erro de tipo: regra é tratado como Int, mas é aplicado a um argumento ("applied to one value argument, but its type Int has none").|Assinatura (Int -> Int) -> Int -> Int.

| 2 | fimDeSemana |A lambda usava => no lugar de ->. | parse error on input '=>'. | \p -> p * 4.

| 3 | natal | campanhaBonus precisa do valor do bônus. Sem ele, natal ficou com o tipo da fábrica e não com o da regra. | Tipo esperado Int -> Int, mas o real era Int -> Int -> Int.| natal = campanhaBonus 300.

| 4 | promocaoAtual | pontosEmDobro 100 já é o resultado (um Int), mas a assinatura pede uma função. | Tipo esperado Int -> Int, mas o real era Int.| promocaoAtual = pontosEmDobro, sem o 100.


Co-authored-by: Suri Savitri <ID+SuriSavitri@users.noreply.github.com>

## Desafio 6 — Haskell × C

Sintaxe e tipo do parâmetro: em Haskell a regra é um valor comum, com tipo (Int -> Int). Em C é preciso declarar um ponteiro para função, int (*regra)(int), e o nome da função precisa existir antes.
Criação de regras: em Haskell dá para criar a regra na hora com lambda (\p -> p * 3) e fabricar regras com outras funções (campanhaMultiplicadora 5). Em C não existe lambda: toda regra precisa ser uma função nomeada, escrita antes, e não dá para fabricá-la a partir de um número em tempo de execução


Co-authored-by: Suri Savitri <ID+SuriSavitri@users.noreply.github.com>

## Evidência de execução

Saída do `main` de `fidelidade.hs`:

--- Desafio 1 ---

120

240

170

240

--- Desafio 2 ---

80

160

130

240

170

--- Desafio 3 ---

750

350

100

55

--- Desafio 4 ---

950

1750

280


Saída do `main` de `revisao.hs` (depois de corrigido):

40

100

400

200

Saída de `pontocerto.c`:

160

130

300


Co-authored-by: Suri Savitri <ID+SuriSavitri@users.noreply.github.com>
