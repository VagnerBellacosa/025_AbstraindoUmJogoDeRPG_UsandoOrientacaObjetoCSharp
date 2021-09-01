# Orientaçao a Objetos

## Explorar programação orientada a objeto com classes e objetos

Neste tutorial, você criará um aplicativo de console e verá os recursos básicos orientados a objeto que fazem parte da linguagem C#.

## Pré-requisitos

O tutorial espera que você tenha uma máquina configurada para desenvolvimento local. No Windows, Linux ou macOS, você pode usar a CLI do .NET para criar, criar e executar aplicativos. No Windows, você pode usar o Visual Studio 2019. Para obter instruções de instalação, consulte Configurar seu ambiente local.

## Criar o aplicativo

Usando uma janela de terminal, crie um diretório chamado classes. Você compilará o aplicativo nesse diretório. Altere para esse diretório e digite dotnet new console na janela do console. Esse comando cria o aplicativo. Abra Program.cs. Ele deverá ser parecido com:

ˋˋˋ
using System;

namespace classes
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}
ˋˋˋ

Neste tutorial, você criará novos tipos que representam uma conta bancária. Normalmente, os desenvolvedores definem cada classe em um arquivo de texto diferente. Isso facilita o gerenciamento à medida que o tamanho do programa aumenta. Crie um novo arquivo chamado BankAccount.cs no diretório classes.

Esse arquivo conterá a definição de uma conta bancária _. A programação orientada a objeto organiza o código criando tipos na forma de classes ___**. Essas classes contêm o código que representa uma entidade específica. A classe BankAccount representa uma conta bancária. O código implementa operações específicas por meio de métodos e propriedades. Neste tutorial, a conta bancária dá suporte a este comportamento:

- Ela tem um número com 10 dígitos que identifica exclusivamente a conta bancária.
- Ela tem uma cadeia de caracteres que armazena o nome ou os nomes dos proprietários.
- O saldo pode ser recuperado.
- Ela aceita depósitos.
- Ele aceita saques.
- O saldo inicial deve ser positivo.
- Os saques não podem resultar em um saldo negativo.
- Definir o tipo de conta bancária

Você pode começar criando as noções básicas de uma classe que define esse comportamento. Crie um novo arquivo usando o comando File:New. Nomeia-o BankAccount.cs. Adicione o seguinte código ao arquivo BankAccount.cs:

ˋˋˋ
using System;

namespace classes{
    public class BankAccount    {
        public string Number { get; }
        public string Owner { get; set; }
        public decimal Balance { get; }

        public void MakeDeposit(decimal amount, DateTime date, string note)        {
        }

        public void MakeWithdrawal(decimal amount, DateTime date, string note)        {
        }
    }
}
ˋˋˋ

Antes de continuar, vamos dar uma olhada no que você compilou. A declaração namespace fornece uma maneira de organizar logicamente seu código. Este tutorial é relativamente pequeno, portanto, você colocará todo o código em um namespace.

**public class BankAccount ** define a classe ou o tipo que você está criando. Tudo dentro de { e que segue a declaração de classe define o estado e o comportamento da } classe. Há cinco membros _ da BankAccount classe . As três primeiras _são_ propriedades . Propriedades são elementos de dados que podem ter um código que impõe a validação ou outras regras. Os dois últimos são métodos ___**. Os métodos são blocos de código que executam uma única função. A leitura dos nomes de cada um dos membros deve fornecer informações suficientes para você, ou outro desenvolvedor, entender o que a classe faz.

- Abrir uma nova conta
O primeiro recurso a ser implementado serve para abrir uma conta bancária. Quando um cliente abre uma conta, ele deve fornecer um saldo inicial e informações sobre o proprietário, ou proprietários, dessa conta.

Criar um novo objeto do BankAccount tiposignifica definir um construtor * _ que atribui esses valores. Um construtor ___* é um membro que tem o mesmo nome que a classe . Ele é usado para inicializar objetos desse tipo de classe. Adicione o construtor a seguir ao BankAccount tipo . Coloque o seguinte código acima da declaração de MakeDeposit :

ˋˋˋ
public BankAccount(string name, decimal initialBalance)
{
    this.Owner = name;
    this.Balance = initialBalance;
}
ˋˋˋ

Construtores são chamados quando você cria um objeto usando new . Substitua a linha Console.WriteLine("Hello World!"); em Program.cs pelo seguinte código (substitua <name> pelo seu nome):

ˋˋˋ
var account = new BankAccount("<name>", 1000);
Console.WriteLine($"Account {account.Number} was created for {account.Owner} with {account.Balance} initial balance.");
ˋˋˋ

