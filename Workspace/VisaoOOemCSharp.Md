# Orientacao a objetos

## C# Orientado a Objetos: Introdução

Neste artigo será apresentado uma introdução a orientação a objetos de uma forma geral em CSharp, em seguida colocaremos em prática os conhecimentos teóricos adquiridos para a linguagem de programação C#.

.NET
### C# Orientado a Objetos: Introdução

A orientação a objetos é uma ponte entre o mundo real e virtual, a partir desta é possível transcrever a forma como enxergamos os elementos do mundo real em código fonte, a fim de nos possibilitar a construção de sistemas complexos baseados em objetos.

O primeiro passo para utilizar o paradigma da orientação a objetos é perceber o universo em que se deseja trabalhar, uma vez que possuímos essa informação é necessário descrever a estrutura desses elementos, ou seja quais são as características mais marcantes destes para o desenvolvimento do sistema proposto.

Vejamos como descrever um objeto “Pessoa”. As perguntas a serem feitas são: “O que é uma pessoa?”,”Quais são as características de uma pessoa?”,”Como uma pessoa se comporta?”. Após responder a este questionário, teremos condições de modelar o objeto da forma como queremos. Vamos responder essas perguntas:

- O que é uma pessoa?

Resposta: A pessoa é um ser do mundo real que interage com toda a natureza.

-· Quais são as características de uma pessoa?

Resposta: Uma pessoa possui: nome, olhos, boca, braços, pernas, cabelos e etc.

-· Como uma pessoa se comporta?

Resposta: Uma pessoa corre, anda, fala, pula, come e etc.

**Nota:** Os objetos a serem implementados no sistema devem obedecer as regras de negócio solicitadas pelo cliente. O analista deve perceber a partir da explicação do usuário o que realmente é necessário e perceber a responsabilidade que os objetos terão.

Agora que já possuímos as informações do que realmente representa um objeto do tipo pessoa, precisaremos passar esse conhecimento utilizando uma linguagem de programação; é claro que qualquer linguagem que se utilize da orientação a objetos, neste artigo será exemplificado com C#.

** Nota:éé  O suporte a orientação a objetos está em muitas linguagens, no entanto a sintaxe e as funções das linguagens são diferentes, ou seja, caso esteja utilizando o Java ou o PHP é necessário verificar as particularidades destes para continuar com o artigo.

## Principais conceitos da OO

Projetamos o nosso elemento do mundo real, agora como iremos traduzir isto para o código fonte? Antes disso é preciso compreender o que foi feito até agora veja os passos:

-· Descrever uma estrutura de uma pessoa

-· Descrever as características de uma pessoa

-· Descrever o comportamento de uma pessoa

Quando descrevemos de estrutura de um elemento, na verdade criamos uma especificação básica do que todo elemento daquele tipo deve ter, isso se chama Classe. Observe a Listagem 1.

### Listagem 1. Classe C# de pessoa

ˋˋˋ
class Pessoa    {
     }
ˋˋˋ
	 
Tudo que faz parte de uma pessoa deve estar contido neste bloco de chaves.

Uma pessoa possui características que as diferem de outros seres do mundo real, isso no mundo da programação é chamado de Atributos (Listagem 2).

### Listagem 2. Atributos C# de pessoa

ˋˋˋ
class Pessoa    {
        string nome;
        int olhos,bracos,pernas;
        string cor_olhos;
        string cor_cabelos;
     }
ˋˋˋ
	 
** Nota: ** É uma boa prática declarar todos os atributos (variáveis) com o modificador de acesso private.

Os atributos devem vir acompanhados dos tipos de dados e também dos modificadores de acesso, neste caso não estamos declarando nenhum modificador de acesso, o C# implicitamente introduz a palavra “private” antes dos atributos e métodos (veremos a seguir). Classes só podem ser “public” ou “internal”. No Java, que possui uma estrutura semelhante à linguagem C#, seria a palavra “default”.

Uma pessoa também possui um comportamento diferenciado de todos os outros elementos da natureza, na POO isso é conceituado como métodos (Listagem 3).

### Listagem 3. Métodos C#

ˋˋˋ
class Pessoa    {
        string nome;
        int olhos, bracos, pernas;
        string cor_olhos;
        string cor_cabelos;
         void andar(int velocidade)        {
             // Ande um pouco
        }
        void falar()        {
             // Converse mais
        }
         void comer()       {
             // alimente-se mais
        }
     }
