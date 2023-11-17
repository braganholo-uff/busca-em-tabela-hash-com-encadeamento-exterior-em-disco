#### Problema 

Implemente a função busca(int cod\_cli, char *nome\_arquivo\_hash, char *nome\_arquivo\_dados, int m) que realiza a busca de clientes em uma Tabela Hash armazenada em disco que usa tratamento de colisão por Encadeamento Exterior. A função recebe o código do cliente a ser buscado, além dos nomes dos dois arquivos que armazenam a tabela Hash e o tamanho m da tabela. O arquivo de hash contém os compartimentos da tabela, e o arquivo de dados contém a lista encadeada. A função de hash a ser usada é h(x) = x mod m.

Veja o slide 15 da aula de [Tratamento de Colisões por Encadeamento Exterior](http://www.ic.uff.br/~vanessa/material/ed/13-TabelasHash-Encadeamento-Exterior.pdf) para entender a estrutura dos arquivos utilizados. 

**É OBRIGATÓRIO** usar o conhecimento da estrutura do arquivo hash para implementar a solução. Soluções que leiam registros desnecessários terão nota modificada para **ZERO**.

São fornecidos arquivos para testes (tabHash.dat e clientes.dat), os quais possuem o seguinte conteúdo e usam hash h(x) = x mod 7: 

```
TABELA HASH:
[0]   0
[1]  -1
[2]   4
[3]   1
[4]  -1
[5]   2
[6]  -1

DADOS:
[  0]  49,         Joao,  -1,  OCUPADO
[  1]  59,        Maria,   3,  OCUPADO
[  2] 103,        Pedro,  -1,  OCUPADO
[  3]   3,        Janio,   5, LIBERADO
[  4]  51,          Ana,  -1,  OCUPADO
[  5]  87,     Mauricio,  -1,  OCUPADO
```

Os valores apresentados em colchetes mostram o **endereço lógico** do registro. São esses endereços lógicos que são usados nos valores dos ponteiros. Note que ponteiros para NULL são representados como -1. No exemplo acima, o compartimento do endereço [2] da tabela Hash aponta para o endereço 4 do arquivo de dados, e lá nesse endereço encontra-se o cliente de chave 51 e nome Ana. O tamanho da tabela (m) nesse exemplo, é 7. Note que 51 mod 7 = 2. 

#### Entrada

- código do cliente
- arquivo hash, que contém os compartimentos da tabela
- arquivo de dados, que contém os registros de clientes armazenados na lista encadeada 

#### Saída 

- a função retorna o endereço (lógico) onde o registro foi encontrado, ou -1 caso não exista registro com aquela chave na tabela.  

Sua função deve imprimir na tela todos os registros acessados ao longo da busca. Para isso, deve-se usar a função imprime\_cliente, disponível no esqueleto de código fornecido nessa avaliação. 

#### Exemplo 1

Assumindo que se deseja busca o cliente de chave **8** e nome **Vanessa**, seu programa deve retornar -1, pois o registro não existe na tabela, e não deve imprimir nenhum registro, pois nenhum registro é acessado (8 mod 7 = 1, e o compartimento 1 tem ponteiro -1, e portanto a lista encadeada associada a esse compartimento está vazia). 

```
REGISTROS ACESSADOS:
RESULTADO: -1
```

#### Exemplo 2: 

Caso o registro buscado esteja marcado como liberado, a função de busca deve retornar -1. Por exemplo, caso seja necessário buscar o cliente de chave **3**, o resultado deve ser o seguinte: 

```
REGISTROS ACESSADOS:
 59,        Maria,   3,  OCUPADO
  3,        Janio,   5, LIBERADO
 87,     Mauricio,  -1,  OCUPADO
RESULTADO: -1
```

#### Exemplo 3

Caso se deseje buscar o registro de chave **103**, o resultado deve ser o seguinte: 

```
REGISTROS ACESSADOS:
103,        Pedro,  -1,  OCUPADO
RESULTADO: 2
```

#### Arquivos a entregar

Entregue apenas o arquivo **encadeamento\_exterior.c**, com sua função de inserção implementada. Os demais arquivos serão adicionados automaticamente pelo Run.Codes na hora da compilação. Por isso é importante que você faça modificações apenas no arquivo encadeamento_exterior.c. 

#### Dicas Importantes: 

- Os arquivos de entrada devem ser colocados dentro da pasta cmake\_build\_debug do projeto caso você esteja usando o CLion
- A entrada e a saída já são tratadas no arquivo fornecido para ler e imprimir os dados no formato esperado pela questão. Vocês devem APENAS implementar a função solicitada no problema
- Não use arquivos .h (coloque todas as definições de tipo no arquivo .c)
- Veja outras dicas em http://www.ic.uff.br/~vanessa/courses/runcodes.html