Vamos executar o que você criou até agora. Se você estiver usando o Visual Studio, selecione Iniciar sem depuração no menu Depurar. Se você estiver usando uma linha de comando, digite dotnet run o diretório em que você criou seu projeto.

Você notou que o número da conta está em branco? É hora de corrigir isso. O número da conta deve ser atribuído na construção do objeto. Mas não é responsabilidade do chamador criá-lo. O código da classe BankAccount deve saber como atribuir novos números de conta. Uma maneira simples de fazer isso é começar com um número de 10 dígitos. Incremente-o à medida que novas contas são criadas. Por fim, armazene o número da conta atual quando um objeto for construído.

Adicione uma declaração de membro à BankAccount classe . Coloque a seguinte linha de código após a chave de { abertura no início da classe BankAccount :

ˋˋˋ
private static int accountNumberSeed = 1234567890;
ˋˋˋ

Este é um membro de dados. Ele é private, o que significa que ele só pode ser acessado pelo código dentro da classe BankAccount. É uma maneira de separar as responsabilidades públicas (como ter um número de conta) da implementação privada (como os números de conta são gerados). Ele também é static, o que significa que é compartilhado por todos os objetos BankAccount. O valor de uma variável não estática é exclusivo para cada instância do objeto BankAccount. Adicione as duas linhas a seguir ao construtor para atribuir o número da conta. Coloque-os após a linha que diz this.Balance = initialBalance :

ˋˋˋ
this.Number = accountNumberSeed.ToString();
accountNumberSeed++;
ˋˋˋ

Digite dotnet run para ver os resultados.

## Criar depósitos e saques

A classe da conta bancária precisa aceitar depósitos e saques para funcionar corretamente. Vamos implementar depósitos e saques criando um diário de todas as transações da conta. Isso apresenta algumas vantagens em comparação à simples atualização do saldo em cada transação. O histórico pode ser usado para auditar todas as transações e gerenciar os saldos diários. Ao calcular o saldo do histórico de todas as transações, quando for necessário, todos os erros corrigidos em uma única transação serão refletidos corretamente no saldo no próximo cálculo.

Vamos começar criando um novo tipo para representar uma transação. É um tipo simples que não tem qualquer responsabilidade. Ele precisa de algumas propriedades. Crie um novo arquivo chamado Transaction.cs. Adicione os seguintes códigos a ela:

ˋˋˋ
using System;

namespace classes{
    public class Transaction    {
        public decimal Amount { get; }
        public DateTime Date { get; }
        public string Notes { get; }

        public Transaction(decimal amount, DateTime date, string note)        {
            this.Amount = amount;
            this.Date = date;
            this.Notes = note;
        }
    }
}
ˋˋˋ

Agora, vamos adicionar um List<T> de Transaction objetos à classe BankAccount. Adicione a seguinte declaração após o construtor no arquivo BankAccount.cs:

ˋˋˋ
private List<Transaction> allTransactions = new List<Transaction>();
ˋˋˋ

A classe List<T> exige que você importe um namespace diferente. Adicione o seguinte no início de BankAccount.cs:

ˋˋˋ
using System.Collections.Generic;
ˋˋˋ

Agora, vamos calcular corretamente o Balance . O saldo atual pode ser encontrado somando os valores de todas as transações. Como o código está atualmente, você só pode obter o saldo inicial da conta, portanto, você terá que atualizar a Balance propriedade. Substitua a linha public decimal Balance { get; } em BankAccount.cs pelo seguinte código:

ˋˋˋ
public decimal Balance{
    get    {
        decimal balance = 0;
        foreach (var item in allTransactions)        {
            balance += item.Amount;
        }

        return balance;
    }
}
ˋˋˋ

Este exemplo mostra um aspecto importante das propriedades. Agora, você está calculando o saldo quando outro programador solicita o valor. Seu cálculo enumera todas as transações e fornece a soma como o saldo atual.

Depois, implemente os métodos MakeDeposit e MakeWithdrawal. Esses métodos aplicarão as duas últimas regras: que o saldo inicial deve ser positivo, e que qualquer saque não pode criar um saldo negativo.

Isso introduz o conceito de exceções. A forma padrão de indicar que um método não pode concluir seu trabalho com êxito é lançar uma exceção. O tipo de exceção e a mensagem associada a ele descrevem o erro. Aqui, o MakeDeposit método lançará uma exceção se a quantidade do depósito não for maior que 0. O método lançará uma exceção se o valor de retirada não for maior que 0 ou se a aplicação da retirada MakeWithdrawal resulta em um saldo negativo. Adicione o seguinte código após a declaração da allTransactions lista:

ˋˋˋ
public void MakeDeposit(decimal amount, DateTime date, string note){
    if (amount <= 0)    {
        throw new ArgumentOutOfRangeException(nameof(amount), "Amount of deposit must be positive");
    }
    var deposit = new Transaction(amount, date, note);
    allTransactions.Add(deposit);
}

public void MakeWithdrawal(decimal amount, DateTime date, string note){
    if (amount <= 0)    {
        throw new ArgumentOutOfRangeException(nameof(amount), "Amount of withdrawal must be positive");
    }
    if (Balance - amount < 0)    {
        throw new InvalidOperationException("Not sufficient funds for this withdrawal");
    }
    var withdrawal = new Transaction(-amount, date, note);
    allTransactions.Add(withdrawal);
}
ˋˋˋ

A throw instrução lança uma exceção. A execução do bloco atual é encerrada e o controle transferido para o bloco catch da primeira correspondência encontrado na pilha de chamadas. Você adicionará um bloco catch para testar esse código um pouco mais tarde.

O construtor deve receber uma alteração para que adicione uma transação inicial, em vez de atualizar o saldo diretamente. Como você já escreveu o método MakeDeposit, chame-o de seu construtor. O construtor concluído deve ter esta aparência:

ˋˋˋ
public BankAccount(string name, decimal initialBalance){
    this.Number = accountNumberSeed.ToString();
    accountNumberSeed++;

    this.Owner = name;
    MakeDeposit(initialBalance, DateTime.Now, "Initial balance");
}
ˋˋˋ

DateTime.Now é uma propriedade que retorna a data e a hora atuais. Teste isso adicionando alguns depósitos e retiradas em seu método, seguindo o Main código que cria um novo BankAccount :

ˋˋˋ
account.MakeWithdrawal(500, DateTime.Now, "Rent payment");
Console.WriteLine(account.Balance);
account.MakeDeposit(100, DateTime.Now, "Friend paid me back");
Console.WriteLine(account.Balance);
ˋˋˋ

Em seguida, teste se você está capturando condições de erro tentando criar uma conta com um saldo negativo. Adicione o seguinte código após o código anterior que você acabou de adicionar:

ˋˋˋ
// Test that the initial balances must be positive.
BankAccount invalidAccount;
try{
    invalidAccount = new BankAccount("invalid", -55);
}
catch (ArgumentOutOfRangeException e){
    Console.WriteLine("Exception caught creating account with negative balance");
    Console.WriteLine(e.ToString());
    return;
}
ˋˋˋ

Use as try instruções e catch para marcar um bloco de código que pode lançar exceções e capturar os erros esperados. Você pode usar a mesma técnica para testar o código que lança uma exceção para um saldo negativo. Adicione o seguinte código ao final do Main método :

ˋˋˋ
// Test for a negative balance.
try {
    account.MakeWithdrawal(750, DateTime.Now, "Attempt to overdraw");
}
catch (InvalidOperationException e){
    Console.WriteLine("Exception caught trying to overdraw");
    Console.WriteLine(e.ToString());
}
ˋˋˋ

Salve o arquivo e digite dotnet run para testá-lo.

## Desafio – registrar em log todas as transações

Para concluir este tutorial, escreva o método GetAccountHistory que cria um string para o histórico de transações. Adicione esse método ao tipo BankAccount:

ˋˋˋ
public string GetAccountHistory(){
    var report = new System.Text.StringBuilder();

    decimal balance = 0;
    report.AppendLine("Date\t\tAmount\tBalance\tNote");
    foreach (var item in allTransactions)    {
        balance += item.Amount;
        report.AppendLine($"{item.Date.ToShortDateString()}\t{item.Amount}\t{balance}\t{item.Notes}");
    }

    return report.ToString();
}
ˋˋˋ

Isso usa a classe StringBuilder para formatar uma cadeia de caracteres que contém uma linha para cada transação. Você viu o código de formatação da cadeia de caracteres anteriormente nesses tutoriais. Um caractere novo é \t. Ele insere uma guia para formatar a saída.

Adicione esta linha para testá-la no Program.cs:

ˋˋˋ
Console.WriteLine(account.GetAccountHistory());
ˋˋˋ

Execute seu programa para ver os resultados.

[Artigo Original](https://docs.microsoft.com/pt-br/dotnet/csharp/fundamentals/tutorials/classes)