ˋˋˋ
	 
Finalmente criamos e modelamos o objeto. Isso pode parecer simples mas no entanto é fundamental para que um projeto orientado a objetos tenha sucesso que o programador de sistemas conheça os conceitos abordados anteriormente.

### Refinando a classe “Pessoa”

Um dos pontos fortes da Orientação a objetos é o reuso de código, ou seja, permitir que outras rotinas utilizem funções predefinidas no sistema. Ou seja, evitar escrever uma rotina várias vezes em locais diferentes. A nossa classe pessoa possui alguns atributos e métodos que podem ser utilizados por outras classes, no entanto falta um pequeno detalhe para que essa comunicação seja realizada. Veja o seguinte exemplo da Figura 1.

Para utilizar a classe Pessoa é necessária a criação de objetos vinculados a esta classe. Para fazer isto seguimos os seguintes passos:

-· Declarar a classe em que deseja que o objeto pertença;

-· Crie um nome para o objeto, neste caso declaramos como ”p”;

-· Acrescente o sinal de “=”, que neste caso não é uma comparação e sim uma atribuição;

-· “new” para a criação de todo objeto;

Veja o resultado na Listagem 4.

### Listagem 4. Objeto C#

ˋˋˋ
Pessoa p = new Pessoa();
ˋˋˋ

Veja que ao fazer a chamada ao método “falar()”, o IntelliSense não reconheceu este procedimento, pois o nível de acessibilidade (como foi visto anteriormente) está declarado de forma implícita como “private”. Uma forma de resolver este problema é declarar o modificador de acesso public no início dos métodos, conforme a Listagem 5.

### Listagem 5. Métodos públicos

ˋˋˋ
class Pessoa   {
       string nome;
       int olhos, bracos, pernas;
       string cor_olhos;
       string cor_cabelos;
       public void andar(int velocidade)       {
            // Ande um pouco
       }
      public void falar()       {
            // Converse mais
       }
       public void comer(string comida)       {
            // alimente-se mais
       }
   }
ˋˋˋ
   
Na classe Program.cs instancie (crie) um objeto do tipo de pessoa e cheque se o Visual Studio reconhece os métodos e propriedades a partir do IntelliSense. Repare que os métodos são reconhecidos, no entanto as propriedades (atributos) ainda continuam invisíveis, identificamos que isso acontece por causa dos modificadores de acesso. O nível de proteção está sendo restringido, isso na POO é definido como encapsulamento.

Para resolvermos os níveis de acesso dos atributos seria muito mais fácil declararmos todos como “public”, a visibilidade se estenderia a todos a classes da aplicação, no entanto não é uma boa prática fazer isto, pois desta forma toda classe pode alterar os atributos.

Uma forma elegante de tratar isto é manter os atributos como privados e utilizar os “Getters and Setters”, como o próprio nome diz “Retornar e alterar”. O método “Get()” será responsável por retornar alguma informação do objeto atual, enquanto o “Set(param)” realizará a alteração do objeto. Vejamos a Listagem 6.

### Listagem 6. Get and Set C#

ˋˋˋ
public string getNome()      {
          return nome; // Retorne o nome da pessoa
      }
       public void setNome(string nome)      {
          this.nome = nome; //Altere o nome da pessoa
      }
ˋˋˋ
	  
Essa é a estrutura básica dos Getters and setters em C#. Veja que no método getNome(), nenhum parâmetro é especificado, apenas a palavra reservada “return” vem seguida do atributo desejado, neste caso o “nome”.

No método setNome(string nome), ao contrário do método getNome(), declaramos um parâmetro que é justamente o valor a ser alterado e não possui nenhum tipo de retorno, por isso utilizamos a palavra “void”.

**Nota:**  Veja que agora podemos manipular as variáveis através dos getters and setters, mesmo os atributos declarados como “private”. Isto é uma boa prática utilizada em todo projeto. Podemos ver que a única classe que pode alterar as variáveis é a classe que possui os métodos get e set declarados.

Caso queira um atalho para esses métodos digite “prop” e em seguida aperte duas vezes a tecla tab; será criado um get e set automático. A estrutura será igual a essa: public int MyProperty{get;set ;}. Uma grande vantagem é que desta forma a variável é criada implicitamente nessa propriedade.

