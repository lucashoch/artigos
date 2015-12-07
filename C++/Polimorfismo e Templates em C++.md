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

  É através dos métodos virtuais que realmente acontece a magia do *Polimorfismo* no C++.<br>
  Métodos virtuais são como placas de sinalização, que indicam ao *Compilador* que, *possivelmente*, haja um método com a mesma assinatura em uma das classes derivadas.<br>
  <br>
  Dessa forma, para praticarmos *Polimorfismo* basta declarar o método da classe **base** como virtual e "sobrecarregá-lo" na classe derivada, da seguinte forma:

    class ClasseBase{
     private:
        string nome = "Classe Base";
     public:
        ClasseBase(){};//construtor padrão
        virtual ~ClasseBase(){};
        virtual void mostraNome(){
            cout << nome << endl;
        }
    };

    class ClasseDerivada : public ClasseBase{
      public:
        void mostraNome(){
            cout << "Estamos praticando Polimorfismo" << endl;
        }
    };

    int main(){
       ClasseBase t1;
       ClasseBase *t2;
       ClasseDerivada t3;
       t2 = &t3;
       t1.mostraNome(); //Resultado : Classe Base
       t2->mostraNome(); //Resultado : Estamos aprendendo Polimorfismo

       return 0;
    }

  Observe que t1 e t2 são do mesmo tipo *ClasseBase* e chamam a mesma função *mostraNome()*, mas apresentam resultados diferentes, pelo fato de t2 ser ponteiro e apontar para um objeto do tipo *ClasseDerivada*.<br>

  Como vimos acima, para acerssarmos nossos métodos polimórficos, basta criarmos um ponteiro da classe **base** e apontarmos este para as classes **derivadas** que queremos acessar.<br>
  Esta tática de programação faz com que a chamada das funções seja feita dinâmicamente pelo compilador (durante a execução do programa e não durante a compilação) e torna muito mais fácil acessar diversos métodos de diversas classes, basta fazer um laço de repetição, onde o ponteiro da classe **base** aponta para diferentes classes **derivadas** durante a execução do laço.

  Repare que o construtor de *ClasseBase* também é virtual, isto acontece pois, por via de regra, quando temos um método virtual em uma classe, seu construtor também deve ser.

### Métodos Virtais Puros

  Métodos Virtuais Puros carregam os mesmos conceitos dos métodos virtuais vistos acima, entretanto possui suas peculiaridades.<br>
  Quando falamos sobre métodos virtuais puros, estamos falando sobre *classes abstratas*, ou seja, classes que não podem ter seus objetos instanciados, não possuem construtor e seus métodos são definidos pelas suas *classes derivadas*.<br>
  No começo é um pouco difícil entender mesmo, mas logo pegamos o jeito. Basicamente, as *classes abstratas* são apenas cabeçalhos de métodos virtuais puros que serão definidos nas *classes derivadas*.<br>
  <br>
  Para construirmos nossos novos métodos virtuais puros, basta fazer igual aos métodos que vimos acima e igualarmos o método à zero, da seguinte forma:

    class Exemplo{ // classe abstrata
      public:
        virtual void mostraNome() = 0; // método virtual puro
    };

  Como a classe não possui construtor, não pode ter objetos instanciados, e as classes abstratas nem precisam ter seus objetos diretamente instanciados.<br>
  Por trás das cortinas, o compilador está sendo "enganado" para acreditar que os métodos virtuais puros existam durante a compilação mas na verdade eles estão sendo definidos em tempo de execução, já que para cada *classe derivada* teremos um método diferente.

### Exemplo

    #include <iostream>

    using namespace std;

    class Funcionario{// classe abstrata
        public:
            virtual float calculaSalario() = 0;// método virtual puro
    };

    class Vendedor : public Funcionario{
        private:
            string nome;
            float salario;
            int nVendas; // número de vendas
        public:
            Vendedor(string, float, int);

            void setSalario(float);// salário fixo
            void setNome(string);
            void setVendas(int);

            string getNome() const;
            float getSalario() const;
            int getVendas() const;

            float calculaSalario(); // calcula salário final baseado no número de vendas + salário fixo
    };

    Vendedor::Vendedor(string nome, float salario, int vendas){
        setNome(nome);
        setVendas(vendas);
        setSalario(salario);
    }

    float Vendedor::calculaSalario(){// calcula salario de vendedor (polimorfismo com virtual puro)
        return (getSalario()+(getSalario()*0.005*getVendas()));
    }

    void Vendedor::setSalario(float s){
        if(s >= 0){
            salario = s;
        }
        else{
            salario = 800.00;
        }
    }

    void Vendedor::setNome( string n){
        nome = n;
    }

    void Vendedor::setVendas(int n){
        if(n >= 0){
            nVendas = n;
        }
        else{
            nVendas = 0;
        }
    }

    string Vendedor::getNome() const{
        return nome;
    }
    float Vendedor::getSalario() const{
        return salario;
    }
    int Vendedor::getVendas() const{
        return nVendas;
    }

    int main()
    {
        Funcionario *f1;
        Vendedor v1("Polimórfico", 1000.00, 100);
        f1 = &v1;
        cout << f1->calculaSalario() << endl;

        return 0;
    }

E dessa forma podemos pensar em classes como Gerente, Programador, Entregador, etc. Cada uma com seu método *calculaSalario()* particular.

## Templates



## Referências Bibliográficas

[Polimorfismo.pdf](https://www.dimap.ufrn.br/~adilson/DIm327/Polimorfismo.pdf) - Por Adilson Lopes. Acesso em 6 de Dezembro de 2015.
