# Banco de Dados para Ecommerce

## 1. Introdução

Um sistema de vendas online depende de um banco de dados. Esse banco de dados armazena informações cruciais, como produtos, preços, estoque e informações dos clientes. Sem ele, o sistema não funcionaria corretamente. Mas a principal função de um banco de dados de um sistema é armazenar, organizar e gerenciar informações de forma estruturada para permitir o acesso, a recuperação e a manipulação eficientes desses dados conforme necessário pela aplicação ou sistema em questão. Isso facilita a coleta, o armazenamento e a consulta de dados de maneira organizada, tornando possível a realização de tarefas como pesquisa, análise, atualização e geração de relatórios de maneira eficaz e segura.

Neste projeto, estruturei um banco de dados utilizando PostgreSQL, para a um sistema de vendas online de supermercado.

O código está disponível no arquivo `querry.sql` deste repositório.

**Status do Projeto:** Concluído e funcionando perfeitamente.

## 2. Descrição

O banco de dados foi modelado com base nas necessidades do supermercado virtual e apresenta as seguintes tabelas, com os devidos relacionamentos:

![123](https://github.com/JonathanBarr0s/PostgreSQL/assets/132490863/74d715e9-2af8-49c1-81d8-921f25b539cd)

###### *O 1 representa uma chave primária.*

###### *O * representa uma chave estrangeira.*

### 2.1 Chave Primária

Toda tabela poderá possuir uma, e somente uma, chave primária. Essa chave é utilizada como **identificador único** da tabela, sendo representada por aquele campo (ou campos) que não receberá valores repetidos. Suas características são:

1. Chaves primárias **não** podem ser nulas;
2. Cada registro na tabela deve possuir uma, e somente uma, chave primária;
3. Normalmente, chaves primárias são incrementadas automaticamente pelo banco de dados, ou seja, não há necessidade de passarmos esse valor em um INSERT. Entretanto, essa é uma opção configurada na criação da base de dados que não é obrigatória. Nos casos em que ela (incremento automático) não é definida, é preciso garantir que não haverá valores repetidos nessa coluna;
4. São as chaves para o relacionamento entre entidades ou tabelas da base de dados. Assim haverá na tabela relacionada uma **referência** a essa chave primária (que será, na tabela relacionada, a chave estrangeira).

### 2.1 Chave Estrangeira

A chave estrangeira é uma referência em uma tabela a uma chave primária de outra tabela. Diferentemente da chave primária, a chave estrangeira:

1. Pode ser nula;
2. É um campo em uma tabela que faz referência a um campo que é chave primária em outra tabela;
3. É possível ter mais de uma (ou nenhuma) em uma tabela.

## 3. ****Estruturação do Banco de Dados****

O banco de dados apresenta as seguintes tabelas, com os devidos relacionamentos:

### 3.1 Categorias

- **id_categoria** (Chave Primária)
- nome

Essa tabela armazena as categorias de produtos disponíveis no supermercado virtual, como frutas, verduras, massas, bebidas e utilidades.

### 3.2 Produtos

- **id_produto** (Chave Primária)
- nome
- descricao
- preco
- quantidade_em_estoque
- categoria_id (Chave Estrangeira referenciando a tabela **`categorias`**)

A tabela de produtos contém informações detalhadas sobre cada item disponível no supermercado virtual, incluindo nome, descrição, preço, quantidade em estoque e a categoria à qual pertence.

### 3.3 Clientes

- **cpf** (Chave Primária)
- nome

Nessa tabela, são armazenados os dados dos clientes que utilizam o sistema de vendas online, incluindo CPF e nome.

### 3.4 Vendedores

- **cpf** (Chave Primária)
- nome

A tabela de vendedores contém informações sobre os vendedores da empresa, incluindo CPF e nome.

### 3.5 Pedidos

- **id** (Chave Primária)
- valor
- client_cpf (Chave Estrangeira referenciando a tabela **`clientes`**)
- vendedor_cpf (Chave Estrangeira referenciando a tabela `vendedores`)

A tabela pedidos registra o resumo dos pedidos relacionando vendedor e cliente.

## 4 Instalação

Aqui estão os passos para configurar o ambiente e executar o projeto:

1. **Instale o PostgreSQL:**

    O PostgreSQL é um sistema de banco de dados relacional de código aberto. Você pode baixá-lo em **[postgresql.org](https://www.postgresql.org/download/)**.

2. **Instale o Beekeeper Studio:**

    O Beekeeper Studio é um editor SQL e gerenciador de banco de dados. Você pode baixá-lo em **[beekeeperstudio.io](https://www.beekeeperstudio.io/)**.

Ao abrir o Beekeeper, será necessário informar o usuário e senha nos campos destacados, que foram fornecidos durante a instalação do PostgreSQL:
    
![123](https://github.com/JonathanBarr0s/PostgreSQL/assets/132490863/562eaf5f-3658-436e-aa9e-bbc264914894)

## 5 Estruturação

Nesta etapa, irei mostrar os passos para estruturação do banco de dados e farei algumas observações.

### 5.1 Criando a Tabela Clientes

```
create table clientes (
  cpf char(11) primary key,
  nome varchar(150)
);
```

1. **`create table clientes`**: Esta parte da consulta indica que estamos criando uma nova tabela chamada "clientes".
2. **`( cpf char(11) primary key,`**: Aqui, estamos definindo a primeira coluna da tabela chamada "cpf". O tipo de dados da coluna é "char(11)", o que significa que ela armazenará caracteres (letras ou números) com um comprimento fixo de 11 caracteres. Além disso, estamos especificando que esta coluna é a chave primária.
3. **`nome varchar(150)`** : Aqui, estamos definindo a segunda coluna da tabela chamada "nome". O tipo de dados da coluna é "varchar(150)", que é usado para armazenar uma sequência de caracteres com um comprimento máximo de 150 caracteres.

### 5.2 Criando a Tabela Categorias

```
create table categorias (
  id serial primary key,
  nome varchar(50)
);
```
1. **`(id serial primary key)`**: Defina a primeira coluna da tabela como "id" com o tipo de dado "serial", geralmente usado para criar uma coluna de autoincremento. Isso significa que sempre que um novo registro for adicionado à tabela, não será necessário especificar um valor para a coluna "id"; isso será feito automaticamente. A cláusula "primary key" indica que esta coluna será a chave primária da tabela, o que significa que ela conterá valores únicos que identificarão de forma exclusiva cada registro na tabela.

### 5.3 Criando a Tabela Produtos

```
create table produtos (
  id serial primary key,
  nome varchar(100),
  descricao text,
  preco int,
  quantidade_em_estoque int,
  categoria_id int not null references categorias(id)
);
```
1. **`descricao text`**: Define uma terceira coluna chamada "descricao" com o tipo de dados "text", que é usado para armazenar texto longo, como descrições de produtos.
2. **`preco int`**: Define uma quarta coluna chamada "preco" com o tipo de dados "int", que é usado para armazenar valores inteiros.
3. **`categoria_id int not null references categorias(id)`**: Define uma sexta coluna chamada "categoria_id" com o tipo de dados "int". A cláusula "not null" indica que esta coluna não pode conter valores nulos. A parte "references categorias(id)" estabelece uma restrição de chave estrangeira, que vincula a coluna "categoria_id" à coluna "id" de outra tabela chamada "categorias". Isso significa que cada produto deve estar associado a uma categoria existente na tabela "categorias".

## 6 Funcionamento

Agora que o banco de dados foi estruturado, precisamos testá-lo para garatir que esteja funcionando corretamente. Para isso, vamos inserir algumas informações ficticias ao bando de dados:

### 6.1 Inserindo as Categorias:

```
insert into categorias (nome) values ('frutas'), ('verduras'), ('massas'), ('bebibas'), ('utilidades');
```

### 6.2 Inserindo os Produtos:

```
insert into produtos (nome, descricao, preco, quantidade_em_estoque, categoria_id)
values
  ('Mamão', 'Rico em vitamina A, potássio e vitamina C', 300, 123, 1),
  ('Maça', 'Fonte de potássio e fibras.', 90, 34, 1),
  ('Cebola', 'Rico em quercetina, antocianinas, vitaminas do complexo B, C.', 50, 76, 2),
  ('Abacate', 'NÃO CONTÉM GLÚTEN.', 150, 64, 1),
  ('Tomate', 'Rico em vitaminas A, B e C.', 125, 88, 2),
  ('Acelga', 'NÃO CONTÉM GLÚTEN.', 235, 13, 2),
  ('Macarrão parafuso', 'Sêmola de trigo enriquecida com ferro e ácido fólico, ovos e corantes naturais', 690, 5, 3),
  ('Massa para lasanha', 'Uma reunião de família precisa ter comida boa e muita alegria.', 875, 19, 3),
  ('Refrigerante coca cola lata', 'Sabor original', 350, 189, 4),
  ('Refrigerante Pepsi 2l', 'NÃO CONTÉM GLÚTEN. NÃO ALCOÓLICO.', 700, 12, 4),
  ('Cerveja Heineken 600ml', 'Heineken é uma cerveja lager Puro Malte, refrescante e de cor amarelo-dourado', 1200, 500, 4),
  ('Agua mineral sem gás', 'Smartwater é água adicionado de sais mineirais (cálcio, potássio e magnésio) livre de sódio e com pH neutro.', 130, 478, 4),
  ('Vassoura', 'Pigmento, matéria sintética e metal.', 2350, 30, 5),
  ('Saco para lixo', 'Reforçado para garantir mais segurança', 1340, 90, 5),
  ('Escova dental', 'Faça uma limpeza profunda com a tecnologia inovadora', 1000, 44, 5),
  ('Balde para lixo 50l', 'Possui tampa e fabricado com material reciclado', 2290, 55, 5),
  ('Manga', 'Rico em Vitamina A, potássio e vitamina C', 198, 176, 1),
  ('Uva', 'NÃO CONTÉM GLÚTEN.', 420, 90, 1);
```

### 6.3 Inserindo os Clientes:

```
insert into clientes (cpf, nome)
values
  ('80371350042', 'José Augusto Silva'),
  ('67642869061', 'Antonio Oliveira'),
  ('63193310034', 'Ana Rodrigues'),
  ('75670505018', 'Maria da Conceição');
```

### 6.4 Inserindo os Vendedores:

```
insert into vendedores (cpf, nome)
values
  ('82539841031', 'Rodrigo Sampaio'),
  ('23262546003', 'Beatriz Souza Santos'),
  ('28007155023', 'Carlos Eduardo');
```


## 7. Contribuição
Contribuições são bem-vindas! Se você quiser contribuir para este projeto, siga as etapas abaixo:
1. Faça um fork do repositório;
2. Crie uma nova branch: `git checkout -b minha-branch`;
3. Faça suas alterações e faça commit: `git commit -m "Minhas alterações"`;
4. Faça push para o repositório remoto: `git push origin minha-branch`;
5. Envie um Pull Request.

## Licença
Este projeto está licenciado sob a licença nenhuma.
