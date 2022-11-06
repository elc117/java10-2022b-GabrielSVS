# java10-2022b-GabrielSVS
java10-2022b-GabrielSVS created by GitHub Classroom

### Execução concorrente - Explicação de resultado incorreto

Para o exemplo, utilizei o código da pasta **sharedaccount**, removendo o *synchronized* dos métodos que o continha. Iniciei o saldo em *100*. O depósito é feito *duas vezes (incrementando 100)*, e a retirada, *uma vez
(decrementando 50)*.

![Execução concorrente com resultado incompleto](https://imgur.com/6HYJEoT.png)

Considerando o exemplo de resultado incorreto para o código sharedaccount, estão separadas em três operações principais:
```
- Carregar: Obter o saldo inicial;
- Manipular: Incrementar +100, ou decrementar -50 do saldo obtido;
- Armazenar: Retornar o saldo alterado;
```
Pela execução acima, entendi que a Thread envolvendo o incremento foi terminada primeiro. Porém, como a Thread do decremento
terminou posteriormente, esta acabou **_sobrescrevendo_** o saldo anteriormente armazenado.

![Diagrama ilustrando a execução do código](https://imgur.com/Z6lW43c.png)
