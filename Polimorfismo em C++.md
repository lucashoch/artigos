# Polimorfismo e Templates em C++
**autor: [André Rocha](http://github.com/andrecgro)**

## Polimorfismo

### Definição

  Polimorfismo, no campo das linguagens de programação, é a capacidade de um determinado objeto se comportar de forma diferente, dada uma ou mais característica e um ambiente que esteja situado. Ou seja, funções de mesmo nome podem desempenhar papéis diferentes para classes diferentes, mas correlacionadas através de conceito de *herança*.

### Conceito

  A utilização do Polimorfismo torna mais fácil, e prática, a forma de tratar métodos com a mesma assinatura (nome+argumentos) para classes bases e derivadas. <br>Podemos pensar que uma determinada classe base *Funcionário* possui um método *calcularSalario()* e é herdada pelas classes *Gerente* e *Vendedor*.
  Seguindo o raciocínio, é fácil imaginar que, mesmo sendo ambos funcionários, o método de calcular o salário de um Gerente pode diferir do método de calcular o salário de um Vendedor.
  <br>
  Logo, o Polimorfismo proporciona a intrigante maneira de permitir que exista um método diferente para cada classe e chamá-lo de maneira simples, através de um ponteiro da classe base.

### Métodos Virtuais

  É através dos métodos virtuais que realmente acontece a magia do *Polimorfismo* no C++.
  Métodos virtuais são como placas de sinalização, que indicam ao *Compilador* que, *possivelmente*, haja um método com a mesma assinatura em uma das classes derivadas.

### Métodos Virtais Puros

### Exemplo

## Templates

## Referências Bibliográficas

[Polimorfismo.pdf](https://www.dimap.ufrn.br/~adilson/DIm327/Polimorfismo.pdf) - Por Adilson Lopes. Acesso em 6 de Dezembro de 2015.