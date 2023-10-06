# Banco de Dados para Ecommerce

## 1. Introdução

Um sistema de vendas online depende de um banco de dados. Esse banco de dados armazena informações cruciais, como produtos, preços, estoque e informações dos clientes. Sem ele, o sistema não funcionaria corretamente. Mas a principal função de um banco de dados de um sistema é armazenar, organizar e gerenciar informações de forma estruturada para permitir o acesso, a recuperação e a manipulação eficientes desses dados conforme necessário pela aplicação ou sistema em questão. Isso facilita a coleta, o armazenamento e a consulta de dados de maneira organizada, tornando possível a realização de tarefas como pesquisa, análise, atualização e geração de relatórios de maneira eficaz e segura.

Neste projeto, estruturei um banco de dados utilizando PostgreSQL, para a um sistema de vendas online de supermercado.

O código está disponível no arquivo `querry.sql` deste repositório.

**Status do Projeto:** Concluído e funcionando perfeitamente.

## 2. Descrição

O banco de dados foi modelado com base nas necessidades do supermercado virtual e apresenta as seguintes tabelas, com os devidos relacionamentos:

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0ce68c8e-9dd9-477b-a9fe-c66e5175566e/130b891a-f3bb-42a1-a2b8-1d3619ec2695/Untitled.png)

###### *O 1 representa uma chave primária.*

###### *O * representa uma chave estrangeira.*

### 2.1 Chave Primária

Toda tabela poderá possuir uma, e somente uma, chave primária. Essa chave é utilizada como **identificador único** da tabela, sendo representada por aquele campo (ou campos) que não receberá valores repetidos. Suas características são:

1. Chaves primárias **não** podem ser nulas;
2. Cada registro na tabela deve possuir uma, e somente uma, chave primária;
3. Normalmente, chaves primárias são incrementadas automaticamente pelo banco de dados, ou seja, não há necessidade de passarmos esse valor em um **[INSERT](http://www.devmedia.com.br/comandos-basicos-em-sql-insert-update-delete-e-select/37170)**. Entretanto, essa é uma opção configurada na criação da base de dados que não é obrigatória. Nos casos em que ela (incremento automático) não é definida, é preciso garantir que não haverá valores repetidos nessa coluna;
4. São as chaves para o relacionamento entre entidades ou tabelas da base de dados. Assim haverá na tabela relacionada uma **referência** a essa chave primária (que será, na tabela relacionada, a chave estrangeira).

### 2.1 Chave Estrangeira

A chave estrangeira é uma referência em uma tabela a uma chave primária de outra tabela. Diferentemente da chave primária, a chave estrangeira:

1. Pode ser nula (NOT NULL);
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

- **cpf** (Chave Primária, com restrição de não aceitar registros duplicados)
- nome

Nessa tabela, são armazenados os dados dos clientes que utilizam o sistema de vendas online, incluindo CPF e nome.

### 3.4 Vendedores

- **cpf** (Chave Primária, com restrição de não aceitar registros duplicados)
- nome

A tabela de vendedores contém informações sobre os vendedores da empresa, incluindo CPF e nome.

### 3.5 Pedidos

- **id** (Chave Primária)
- valor
- client_cpf (Chave Estrangeira referenciando a tabela **`clientes`**)
- vendedor_cpf (Chave Estrangeira referenciando a tabela `vendedores`)

A tabela pedidos registra o resumo dos pedidos relacionando vendedor e cliente.
