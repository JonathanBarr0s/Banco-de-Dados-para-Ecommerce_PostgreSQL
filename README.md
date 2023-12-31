# Banco de Dados para Ecommerce

## 1. Introdução

Um sistema de vendas online depende de um banco de dados. Esse banco de dados armazena informações cruciais, como produtos, preços, estoque e informações dos clientes. Sem ele, o sistema não funcionaria corretamente. Mas a principal função de um banco de dados de um sistema é armazenar, organizar e gerenciar informações de forma estruturada para permitir o acesso, a recuperação e a manipulação eficientes desses dados conforme necessário pela aplicação ou sistema em questão. Isso facilita a coleta, o armazenamento e a consulta de dados de maneira organizada, tornando possível a realização de tarefas como pesquisa, análise, atualização e geração de relatórios de maneira eficaz e segura.

Neste projeto, estruturei um banco de dados utilizando PostgreSQL, para a um sistema de vendas online de supermercado.

O código está disponível no arquivo `querry.sql` deste repositório.

**Status do Projeto:** Concluído e funcionando perfeitamente.

## 2. Descrição

O banco de dados foi modelado com base nas necessidades do supermercado virtual e apresenta as seguintes tabelas, com os devidos relacionamentos:

![Tabela](https://github.com/JonathanBarr0s/Banco-de-Dados-para-Ecommerce_PostgreSQL/assets/132490863/78abfe61-8b05-4c52-a97d-e54b50526373)

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
    
![Captura de tela 2023-10-09 133233](https://github.com/JonathanBarr0s/Banco-de-Dados-para-Ecommerce_PostgreSQL/assets/132490863/e97f0507-5b49-44f5-bfe8-1a49e27b1931)

## 5 Estruturação

Nesta etapa, irei mostrar os passos para a estruturação do banco de dados e farei algumas observações.

Um ponto importante é que, antes de criar uma tabela B que possui uma **chave estrangeira**, é necessário primeiro criar a tabela A que possui a **chave primária** à qual a tabela B irá se referenciar. Isso ocorre porque não é possível criar uma chave estrangeira para uma chave primária de uma tabela que ainda não existe.

No Beekeeper, a chave primária é ilustrada na cor azul, no cabeçalho da coluna, e a chave estrangeira na cor amarela.

### 5.1 Criando o Banco de Dados

```
create database ecommerce;
```

![1](https://github.com/JonathanBarr0s/Banco-de-Dados-para-Ecommerce_PostgreSQL/assets/132490863/7ab29847-7c48-47b2-8d7e-cd0e04eb15d9)

1. Quando essa consulta é executada, um novo banco de dados vazio chamado "ecommerce" será criado. Esse banco de dados poderá, então, armazenar as tabelas que vamos criar logo abaixo.

### 5.2 Criando a Tabela Clientes

```
create table clientes (
  cpf char(11) primary key,
  nome varchar(150)
);
```
![2](https://github.com/JonathanBarr0s/Banco-de-Dados-para-Ecommerce_PostgreSQL/assets/132490863/5bdbeb9e-f9de-4eda-a17b-491ce431eaa4)

1. **`create table clientes`**: Esta parte da consulta indica que estamos criando uma nova tabela chamada "clientes".
2. **`( cpf char(11) primary key,`**: Aqui, estamos definindo a primeira coluna da tabela chamada "cpf". O tipo de dados da coluna é "char(11)", o que significa que ela armazenará caracteres (letras ou números) com um comprimento fixo de 11 caracteres. Além disso, estamos especificando que esta coluna é a chave primária.
3. **`nome varchar(150)`** : Aqui, estamos definindo a segunda coluna da tabela chamada "nome". O tipo de dados da coluna é "varchar(150)", que é usado para armazenar uma sequência de caracteres com um comprimento máximo de 150 caracteres.

### 5.3 Criando a Tabela Categorias

```
create table categorias (
  id serial primary key,
  nome varchar(50)
);
```
![3](https://github.com/JonathanBarr0s/Banco-de-Dados-para-Ecommerce_PostgreSQL/assets/132490863/0fd5d2f5-1d84-48c6-bd58-8614e90fa850)

1. **`(id serial primary key)`**: Defina a primeira coluna da tabela como "id" com o tipo de dado "serial", geralmente usado para criar uma coluna de autoincremento. Isso significa que sempre que um novo registro for adicionado à tabela, não será necessário especificar um valor para a coluna "id"; isso será feito automaticamente. 

### 5.4 Criando a Tabela Produtos

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
![4](https://github.com/JonathanBarr0s/Banco-de-Dados-para-Ecommerce_PostgreSQL/assets/132490863/d15b5302-0335-4197-9f72-8f186fd915f3)

1. **`descricao text`**: Define uma terceira coluna chamada "descricao" com o tipo de dados "text", que é usado para armazenar texto longo, como descrições de produtos.
2. **`preco int`**: Define uma quarta coluna chamada "preco" com o tipo de dados "int", que é usado para armazenar valores inteiros.
3. **`categoria_id int not null references categorias(id)`**: Define uma sexta coluna chamada "categoria_id" com o tipo de dados "int". A cláusula "not null" indica que esta coluna não pode conter valores nulos. A parte "references categorias(id)" estabelece uma restrição de chave estrangeira, que vincula a coluna "categoria_id" à coluna "id" de outra tabela chamada "categorias". Isso significa que cada produto deve estar associado a uma categoria existente na tabela "categorias".

### 5.5 Criando a Tabela Vendedores

```
create table vendedores (
  cpf char(11) primary key,
  nome varchar(150)
);
```
![5](https://github.com/JonathanBarr0s/Banco-de-Dados-para-Ecommerce_PostgreSQL/assets/132490863/d8260573-30df-47b5-939b-ceba40edaf97)

### 5.6 Criando a Tabela Pedidos

```
create table pedidos (
  id serial primary key,
  valor int,
  client_cpf char(11) not null references clientes(cpf),
  vendedor_cpf char(11) not null references vendedores(cpf)
);
```
![6](https://github.com/JonathanBarr0s/Banco-de-Dados-para-Ecommerce_PostgreSQL/assets/132490863/258714c1-2626-4baa-9798-71a3e04bc3eb)

### 5.7 Criando a Tabela Itens do Pedido

```
create table itens_do_pedido (
 id serial primary key,
  pedido_id int not null references pedidos(id),
  quantidade int,
  produto_id int not null references produtos(id)
);
```
![7](https://github.com/JonathanBarr0s/Banco-de-Dados-para-Ecommerce_PostgreSQL/assets/132490863/dd302bd4-8484-4e9a-8993-5e8afb60e12b)

## 6 Funcionamento

Agora que o banco de dados foi estruturado, precisamos testá-lo para garantir que esteja funcionando corretamente. Para isso, vamos inserir algumas informações fictícias:

### 6.1 Inserindo as Categorias:

```
insert into categorias (nome) values ('frutas'), ('verduras'), ('massas'), ('bebibas'), ('utilidades');
```
![8](https://github.com/JonathanBarr0s/Banco-de-Dados-para-Ecommerce_PostgreSQL/assets/132490863/f7308dc3-8816-47fe-b486-95d46ae7cfff)

1. **`insert into categorias`**: Isso indica que vamos inserir dados na tabela "categorias".
2. **`(nome)`**: Esta parte entre parênteses especifica a lista de colunas nas quais vamos inserir valores. Neste caso, vamos inserir valores apenas na coluna "nome".
3. **`values ('frutas'), ('verduras'), ('massas'), ('bebidas'), ('utilidades');`**: Esta é a lista de valores que serão inseridos na coluna "nome" da tabela "categorias". 

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
![9](https://github.com/JonathanBarr0s/Banco-de-Dados-para-Ecommerce_PostgreSQL/assets/132490863/ca2ea841-9f8a-4556-84cf-abbe99510d43)

### 6.3 Inserindo os Clientes:

```
insert into clientes (cpf, nome)
values
  ('80371350042', 'José Augusto Silva'),
  ('67642869061', 'Antonio Oliveira'),
  ('63193310034', 'Ana Rodrigues'),
  ('75670505018', 'Maria da Conceição');
```
![10](https://github.com/JonathanBarr0s/Banco-de-Dados-para-Ecommerce_PostgreSQL/assets/132490863/486a2b64-50af-4c7b-8911-6c60675011a6)

### 6.4 Inserindo os Vendedores:

```
insert into vendedores (cpf, nome)
values
  ('82539841031', 'Rodrigo Sampaio'),
  ('23262546003', 'Beatriz Souza Santos'),
  ('28007155023', 'Carlos Eduardo');
```
![11](https://github.com/JonathanBarr0s/Banco-de-Dados-para-Ecommerce_PostgreSQL/assets/132490863/f443909e-1678-4e79-8026-771ba0edb00e)

## 7. Registrando Pedidos

Agora que o banco de dados está alimentado, é hora de simular algumas vendas.

As ações abaixo serão realizadas de forma automática pelo próprio sistema, mas para fins de teste, vamos criar alguns registros fictícios:

### 7.1 Inserindo o Primeiro Registro:

1. Primeiro, vamos registrar o pedido na tabela Pedidos:

```
insert into pedidos (valor, client_cpf, vendedor_cpf) values (9650, '80371350042', '28007155023');
```

2. Com o pedido registrado, podemos inserir os primeiros registros na tabela Itens do Pedido:

```
insert into itens_do_pedido (quantidade, pedido_id, produto_id)
values
(1, 1, 1),
(1, 1, 10),
(6, 1, 11),
(1, 1, 15),
(5, 1, 2);
```

3. Após concluir a venda, precisamos atualizar o estoque:

```
update produtos set quantidade_em_estoque = quantidade_em_estoque - 1 where id = 10;

update produtos set quantidade_em_estoque = quantidade_em_estoque - 1 where id = 1;

update produtos set quantidade_em_estoque = quantidade_em_estoque - 5 where id = 2;

update produtos set quantidade_em_estoque = quantidade_em_estoque - 1 where id = 15;

update produtos set quantidade_em_estoque = quantidade_em_estoque - 6 where id = 11;
```

1. **`update produtos`**: Isso indica que vamos executar uma operação de atualização na tabela "produtos".
2. **`set quantidade_em_estoque = quantidade_em_estoque - 1`**: Esta parte da consulta especifica a atualização que será feita. Ela está diminuindo a coluna "quantidade_em_estoque" em 1 unidade. 
3. **`where id = 10;`**: O "where" é usado para definir uma condição para a atualização. Neste caso, a atualização só ocorrerá se a coluna "id" for igual a 10. Isso significa que somente o registro com "id" igual a 10 terá sua quantidade em estoque diminuída em 1. 

## 8. Contribuição
Contribuições são bem-vindas! Se você quiser contribuir para este projeto, siga as etapas abaixo:
1. Faça um fork do repositório;
2. Crie uma nova branch: `git checkout -b minha-branch`;
3. Faça suas alterações e faça commit: `git commit -m "Minhas alterações"`;
4. Faça push para o repositório remoto: `git push origin minha-branch`;
5. Envie um Pull Request.

## Licença
Este projeto está licenciado sob a licença nenhuma.
