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

## 4 Instalação

Aqui estão os passos para configurar o ambiente e executar o projeto:

1. **Instale o PostgreSQL:**

    O PostgreSQL é um sistema de banco de dados relacional de código aberto. Você pode baixá-lo em **[postgresql.org](https://www.postgresql.org/download/)**.

2. **Instale o Beekeeper Studio:**

    O Beekeeper Studio é um editor SQL e gerenciador de banco de dados. Você pode baixá-lo em **[beekeeperstudio.io](https://www.beekeeperstudio.io/)**.

Ao abrir o Beekeeper, será necessário informar o usuário e senha nos campos destacados, que foram fornecidos durante a instalação do PostgreSQL:
    
![123](https://github.com/JonathanBarr0s/PostgreSQL/assets/132490863/562eaf5f-3658-436e-aa9e-bbc264914894)

## 5 Funcionamento

## 6. Contribuição
Contribuições são bem-vindas! Se você quiser contribuir para este projeto, siga as etapas abaixo:
1. Faça um fork do repositório;
2. Crie uma nova branch: `git checkout -b minha-branch`;
3. Faça suas alterações e faça commit: `git commit -m "Minhas alterações"`;
4. Faça push para o repositório remoto: `git push origin minha-branch`;
5. Envie um Pull Request.

## Licença
Este projeto está licenciado sob a licença nenhuma.
