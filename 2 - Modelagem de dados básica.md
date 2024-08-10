# Ferramentas que iremos utilizar
1 - [Draw.io](https://app.diagrams.net/)
2 - [SQL OnLine IDE (sqliteonline.com)](https://sqliteonline.com/)

## Modelagem de dados
A modelagem de dados em SQL é a criação de um modelo que representa as entidades, atributos e relacionamentos de um banco de dados. Isso envolve identificar quais dados devem ser armazenados em tabelas separadas e definir as associações entre essas tabelas. A modelagem adequada de dados é essencial para garantir a consistência, integridade e eficiência do banco de dados.

## **PK (Primary Key)**
- A ***PRIMARY KEY*** identifica exclusivamente cada registro em uma tabela. Como se fosse um "RG" de cada registro. Cada tabela pode possuir apenas uma Primary Key.
- Sempre olhar para regra de negocio para saber como definir a primary key.

## **Foreign Key**
- A **Foreign Key** é usada para evitar ações que destruiriam links entre tabelas. A foreign key é um campo (ou coleção de campos) em uma tabela, que se refere a PRIMARY KEY de outra tabela.

## **Relacionamentos em Modelagem de Dados:**
Relacionamentos em modelagem de dados descrevem como duas ou mais tabelas em um banco de dados estão conectadas ou relacionadas. Eles ajudam a estruturar os dados de maneira que as tabelas possam interagir corretamente.

### Tipos de Relacionamentos:
1. **1:1 (Um para Um)**:
    - Cada registro em uma tabela está associado a, no máximo, um registro em outra tabela, e vice-versa.
    - **Exemplo:** Se cada cliente tivesse exatamente uma nota fiscal e cada nota fiscal pertencesse a exatamente um cliente, seria um relacionamento 1:1.
2. **1**
    **(Um para Muitos)**:
    - Um registro em uma tabela pode estar associado a vários registros em outra tabela, mas cada registro na segunda tabela está associado a um único registro na primeira.
    - **Exemplo:** Um cliente pode ter várias notas fiscais, mas cada nota fiscal pertence a apenas um cliente. Esse é um relacionamento 1
3. **N**
    **(Muitos para Muitos)**:
    - Vários registros em uma tabela podem estar associados a vários registros em outra tabela.
    - **Exemplo:** Se um cliente pudesse estar relacionado a várias notas fiscais, e cada nota fiscal pudesse incluir informações de vários clientes (algo menos comum para notas fiscais, mas comum em outros contextos), seria um relacionamento N. Para representar isso, normalmente se usa uma tabela intermediária que liga os registros.
4. **1:0..1 (Um para Zero ou Um)**:
    - Um registro em uma tabela pode estar associado a zero ou um registro em outra tabela.
    - **Exemplo:** Se uma nota fiscal opcionalmente tivesse um cliente associado (por exemplo, uma nota fiscal pode ser de um cliente ou não estar associada a nenhum), seria um relacionamento 1:0..1.

Esses relacionamentos ajudam a garantir a integridade dos dados e são essenciais na modelagem para organizar e acessar as informações de forma eficiente.

## No diagrama a baixo desenvolvi um modelo de banco de dados simples para um sistema que guarda notas fiscais.
### Diagrama:
![[Pasted image 20240810182610.png]]

### Comandos SQL para criar as tabelas modeladas acima:
`CREATE TABLE Clientes (`
  `id_cliente INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT,`
  `nome VARCHAR(20),`
  `telefone VARCHAR(15)`
  `);`
  
  `CREATE TABLE Nota_fiscal (`
  `id_nota_fiscal INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT,`
  `numero VARCHAR(20),`
  `valor float,`
  `id_cliente INTEGER,`
  `FOREIGN KEY (id_cliente) REFERENCES Clientes(id_cliente)`
  `);`
  
  `CREATE TABLE Item_Nota_Fiscal (`
  `id_item_nota_fiscal INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT,`
  `nome VARCHAR(20),`
  `descricao VARCHAR(100),`
  `id_nota_fiscal INTEGER,`
  `FOREIGN KEY (id_nota_fiscal) REFERENCES Nota_fiscal(id_nota_fiscal)`
  `);`