Na Listagem 7 vemos a execução do projeto.

### Listagem 7. Executando o projeto

ˋˋˋ
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
 namespace POO{
    class Program    {
        static void Main(string[] args)        {
            Pessoa p = new Pessoa();
            p.setNome("Tiago de Oliveira Vale");
            Console.WriteLine("A pessoa: " + p.getNome() +
             " foi criada com sucesso");
            Console.ReadKey();
        }
    }
}
ˋˋˋ

Execute o projeto e visualize a informação apresentada na tela de console. Primeiro foi criado o objeto “p” do tipo Pessoa, em seguida realizamos uma chamada ao método setNome(string nome), para alterar o nome do objeto e em seguinte o objeto chama o método getNome() para retornar o nome da pessoa.

## Inicialização dos objetos

Existem objetos que possuem valores padrões, ou seja, nós queremos que toda instância de uma classe apresente os mesmos valores. No nosso exemplo declaramos variáveis de tipos primitivos com os seguintes nomes: bracos, pernas, olhos.

Para fazer isto podemos utilizar os getters and setters, mas só isso não ia adiantar, seria necessário declarar manualmente a quantidade de braços, olhos e pernas. Assumindo que nosso sistema não terá ninguém com três olhos, dez pernas e cinco braços, faz-se necessário a criação de um construtor.

O .NET nos presenteia com um construtor padrão que não recebe nenhum argumento e ele é executado sempre que criamos um objeto na memória (Listagem 8).

### Listagem 8. Construtor padrão

ˋˋˋ
public Pessoa()       {
       }
ˋˋˋ
	   
Observe que em nosso exemplo não criamos este construtor, no entanto se precisarmos de mais construtores é necessário que especifique o “construtor padrão”. Todo construtor deve possuir o mesmo nome da classe. Observe a Listagem 9.

### Listagem 9. Classe Pessoa final com construtores

ˋˋˋ
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
 namespace POO{
    public class Pessoa    {
         public Pessoa(string cabelo)//Valor obrigatório        {
            Olhos = 2;//Valor default
            Bracos = 2;
            Pernas = 2;
            CorCabelo = cabelo;
         }
        public Pessoa() {          }
        public string Nome { get; set; }
        public int Olhos { get; set; }
        public string CorCabelo { get; set; }
        public int Bracos { get; set; }
        public int Pernas { get; set; }
		}
}
ˋˋˋ

Veja como a estrutura da nossa classe está bem mais enxuta com os getters and setters automáticos. Observe que em vez de apenas um construtor temos dois.

Agora veja a Listagem 10.

### Listagem 10. Program.cs final

ˋˋˋ
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace POO{
    class Program    {
        static void Main(string[] args)        {
            Pessoa p = new Pessoa();//UTILIZANDO CONSTRUTOR DEFAULT
            p.Nome = "Tiago de Oliveira Vale";
            p.Bracos = 2;
            p.Pernas = 2;
            p.Olhos = 2;
            p.CorCabelo = "Preto";
            Console.WriteLine(p.Nome + " possui " + p.Bracos +
            " braços," + "\n" + p.Pernas + " pernas, \n " + p.Olhos +
            " olhos e cabelo " + p.CorCabelo+"\n");

            Pessoa p1 = new Pessoa("Loiro");
            //UTILIZANDO CONSTRUTOR PERSONALIZADO
            p1.Nome = "Fulano";

            Console.WriteLine(p1.Nome+" possui "+p1.Bracos+
            " braços"+",\n"+p1.Pernas+" pernas, \n "+p1.Olhos+
            " olhos e cabelo "+p1.CorCabelo);

            Console.ReadKey();
        }
    }
}
ˋˋˋ

Observe como reduzimos a quantidade de linhas de código com um construtor personalizado, sem dúvidas a melhor saída para utilizar valores default na POO.

Portanto, neste artigo abordamos os conceitos básicos de orientação a objetos, aprendemos como modelar uma classe e algumas boas práticas adotadas pelo mercado, como a utilização de getters and setters. Todos os exemplos foram utilizados com a linguagem C#, mas os conceitos aprendidos são reaproveitados para outras linguagens que suportam a orientação a objetos.

Espero que tenham gostado e até o próximo artigo.

[]Artigo original](https://www.devmedia.com.br/csharp-orientado-a-objetos-introducao/29539)