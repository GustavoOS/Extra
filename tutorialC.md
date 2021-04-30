# C para programadores de Python

C é uma linguagem que foi criada em 1972, muito antes do Python.
Diferente do Python, é uma linguagem estritamente compilada, feita
sem a intercompatibilidade em mente.


A partir da década de 1990, houve a criação de uma linguagem irmã
C++ que trouxe várias novidades como o suporte nativo a classes, orientação a objeto, etc. C++ mantém a retrocompatibilidade com C.

Como tanto C quanto C++ são linguagens compiladas, tem a vantagem de utilizar menos recursos da máquina, possibilitando ganhos de performance. Esses ganhos de performance podem ser cruciais em algumas aplicações críticas. A maioria dos sistemas operacionais modernos são escritos em C ou C++, bem como as aplicações da pilha de redes.

Esse é um tutorial rápido, para uma apostila mais completa, confira a [apostila C Descomplicado](https://1drv.ms/b/s!AiJdOAM_D4UVg-4f8Osc8CcfCNqOGg).

Para aprender mais sobre C++, sugiro o artigo [A quick introduction to C++](https://homes.cs.washington.edu/~tom/c++example/c++.pdf).



## Compilador


### Rode online

Programas escritos em C podem ser executados online pelo [GDB Online](https://www.onlinegdb.com/online_c_compiler).

### Linux
Existem vários compiladores de C/C++, e cada compilador possui algumas características de funcionamento muito próprias.
O principal compilador de C é o [GCC](https://gcc.gnu.org/), que roda em Linux. Mas, é muito mais comum utilizar o compilador de C++,
o G++, que utiliza o GCC debaixo dos panos e pode entregar mensagens mais úteis ao programador.

Para instalá-los, caso esteja desenvolvendo em Ubuntu ou Debian, rode o seguinte comando:
```sh
    sudo apt install build-essential
```
#### Compilando utilizando o G++

Para compilar um programa C utilizando o G++, tenha ele escrito em um arquivo com a extensão ".c". Assumindo que o nome do arquivo é "programa.c", rode o comando na mesma pasta onde está o arquivo:
```sh
    g++ -Wall programa.c -o  programa
```
Decifrando o comando:
1. `g++` é o compilador
1. `-Wall` é uma opção para exibir avisos
1. `programa.c` é o arquivo que contém o código C
1. `-o` é uma opção que diz ao compilador que queremos dar um nome para o arquivo compilado
1. `programa` é o nome do programa executável gerado ao final do processo de compilação

Esse comando gera um arquivo executável. Para executar esse arquivo, rode o comando:
```sh
    ./programa
```

### Windows
No Windows, pode-se usar alguma virtualização de Linux (como o [MingW](https://terminaldeinformacao.com/2015/10/08/como-instalar-e-configurar-o-gcc-no-windows-mingw/), máquina virtual ou [WSL](https://docs.microsoft.com/pt-br/windows/wsl/install-win10)) para utilizar o G++ ou o GCC, ou ainda utilizar o Microsoft Visual Studio, que possui o compilador Visual C++.


Caso queira utilizar o CodeBlocks junto com o MingW, baixe um instalador [nesse link](https://www.codeblocks.org/downloads/binaries/) com o mingw embutido, é a opção mais cômoda.

Caso queira utilizar o Visual Studio Code junto com o WSL, siga [esse tutorial] (https://code.visualstudio.com/docs/cpp/config-wsl).

Caso queira programar com o Microsoft Visual Studio, baixe [nesse link](https://visualstudio.microsoft.com/pt-br/vs/features/cplusplus/). Para desenvolver utilizando o Visual Studio, crie uma aplicação de console em C/C++. É necessário usar o comando abaixo ao final da função main (veremos o que significa adiante) para que o console (terminal) não seja fechado automaticamente ao final da execução. A própria IDE tem botões específicos para compilar e executar o código.

```c
    system("pause");
```


## Hello, World

Uma boa maneira para começar a entender uma linguagem nova é entendendo como funciona um programa `"Hello, world"`.
Vamos ao código:

```c
#include<stdio.h>

int main(void) {
    printf("Hello, World!\n");

    return 0;
}

```
A primeira linha possui uma inclusão da biblioteca padrão para entrada e saída, que é definida por arquivo de cabeçalho `stdio.h`. Essa biblioteca é responsável pela interação da máquina com o as entradas e saídas do programa.

A terceira linha define a função principal `main`. Essa função define a ordem do que vai ser executado. A palavra `int` significa que o retorno da função é um número inteiro. A palavra `void` entre parênteses após o nome da função significa que a função não está recebendo nenhum parâmetro.

A quarta linha acontece uma saída formatada `printf()`, imprimindo um texto formatado na tela. Esse texto é a string `"Hello, World!\n"`. Esse `\n` é um caractere especial, que simboliza uma mudança de linha. Ao final do comando, existe a demarcação feita pelo `;`.

Na sexta linha ocorre o retorno, feito pelo `return`, da função principal com o número `0`, que indica que o programa funcionou sem erros.

Na sétima linha, o símbolo `}` representa o final da função principal, iniciada na terceira linha pelo símbolo `{`.

Repare que existem `;` ao final de cada comando. Isso acontece para que expressões grandes possam ser divididas em várias linhas e para permitir que a identação se torne livre sem perder o controle do escopo. O escopo é iniciado pelo par de {}, não pela identação. Por exemplo, o mesmo programa Hello World poderia ser escrito assim:

```c
#include<stdio.h>

int main(void) {
    printf(
            "Hello, World!\n"
        );

    return 0;
}

```

## Comentários

Nem tudo o que está escritoem um código fonte precisa ser compilado. Para isso, C dá suporte a comentários, que podem ser úteis para entender o que parte de um código está fazendo. Em C, existem dois tipos de comentários: de uma linha e de várias linhas

Para sinalizar um comentário de uma linha, escreva `//`. Tudo o que estiver escrito naquela linha após as barras será ignorado pelo compilador.

Para comentários de mais de uma linha, é necessário sinalizar um início e um fim. O início de um comentário de muitas linhas é demarcado por `/*` e o fim por `*/`

```c
    // Eu sou um comentário de uma linha
    /* EU
    SOU
    UM
    COMENTÁRIO
    BEM
    LONGO
    */
```


## Tipos de dados em C

Os tipos de dados de uma variável em C não podem mudar, como em Python. Por isso, é bastante importante saber quais são os tipos e o que eles representam. Os **principais** e mais primitivos tipos são definidos na tabela abaixo:


Tipo de Dado | O que representa | Número de Bits da informação
------------ | ----------------- | -------------
`int` | Número inteiro | 32
`char` | Caractere ou número pequeno | 8
`double` | Número fracionário | 64


### Modificadores de tipos


Todos os modificadores de tipos que veremos são opcionais, são palavras que vem antes do tipo do dado e modificam a interpretação do tipo.

Por padrão, números em C podem ter sinal, ou seja são números `signed`. Porém, dependendo da grandeza desses números, pode ser útil ignorar os sinais, armazenando apenas números positivos. Para isso, podemos utilizar a palavra `unsigned` antes do tipo de dado.

O tipo int pode ser encurtado, passando a utilizar apenas 16 bits, utilizando a palavra `short` antes do tipo de dado.

O tipo double pode ser alongado, passando a utilizar 96 bits, utilizando a palavra `long` antes do tipo de dado.


## Declaração de Variáveis

Em C, antes de poder se utilizar uma variável, é necessário declará-la. Para isso acontecer, é preciso definir qual o tipo de dados ela armazenará.

Sintaxe: (tipo) (nome da variável);
Exemplo:
```c
    int quantidade;
```

É possível declarar de uma vez várias variáveis do mesmo tipo basta colocar uma sequência de nomes separados por vírgula, veja:
```c
    double pi, euler;
```

Ainda é possível atribuir um valor à variável durante a sua declaração:
```c
    int ano = 1972;
```

### Arrays, Strings e Matrizes

Para armazenar uma sequência de valores em uma única variável, são utilizados os arrays.
Para isso, durante a declaração da variável, após o nome da variável, defina a quantidade de dados da sequência.
Por exemplo, se uma variável precisa armazenar uma sequência que pode assumir até 10 valores, declara-se assim:
```c
    int sequencia [10];
```
Durante a declaração, ainda é possível atribuir de vez um valor a esse array, colocando uma sequência separada por vírgulas delimitada por {}:
```c
    int sequencia [10] = {1, 12, 23, 34, 45, 56, 67, 78, 89, 90};
```

Arrays podem ser acessados pelo seu índice, que assim como no Python começam a partir do 0. Mas cuidado! Acessar uma posição de um array que não existe causa o terrível erro "Segmentation Fault", ou "Core Dumped". Ao se deparar com esses erros, verifique se o acesso a vetores está utilizando os índices corretos. Ao contrário do Python,  os arrays em C não armazenam a quantidade de elementos, e devem possuir um tamanho máximo fixo.

```c
#include<stdio.h>

int main(void) {
    int sequencia [10] = {1, 12, 23, 34, 45, 56, 67, 78, 89, 90};
    printf("%d - %d", sequencia[0], sequencia[9]);
    return 0;
}
```
Strings, que representam texto, são um tipo específico de array: um array de caracteres terminado pelo caractere `\0`. Cada caractere é representado entre aspas simples. 
```c
    char joe [4] = {'J', 'o', 'e','\0'};
```
Para facilitar a declaração, pode-se utilizar aspas duplas e omitir o último carectere.
```c
    char maria[6] = "maria";
```
Matrizes são arrays com mais dimensões. Por exemplo, uma matriz 3x3 possui 2 dimensões. Para declarar uma matriz em C, utiliza-se o tamanho de cada dimensão entre []. Para declarar uma matriz de 4 linhas e 5 colunas, pode-se fazer do jeito abaixo:
```c
    int matriz [4][5];
```
Um exemplo de declaração de matriz com atribuição:
```c
    int matriz [3][4] = {{1, 2, 3, 4}, {5, 6, 7, 8}, {9, 10, 11, 12}};
```

Declarar um array, string ou matriz junto com uma atribuição pode dar uma vantagem: o compilador pode definir o tamanho automaticamente, omitindo o tamanho e mantendo os []. Lembrando que uma vez o tamanho definido, não pode ser alterado. Exemplo:
```c
    char texto [] = "não precisei contar o número de caracteres nem somar 1";
```
## Atribuição

Uma variável declarada pode receber valores. O operador `=` é utilizado para definir uma atribuição de valor.

```c
    int i, j [4];
    i = 5; //Atribuição
    j[0] = 4; // Como no Python, os índices de um array de 4 elementos vão de 0 a 3
```

Para copiar uma string para outra variável, utilize a biblioteca string.h, especialmente a strcpy, responsável por copiar
```c
#include<stdio.h>
#include<string.h>

int main (void) 
{
    char texto [50] = "esse é o texto", copia[50];
    strcpy(copia, texto); // primeiro parâmetro é o destino, o segundo a origem
    printf("%s", copia);
    return 0;
}
```
## Imprimindo na tela

A função `printf` é diferente da função print do Python, pois a printf facilita a substituição de trechos de um texto por outras variáveis. Para fazer isso, é preciso informar ao printf onde o programador deseja fazer essa substituição e passar a variável que possui o valor desejado. O primeiro parâmetro a ser passado para a função é o texto formatado. Os demais parâmetros são as variáveis que possuem os valores, na ordem em que são sinalizados no texto.


Sinalização | Interpretação
----------- | -------------
%s | texto
%d | número inteiro
%lf | número real
%c | caractere

Exemplo:
```c
#include<stdio.h>

int main(void){
    char produto [] = "coca-cola";
    int preco = 3;
    printf("O produto %s custa %d reais\n", produto, preco);

    return 0;
}

```

Números reais podem possuir muitas casas decimais. Para limitar as casas decimais de um número, entre o % e o lf, adicione um ponto e o número de casas. Por exemplo, para mostrar apenas duas casas decimais, use %.2lf :

```c
#include<stdio.h>

int main(void){
    char produto [] = "coca-cola";
    double preco = 6.90;
    printf("O produto %s custa %.2lf reais\n", produto, preco);

    return 0;
}

```

## Lendo do teclado

Para ler do teclado, utiliza-se a função `scanf()`, também definida na `stdio.h`. Ela funciona semelhante à printf, recebendo uma string formatada, retirando da string recebida do teclado as variáveis. A diferença é que os nomes das variáveis devem ser precedidos pelo símbolo `&`.

```c
#include<stdio.h>

int main(void){
    double numero;
    printf("Digite um número\n");
    scanf("%lf", &numero);
    printf("O número digitado foi %lf", numero);
    return 0;
}

```


## Operações

Símbolo | Significado | Exemplo de uso
------- | -------- | ------------
`+` | Soma | `2 + 3`
`-` | Subtração | `3 - 2`
`*` | Multiplicação | `3 * 2`
`/` | Divisão | `3 / 2`
`%` | Resto de divisão | `3 % 2`
`==` | Comparação de igualdade | `1 == 1`
`!=` | Comparação de desigualdade | `2 != 3`
`++` | Auto incremento passo 1 | `contador++`
`--` | Auto decremento passo 1 | `contador--`
`+=` | Auto incremento ao passo | `total += preco`
`-=` | Auto decremento ao passo | `saldo -= saque`
`*=` | Auto multiplicação ao passo | `montante*=(1 + juros)`
`/=` | Auto divisão ao passo | `valor/=numeroDePessoas`
`<` | Menor | `2 < 3`
`<=` | Menor ou igual | `3 <= 2`
`>` | Maior | `3 > 2`
`>=` | Maior ou igual | `3 >= 2`
`&&` | O mesmo que `and` no Python | `2 >= 1 && saque < saldo`
`\|\|` | O mesmo que `or` no Python | `saque < saldo \|\| saque < creditoDisponivel`

## Condicionais

Assim como Python, C possui estruturas de if/else. Porém não apresenta os elifs. O escopo do if e do else não são marcados pela identação, mas pelas {}
```c
#include<stdio.h>

int main (void)
{
    int number;
    scanf("%d", &number);
    if ((number % 2) == 0)
    {
        printf("Número %d é par", number);
    }
    else
    {
        printf("Número %d é ímpar", number);
    }
    return 0;
}

```

Caso o if só possua uma linha de código, é possível remover os {}

```c
#include<stdio.h>

int main (void) 
{
    int number;
    scanf("%d", &number);
    if ((number % 2) == 0)
        printf("Número %d é par", number);
    else
        printf("Número %d é ímpar", number);

    return 0;
}
```

### Atribuição condicional

O operador ternário pode ser usado para realizar atribuição condicional, ou seja, existir atribuições diferentes para a mesma variável a depender de uma condição. As seguintes linhas de código possuem o mesmo resultado.
```c
    int a;
    a = 2 > 3 ? 27 : 45; // Opção com operador ternário. No caso, a vai receber o valor 27.

    //Segunda opção realiza o mesmo que a opção com operador ternário
    if(2 > 3)
        a = 27;
    else
        a = 45;

```

### Switch/case

Recurso semelhante ao match/case do novíssimo [Python 3.10](https://martinheinz.dev/blog/46), permite a avaliação consecutiva de um valor. Um exemplo clássico é o sistema de telemarketing: quando você liga, o sistema te apresenta um menu onde todas as opções dependem do valor que você digitar no teclado; o switch case funciona justamente para que cada opção possa ser discernida sem utilizar vários if e elses aninhados.

```c
    // Exemplo de call center
    switch (numeroDiscado) // a expressão a ser avaliada deve ser inteira
    {
        case 1: /* todo númeroDiscado vai ser avaliado se o valor é 1,
                 se sim, começa a executar, se não, passa pro pro próximo
                 case */
            printf("Empréstimos");
            break; /* Se estiver ausente, após a execução das linhas acima,
                    irá continuar a executar os próximos casos */
        case 2: // Pode haver quantos casos quiser
            printf("Cancelamento de conta");
            break; // Não se esqueça do break
        default: // Opção padrão, aquela que é executada quando nenhum dos casos dá certo
            printf("Opção inválida");
            break;
    }

```

## Repetições

### While

Muito semelhante ao while em Python. Executa o conteúdo do laço delimitado pelos {} enquanto a condição for verdadeira.

```c
#include<stdio.h>

int main (void) 
{
    int i = 0;
    while(i < 10) { //Chaves importantes no while
        printf("%d\n", i);
        i++; // O mesmo que i = i + 1;
    }
    return 0;
}
```
### For


Outra estrutura semelhante do Python é o for. Porém a ausência do range no C faz com o que seu uso seja um pouco diferente. Nos argumentos do for existe três partes, a primeira é a inicialização, a do meio é a condição e a final é a alteração. Abaixo vemos um exemplo que mostra o intervalo de 0 a 9, o que totaliza 10 elementos. Para isso, a inicialização da variável i como 0, a condição i < 10, e o incremento de i é a alteração. Toda vez que a condição é verdadeira, o corpo do laço é executado, e depois o incremento acontece. Muito útil para ver todos os elementos de um array.

```c
#include<stdio.h>

int main (void) 
{
    for (int i = 0; i < 10; i++) {
        printf("%d\n", i);
    }
    return 0;
}
```
Se a variável for declarada no campo de inicialização de um for, ela só será acessível no corpo desse for.
Assim como no if, se o corpo do for só possuir uma única linha, os {} são desnecessários:

```c
#include<stdio.h>

int main (void) 
{
    for (int i = 0; i < 10; i++)
        printf("%d\n", i);
    return 0;
}
```

## Funções

Dizem por aí que o melhor código é aquele que você não precisa de escrever. Isso só é possível em um ambiente onde um código já escrito pode ser reaproveitado, funcionando de maneira semelhante, mediante ao envio de argumentos novos. Essa reutilização de código é feita em C através das funções.

### Declarando funções

Funções em C devem especificar o tipo de seus parâmetros e do seu retorno. Quando não admite retorno, o tipo a ser declarado será `void`.

Para declarar uma função, especifique o tipo de retorno, dê um nome para a função, e elenque os seus parâmetros e seus tipos, para então definir seu funcionamento.
```c
#include<stdio.h>
// Função sem parâmetros e sem retorno
void latir()
{
    printf("auau\n");
}

// Função sem retorno com um parâmetro
void digaIdade(int idade)
{
    printf("Eu tenho %d anos\n", idade);
}

// Função sem retorno com parâmetros
void conteDeAte(int de, int ate)
{
    for(int i = de; i <= ate; i++)
        printf("%d\n", i);
}

// Função com retorno inteiro e parâmetros
int escolheOMaior(int a, int b)
{
    return a > b? a : b;
}
```
### Usando funções

Para utilizar uma função, escreva seu nome e passe a lista de argumentos na ordem correta entre parênteses. Se for armazenar o resultado em uma variável, a variável precisa ter o mesmo tipo da função. Teste:

```c
#include<stdio.h>
// Função sem parâmetros e sem retorno
void latir()
{
    printf("auau\n");
}

// Função sem retorno com um parâmetro
void digaIdade(int idade)
{
    printf("Eu tenho %d anos\n", idade);
}

// Função sem retorno com parâmetros
void conteDeAte(int de, int ate)
{
    for(int i = de; i <= ate; i++)
        printf("%d\n", i);
}

// Função com retorno inteiro e parâmetros
int escolheOMaior(int a, int b)
{
    return a > b? a : b;
}

int main(void) {
    latir();
    digaIdade(5);
    conteDeAte(100, 110);
    int maior = escolheOMaior(50, 60);
    printf("O maior é %d\n", maior);
    return 0;
}
```

### Recursividade

Uma função pode chamar ela própria para resolver algum problema. Por exemplo, veremos uma função que calcula o fatorial de um número:

```c
unsigned int fatorial(unsigned int x){ //unsigned nos livra de analisar números negativos
    if(x == 0 || x == 1) // Condição para parar de chamar a si mesmo
        return 1; // Fatorial de 0 é 1, bem como fatorial de 1
    return x * fatorial(x - 1); // Fatorial de x é igual x vezes fatorial de x-1
}
```

Durante uma chamada recursiva, o compilador para a execução, guarda onde está, e começa uma execução da função nova, empilhando o contexto da nova chamada de função. Quando a execução acabar, o programa desempilha todo o contexto e continua de onde parou. O perigo da função recursiva é de ela ficar chamando a si mesma e nunca parar de se chamar, e isso acaba causando um erro de estouro de pilha, conhecido como "stack overflow".

## Tipos definidos pelo programador

Python é uma linguagem moderna, possui classes, dicionários, etc. Mas C é uma linguagem muito mais simples, mas como um programador pode fazer que uma única variável possa guardar mais informações?

A resposta para essa pergunta é: utilizando estruturas, ou *structs*. Para criar uma estrutura, damos um nome para ela, definimos os tipos e os nomes de seus campos. Structs devem ser declarados fora de qualquer função, inclusive da main. Veja como poderíamos criar uma estrutura de formulário:

```c
struct formulario {
    char nome [50];
    int idade;
    char rua [50];
    int numero;
    char ddd [3];
    char celular [10];
}; // Não esquecer do ;
```

Se quisermos criar uma variável com a estrutura acima, quando declararmos a variável será necessário definir o tipo como `struct formulario`. Acessamos os campos da estrutura utilizando a notação ponto. Veja o exemplo:

```c
#include<stdio.h>
#include<string.h>

struct cadastro {
    char nome [50];
    int idade;
};

int main(void) {
    struct cadastro meuCadastro;
    strcpy(meuCadastro.nome, "Enzo"); // Copia "Enzo" para o campo nome da variável meuCadastro
    meuCadastro.idade = 18; // Atribui 18 ao campo idade

    /* ***************************************
    Imprime como se fosse um dicionário ou JSON
    O \" sinaliza que é para imprimir as aspas,
    não terminando a string antes da hora.
    **************************************** */
    printf("{\n  \"nome\" : \"%s\",\n  \"idade\" : %d\n}", meuCadastro.nome, meuCadastro.idade);
}
```
## Renomeando tipos

Podemos renomear os tipos, tanto primitivos quanto estrutuas utilizando o comando `typedef`. É bastante útil para estruturas pois evita a repetição do nome *struct*. Veja alguns exemplos:

```c
typedef int inteiro;
/* A partir de agora pode-se declarar variáveis utilizando o tipo inteiro */
inteiro x;


typedef struct cad {
    char nome [50];
    int idade;
} cadastro;

// A partir de agora pode-se declarar o cadastro utilizando somente cadastro como tipo:
cadastro meuCadastro;
```


## Ponteiros

Em Python, diz-se que em tudo se trabalha com referências. Em C, para se trabalhar com referências, é preciso especificar essas referências. Vamos entender melhor? Quando uma variável é criada e possui um valor, esse valor é armazenado em algum lugar na memória. A linguagem reconhece onde está a informação através do endereço da memória. Toda variável tem um endereço, e o C possui uma maneira para acessar esse endereço, que é utilizando o & (lembre de e comercial serve para E de endereço). Veja só um exemplo de como podemos imprimir esse endereço:

```c
#include<stdio.h>

int main(void) {
    int a = 23;
    int endereco = &a;

    printf("%d", endereco);
}
```


Esse código vai apresentar alguns avisos (afinal, não é nada seguro imprimir endereços de memória). Mas repare que toda vez que esse código executar, imprimirá um endereço diferente. Isso acontece por que o sistema operacional é quem escolhe quais áreas da memória cada programa recebe.

Repare que já usamos o & toda vez que utilizmos a função scanf. Nela, passamos os endereços das variáveis e é assim que a função scanf sabe onde colocar cada valor de variável.

C possui um modificador de tipo que permite a uma variável armazenar endereços. Para declarar uma variável que guarde o endereço de onde está armazenado um numero inteiro utilize o asterisco antes do nome da variável:

```c
int *end; // Indica que a variável end armazena o endereço de uma informação do tipo inteiro
```

Quando uma variável aramazena um endereço, ela é chamada de ponteiro. No último exemplo, a variável end é um ponteiro de inteiro, pois aponta onde na memória está o inteiro.

Vimos que a função scanf recebe os endereços das variáveis e preenche nelas o valor recebido do teclado. Podemos também alterar o conteúdo mesmo quando só temos acesso ao ponteiro? Sim. Para acessar o conteúdo usamos o * antes da variável.
```c
#include<stdio.h>

int main(void) {
    int a = 23;
    int *endereco = &a;

    *endereco = 15; // Altera o CONTEÚDO, ou seja vai até o endereço armazenado para alterar o conteúdo

    printf("%d", a); // Vai imprimir 15, não o 23
    return 0;
}
```

Algumas situações onde é melhor se trabalhar com ponteiros:
1. Trabalhando com atribuição de texto
    ```c
    #include<stdio.h>

    int main(void) {
        char *texto = "Olá, mundo";
        texto = "Esse é meu novo texto"; // Sem ponteiros, essa atribuição deveria ser feita com strcpy

        printf("%s\n", texto);
        return 0;
    }
    ```
1. Passando arrays para funções, ou retornando delas
    ```c
    #include<stdio.h>

    void imprimePrimeiroElemento( int * array) {
        // Arrays são ponteiros especiais: tem tamanho definido na declaração
        printf("Primeiro elemento: %d\n", array[0]);
    }

    int main (void) {
        int valores [3] = { 29, 30, 31}; // declaração normal de um array

        imprimePrimeiroElemento(valores);
    }
    ```
1. Passando estruturas para dentro ou fora de uma função
    Mas para acessar campos dentro de uma ponteiro de estrutura, troque o ponto "." pela seta "->" (também conhecida como pointer).
    ```c
    #include<stdio.h>

    typedef struct C {
        char * nome;
        int idade;
    } Cadastro;
    /*  **********************************************************************
    Cadastro foi escrito com um C maiúsculo pois em OO existe uma convenção
    que prega que tipos devem começar com letra maiúscula, enquanto variáveis
    devem começar com letras minúsculas.
    ************************************************************************* */
    

    void printJSON(Cadastro * cadastro){
        printf("{\n  \"nome\" : \"%s\",\n  \"idade\" : %d\n}", cadastro->nome, cadastro->idade);
        // Acesso ao nome foi feito usando a seta, cadastro->nome
    }

    int main (void) {
        Cadastro c = {"Joao", 18}; // inicializando na ordem da definição

        printJSON(&c); // passando endereço

        return 0;
    }
    ```
1. Para trabalhar com alocação dinâmica (a seguir!)


## Alocação Dinâmica

Quando declaramos um array, pedimos um espaço com alguns endereços seguidos que cabem uma certa quantidade de dados, a depender do tipo. Um vetor de doubles, por exemplo, vai usar mais memória que um vetor de inteiros.
O que acontece quando queremos que um array aumente ou diminua? Isso resultaria em algum tipo de erro.

### Reservando Espaço
Em C, é possível reservar (ou alocar) espaço em memória durante a execução de um programa, utilizando a função `malloc`. Essa função é um tanto peculiar devido a seu retorno e a seu parâmetro.


Para funcionar, essa função precisa usar um parâmetro que é o tamanho, em bytes, de todo o espaço a ser reservado. Mas nem sempre iremos saber de cabeça o tamanho de cada tipo, especialmente quando estamos trabalhando com estruturas. Para resolver esse problema, usamos a função `sizeof()` como argumento da função. A função sizeof, por sua vez, leva como parâmetro um tipo e ela retorna o tamanho, em bytes, desse tipo. Podemos passar como argumento da malloc o número de elementos multiplicado pelo tamanho de cada elemento.

Outra peculiaridade é que a função malloc retorna um ponteiro genérico, que precisa ser convertido para um ponteiro de tipo específico. Essa conversão é feita através de um recurso denominado cast. Para realizar o cast, à esquerda de um valor, coloque entre parênteses o tipo que se quer converter.

Veja um exemplo de alocação dinâmica:

```c
#include<stdio.h>
#include<stdlib.h> // Biblioteca necessária para o malloc e sizeof

void JSONfy(int * lista) {
    printf("\n[");
    for(int i = 0; i< 4; i++)
        printf("%d, ", lista[i]);
    printf("%d]", lista[4]);
}

int main(void) {
    int * posicoes;

    // Não é necessário pular essas linhas
    posicoes = (int *) // Cast
                malloc( //Reserva memória
                    5 * // Número de elementos a serem reservados
                    sizeof( // Calcula o tamanho em bytes
                        int //Tipo de cada elemento
                    )
                );
    for(int i = 0; i < 5; i++) {
        printf("Digite o valor da posição %d\n", i);
        scanf("%d", &posicoes[i]);
    }

    JSONfy(posicoes);

    return 0;
}
```

### Liberando Espaço

Para liberar espaço, envie o endereço a ser liberado para a função free

```c
#include<stdio.h>
#include<stdlib.h> // Biblioteca necessária para o malloc e sizeof

void JSONfy(int * lista) {
    printf("\n[");
    for(int i = 0; i< 4; i++)
        printf("%d, ", lista[i]);
    printf("%d]", lista[4]);
}

int main(void) {
    int * posicoes;

    // Não é necessário pular essas linhas
    posicoes = (int *) // Cast
                malloc( //Reserva memória
                    5 * // Número de elementos a serem reservados
                    sizeof( // Calcula o tamanho em bytes
                        int //Tipo de cada elemento
                    )
                );
    for(int i = 0; i < 5; i++) {
        printf("Digite o valor da posição %d\n", i);
        scanf("%d", &posicoes[i]);
    }

    JSONfy(posicoes);

    free(posicoes); // LIBERA espaço bem aqui

    return 0;
}
```

## Considerações adicionais

Para se comparar duas strings, utilize o `strcmp`, veja um exemplo:
```c
#include<stdio.h>
#include<string.h>


int main(void) {
    char * texto = "olá";
    char * copia = "olá"; // Troque esse texto por outro para ver o que acontece
    if(strcmp(texto,copia) == 0) // Quando as strings são iguais, o resultado é 0
    {
        printf("Textos Iguais!");
        return 0;
    }
    printf("Textos diferentes");
    return 1; // Sinalização de erro
}
```

Para utilizar exponenciação, utilize a função `pow(base,expoente)` presente na biblioteca `math.h`.

```c
#include<stdio.h>
#include<math.h>

int main(void){
    double base=2, expoente = 10, resultado;

    resultado = pow(base,expoente); // calcula 2^10

    printf("%.0lf^%.0lf = %.0lf\n", base, expoente, resultado);
}
```
Um valor muito crítico para a linguagem C é o valor `NULL`, que equivale ao `None` no Python. **Cuidado para não acessar o conteúdo de ponteiros de valor NULL** para não resultar no terrível **Segmentation fault**. Só atribua valores a variáveis já declaradas, não assuma o conteúdo delas a menos que haja algum tipo de atribuição de valor.
