# Orientaçao a Objetos

## Programação Orientada a Objetos com C#
##### Renicius Pagotto Fostaini

Hoje abordaremos conceitos básicos de Programação Orientada a Objetos, mais conhecido como OOP, ou pelo menos vamos relembrar seus pontos chaves, afinal, utilizamos na grande maioria dos projetos que trabalhamos.

OOP é um estilo de programação que esta diretamente associado com conceitos de classes, objetos, herança, polimorfismo, encapsulamento e abstração

## O que é Objeto?

O objeto representa alguma coisa dentro do nosso sistema, por exemplo: Casa, Pessoa, Carro. Em resumo é uma abstração de algum modelo real dentro do nosso sistema.

## O que é Classe?

A classe é uma estrutura de código que contêm métodos, variáveis e comportamentos

Com esses dois conceitos explicados, vamos agora falar um pouco sobre os 4 pilares da OOP.

## Herança

É uma funcionalidade que permite o uso de códigos entre objetos relacionados, ou seja, caso eu possua um Objeto B que contêm as mesmas propriedades do Objeto A, posso utilizar herança, com o objetivo de evitar a duplicação de código.

Outro exemplo são entidades com relacionamento pai e filho. Imagine uma classe clamada Veículos, no qual um veículo pode se compartar de diferentes maneiras conforme seu tipo, porém, possuem características em comum, como por exemplo: Motor, Acelerador, Freio, etc. Desta maneira, usamos a herança de uma forma eficaz, melhorando a legibilidade e evitando a duplicação de características entre as classes.

## Abstração

Essa característica esta diretamente ligada com uso de classes, conforme abordado mais acima. É nesse momento que abstraímos o mundo real em nossa classe.

Utilizando o exemplo do veículo, vemos que possuem motor, acelerador, freio, utilizam combustível, entre outras caracteristicas. Portanto é com base nessas informações que vamos construir nossa classe.

Como observamos acima, os veículos possuem a ação acelerador e freiar em comum, logo, todos as entidades relacionadas a veículos também vão possuir.

Note que nesse momento eu fiz uma pequena abstração de veículo e ainda utilizei a herança.

## Encapsulamento

É a tecnica de esconder detalhes de funcionamento interno do nosso objeto ou classe para outros objetos, pois um objeto A que utilize alguma ação de um objeto B, não precisa conhecer os detalhes de implementação daquela ação.

Trazendo um pouco mais para o nosso mundo. Imagine que ao entrar no veículo, precisamos liga-lo para que possamos andar com eles pela rua. A ação de ligar o motor é um encapsulamento do que acontece internamente no motor, pois não necessitamos saber que ao rodar a chave, vai ser acionado o motor de partida, feito a injeção de combustível e realizado a queima do mesmo, apenas necessitamos ligar o motor.

Perceba que em nosso console, apenas realizamos uma chamada para o método ligar, pois não precisamos conhecer detalhes internos desses objetos.

## Polimorfismo

É uma funcionalidade no qual objetos relacionados se comportam de maneiras totalmente distintas, ou seja, podemos invocar métodos comuns entre os objetos, onde cada objeto possuirá um comportamento diferente.

No exemplo exibido acima, possuímos a classe base Veiculo, que possui o método Ligar em comum para suas derivações, ou seja, para Aviao e Carro, mas perceba que eles possuem implementações (comportamentos) diferentes para cada tipo de derivação.

Perceba que ao instanciar um veículo, chamamos um objeto Carro, mas atribuímos em uma varíavel do tipo Veiculo, isso somente é permitido pois Carro é uma classe derivada de veículo, logo a classe Veículo pode se comportar de diferentes formas dependendo do tipo da classe derivada está sendo utilizada naquele momento.

Em resumo, polimorfismo nada mais é do que a capacidade de invocar métodos comuns que possuem comportamento específicos para cada tipo do objeto.

## Conclusão

OOP é o paradigma de programação que se aproxima muito como mundo real, por causa disso é de fácil entendimento. Ela traz grandes benefícios para o nosso código, dentre eles a reutilização de objetos, flexibilidade para adaptar novos comportamentos entre outros.

[Artigo Original](https://renicius-pagotto.medium.com/programa%C3%A7%C3%A3o-orientada-a-objetos-com-c-906e8fb6610c)
