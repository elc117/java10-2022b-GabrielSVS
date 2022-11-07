# java10-2022b-GabrielSVS

### 1) Execução concorrente - Explicação de resultado incorreto

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

### 2) Indo além

Neste trecho de código abaixo, nunca tinha visto estes nomes de blocos (`try` e `catch`) empregados em um código, e inicialmente, por não conhecer, pareceu ser similar com os blocos if e else.

![Trecho de código](https://imgur.com/gX6iCp5.png)

Pelo que entendi, estes [nomes de blocos](http://www.universidadejava.com.br/java/java-excecoes/) são usados para **tratar erros, sem a necessidade de interromper/aguardar o retorno final do código**, em si. De modo simplificado, o bloco `try` contém o trecho de código onde a exceção *pode ocorrer*, e o bloco `catch` seria o *tratamento, caso ela ocorrer*.
Notei também o objeto que é passado como parâmetro no bloco catch, que é do tipo `Exception`, e além disso, este contém classes filhas, onde vi em alguns [exemplos](https://www.javatpoint.com/try-catch-block) (`InterruptedException`, para Threads / `ArithmeticException`, para aritmética).
Agora, sobre o [método](https://imgur.com/LT6fOQG.png) `printStackTrace()`, ele parece vir da classe `Throwable`, do Java, e é outra ferramenta para localização e tratamento de erros, retornando alguns detalhes com relação ao local onde o erro ocorreu (número da linha, classe), sendo que esses detalhes estão organizados em um [método](https://imgur.com/F4DP54w.png) `toString()`, e também é auxiliada por um método `fillInStackTrace()`, que seu formato depende de como o código for implementado.
