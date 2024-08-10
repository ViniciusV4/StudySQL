
- O artigo a seguir tem como objetivo te ensinar na pratica e simples como funcionam os seguintes recursos em SQL:
	-  **FUNÇÕES DE AGREGAÇÃO;**
	- **JOIN**, **LEFT JOIN** E **UNION ALL**;
	- **CASE.**
# PARA EXECUTAR A PARTE PRATICA, EXECUTE OS COMANDO A BAIXO. 
**1 - Busque no google por sqllite online ou entre no link ([SQL OnLine IDE (sqliteonline.com)](https://sqliteonline.com/));**
**2 - Crie as tabelas:**
	-- Criar tabela de Fornecedor 
	`CREATE TABLE fornecedor (`
	 `id_fornecedor INTEGER PRIMARY KEY AUTOINCREMENT,`
	 `nome TEXT NOT NULL,` 
	 `email TEXT NOT NULL,` 
	 `telefone TEXT NOT NULL,` 
	 `endereco TEXT NOT NULL );` 
	 
	-- Criar tabela de Produto 
	`CREATE TABLE produto (
	 id_produto INTEGER PRIMARY KEY AUTOINCREMENT, 
	 nome TEXT NOT NULL, valor REAL NOT NULL, 
	 quantidade_estoque INTEGER NOT NULL, 
	 categoria TEXT NOT NULL, 
	 id_fornecedor INTEGER, 
	 FOREIGN KEY (id_fornecedor) REFERENCES fornecedor(id_fornecedor) 
	 );`
**3 - Insira os dados na tabela:**
	-- Inserir registros na tabela Fornecedor 
	`INSERT INTO fornecedor (nome, email, telefone, endereco) VALUES` 
	`('Fornecedor 1', 'fornecedor1@example.com', '1234-5678', 'Rua A, 123'),` 
	`('Fornecedor 2', 'fornecedor2@example.com', '2345-6789', 'Rua B, 456'),` 
	`('Fornecedor 3', 'fornecedor3@example.com', '3456-7890', 'Rua C, 789'),` 
	`('Fornecedor 4', 'fornecedor4@example.com', '4567-8901', 'Rua D, 012');`

`INSERT INTO produto (nome, valor, quantidade_estoque, categoria, id_fornecedor) VALUES` 
	`('Produto 1', 10.00, 100, 'Categoria A', 1),`
	`('Produto 2', 20.00, 150, 'Categoria A', 1),`
	`('Produto 3', 15.00, 200, 'Categoria A', 2),`
	`('Produto 4', 25.00, 250, 'Categoria A', 2),`
	`('Produto 5', 30.00, 50, 'Categoria B', 3),` 
	`('Produto 6', 40.00, 75, 'Categoria B', 3),`
	`('Produto 7', 35.00, 120, 'Categoria B', 4),` 
	`('Produto 8', 45.00, 180, 'Categoria B', 4),`
	`('Produto 9', 50.00, 60, 'Categoria C', 1),`
	`('Produto 10', 55.00, 110, 'Categoria C', 1),`
	`('Produto 11', 60.00, 130, 'Categoria C', 2),` 
	`('Produto 12', 65.00, 140, 'Categoria C', 2),` 
	`('Produto 13', 70.00, 170, 'Categoria D', 3),`
	`('Produto 14', 75.00, 210, 'Categoria D', 3),` 
	`('Produto 15', 80.00, 220, 'Categoria D', 4),`
	`('Produto 16', 85.00, 240, 'Categoria D', 4),` 
	`('Produto 17', 90.00, 300, 'Categoria A', 1),` 
	`('Produto 18', 95.00, 320, 'Categoria B', 2),` 
	`('Produto 19', 100.00, 340, 'Categoria C', 3),` 
	`('Produto 20', 105.00, 360, 'Categoria D', 4);`
	
**4 - FAÇA O INSERT A SEGUIR APENAS QUANDO CHEGAR NO EXEMPLO DE LEFT JOIN:**
-- Inserindo 2 fornecedores novos, eles não vão ter produtos cadastrados na tabela de produto
`INSERT INTO fornecedor (nome, email, telefone, endereco) VALUES` 
`('Fornecedor novo 1', 'fornecedorNovo1@example.com', '1234-5678', 'Rua nova A, 123'),`
`('Fornecedor novo 2', 'fornecedorNovo2@example.com', '1234-5678', 'Rua nova B, 123');`

DEPOIS DE EXECUTAR OS PASSOS 1, 2 E 3, SIGA PARA O CONTEÚDO TEORICO QUE ESTÁ A BAIXO, APROVEITE A VIAGEM!! 🚀

# TÓPICOS
- **FUNÇÕES DE AGREGAÇÃO;**
- **JOIN, LEFT JOIN E UNION ALL;**
- **CASE.**

## FUNÇÕES DE AGREGAÇÃO
**Funções agregadas:**
- **MIN** - Retorna o menor valor da coluna;
	 `SELECT MIN(valor) AS valor_minimo FROM produto;`
	 
- **MAX** - Retorna o maior valor da coluna;
	 `SELECT MAX(valor) AS valor_maximo FROM produto;`
	 
- **SUM** - Retorna a soma dos valores da coluna;
	 `SELECT SUM(valor) as soma_de_todos_os_valores FROM produto;`
	 
- **AVG** - Retorna a média dos valores da coluna;
	 `SELECT SUM(valor) as soma_de_todos_os_valores FROM produto;`
	 
- **COUNT** - Retorna a quantidade de linhas da coluna;
	 `SELECT SUM(valor) as soma_de_todos_os_valores FROM produto;`
	 *A função `COUNT` em SQL não conta valores `NULL` quando aplicada a uma coluna específica.*
	 Aqui também da pra buscar pelo numero da coluna; 
	 
- **COUNT()** - Retorna a quantidade de linhas da tabela.
	 `SELECT COUNT(*) FROM fornecedor;`

## JOIN, LEFT JOIN E UNION ALL
Essas operações são usadas para combinar dados de duas ou mais tabelas em uma condição de junção especificada.

**JOIN** ou **INNER JOIN** - Retorna somente as linhas que tem correspondência em ambas tabelas;

**LEFT JOIN** - Retorna todas as linhas da tabela da esquerda e as correspondentes na tabela da direita, porém preenchendo com nulo quando não houver correspondências.

**UNION ALL** - É utilizada para combinar resultados de duas ou mais consultas em uma única lista de resultados.

### EXEMPLOS:
### Problema - **INNER JOIN** ou **JOIN**:
Uma empresa precisa gerar um relatório que mostre quais produtos cada fornecedor está fornecendo e qual a quantidade disponível em estoque para facilitar o planejamento de compras ou a reposição de mercadorias. Eles querem visualizar essa informação organizada por fornecedor, em ordem alfabética.
A query a seguir pode ser usada para resolver o problema de listar os produtos de cada fornecedor com as seguintes informações: o nome e telefone do fornecedor, o nome do produto e a quantidade em estoque.

`SELECT fornecedor.nome, fornecedor.telefone, produto.nome, produto.quantidade_estoque`
`FROM fornecedor inner JOIN produto` 
`ON fornecedor.id_fornecedor = produto.id_fornecedor`
`order by fornecedor.nome ASC;`

USANDO ***AS*** (renomeia o nome da coluna na exibição, ou seja, não altera no banco, só na exibição):

`SELECT forn.nome, forn.telefone, pdt.nome, pdt.quantidade_estoque`
`FROM fornecedor as forn inner JOIN produto AS pdt` 
`ON forn.id_fornecedor = pdt.id_fornecedor`
`order by forn.nome ASC;`

Você também pode usar operadores lógicos para trazer os valores, *EX*: **AND** e **OR**
**No exemplo a baixo vou trazer apenas os valores que tinham quantidade maior que 100 em estoque.**

SELECT forn.nome, forn.telefone, pdt.nome, pdt.quantidade_estoque
FROM fornecedor as forn inner JOIN produto AS pdt 
ON forn.id_fornecedor = pdt.id_fornecedor
**AND pdt.quantidade_estoque > 100**
order by forn.nome ASC;

**Diferença entre `JOIN` (ou `INNER JOIN`) e `LEFT JOIN`:**
1. **`JOIN` (ou `INNER JOIN`)**:
    - Retorna apenas os registros que têm correspondência em ambas as tabelas.
    - Se um registro na tabela A não tiver um correspondente na tabela B, ele não será incluído no resultado.
    
2. **`LEFT JOIN`**:
    - Retorna todos os registros da tabela A (à esquerda), mesmo que não tenham correspondência na tabela B.
    - Se não houver correspondência, os campos da tabela B retornarão como `NULL`
    

### Exemplo de Problema Resolvido com `LEFT JOIN`:
Imagine que você precisa criar um relatório que mostre todos os fornecedores cadastrados, incluindo aqueles que ainda não têm produtos associados.

**Problema:** A empresa quer saber quais fornecedores ainda não têm produtos registrados no sistema para que o departamento de compras possa entrar em contato com eles e verificar o motivo.

Para resolver esse problema, você usaria um `LEFT JOIN` para garantir que todos os fornecedores apareçam na lista, mesmo que não tenham produtos cadastrados.

**Exemplo de Query:**
`SELECT fornecedor.nome, fornecedor.telefone, produto.nome, produto.quantidade_estoque FROM fornecedor  LEFT JOIN produto ON fornecedor.id_fornecedor = produto.id_fornecedor ORDER BY fornecedor.nome ASC;`

**O que acontece aqui:**
- Todos os fornecedores são listados, mesmo que não tenham nenhum produto cadastrado.
- Se um fornecedor não tiver produtos, os campos `produto.nome` e `produto.quantidade_estoque` aparecerão como `NULL` na saída, indicando a ausência de produtos para aquele fornecedor.

Este tipo de query é essencial quando você precisa incluir todos os registros de uma tabela, independentemente de eles terem correspondência na outra tabela.

**OUTRO EXEMPLO:**
- Criei dois novos fornecedores e não associei nenhum produto a eles.

**JOIN** ou **INNER JOIN:**
![[Pasted image 20240810140041.png]]
***Não retorna valores dos fornecedores novos, porque eles não tem produtos associado*** 

**LEFT JOIN:**
![[Pasted image 20240810140230.png]]
***Retorna o valores da tabela da esquerda (fornecedor) mesmo que eles estejam nulos na outra tabela.***

### **Como funciona o `UNION ALL`:**
O `UNION ALL` combina os resultados de duas ou mais consultas SQL em uma única saída, incluindo todas as linhas de cada consulta, mesmo que elas sejam duplicadas. Diferente do `UNION`, que remove duplicatas, o `UNION ALL` mantém todas as linhas.

### Exemplo de Problema Resolvido com `UNION ALL`:
**Problema:** Uma empresa quer gerar um relatório que mostre tanto os produtos disponíveis no estoque quanto os produtos que foram recentemente descontinuados. As informações de produtos ativos e descontinuados estão em consultas separadas.

Para resolver isso, você pode usar `UNION ALL` para combinar essas duas listas em um único relatório.

**Exemplo de Query:**
`SELECT nome, quantidade_estoque, 'Ativo' AS status FROM produto WHERE quantidade_estoque > 0`  

`UNION ALL`  

`SELECT nome, 0 AS quantidade_estoque, 'Descontinuado' AS status FROM produto WHERE quantidade_estoque = 0;`

**O que acontece aqui:**
- A primeira consulta seleciona produtos que ainda estão em estoque.
- A segunda consulta seleciona produtos descontinuados (sem estoque).
- O `UNION ALL` combina ambas as listas, permitindo que todos os produtos sejam exibidos em um único relatório, incluindo os produtos descontinuados.

Este tipo de query é útil quando você precisa combinar várias fontes de dados sem perder informações, mesmo que existam registros duplicados entre elas.

### **Como funciona o `CASE`:**
O `CASE` é uma estrutura condicional em SQL que permite executar diferentes lógicas em uma consulta, retornando valores diferentes com base em condições especificadas. Ele funciona de maneira semelhante a uma instrução `if-else` em outras linguagens de programação.
### Sintaxe Básica:
`SELECT` 
	`coluna1, coluna2,`     
	`CASE`          
		`WHEN condição1 THEN resultado1`         
		`WHEN condição2 THEN resultado2`         
		`ELSE resultado_padrão`     
	`END AS novo_nome_coluna` 
`FROM tabela;`

- `WHEN` define a condição a ser avaliada.
- `THEN` especifica o valor a ser retornado se a condição for verdadeira.
- `ELSE` (opcional) define o valor a ser retornado se nenhuma das condições for atendida.
- `END` marca o final da estrutura `CASE`.

### Exemplo de Problema Resolvido com `CASE`:
**Problema:** Uma empresa quer categorizar os produtos em um relatório com base na quantidade em estoque. Eles desejam que produtos com mais de 100 unidades sejam marcados como "Alta", entre 50 e 100 como "Média", e menos de 50 como "Baixa".

**Exemplo de Query com `CASE`:**
`SELECT`      
	`nome, quantidade_estoque,`
	`CASE`         
		 `WHEN quantidade_estoque > 100 THEN 'Alta'`         
		 `WHEN quantidade_estoque BETWEEN 50 AND 100 THEN 'Média'`         
		 `ELSE 'Baixa'`     
	`END AS categoria_estoque` 
`FROM produto;`

**O que acontece aqui:**
- A query verifica a quantidade de estoque de cada produto.
- Se a quantidade for maior que 100, o produto é categorizado como "Alta".
- Se a quantidade estiver entre 50 e 100, o produto é categorizado como "Média".
- Se a quantidade for inferior a 50, o produto é categorizado como "Baixa".
- O resultado é uma nova coluna chamada `categoria_estoque` que categoriza cada produto com base na sua quantidade em estoque.

Este tipo de lógica é útil para classificar ou categorizar dados dinamicamente dentro de uma consulta SQL, sem precisar modificar os dados originais na tabela.

**Aqui está um exemplo fictício do retorno que você poderia obter ao executar a query com `CASE`:**

| nome      | quantidade_estoque | categoria_estoque |
| --------- | ------------------ | ----------------- |
| Produto A | 120                | Alta              |
| Produto B | 75                 | Média             |
| Produto C | 45                 | Baixa             |
| Produto D | 150                | Alta              |
| Produto E | 95                 | Média             |
| Produto F | 30                 | Baixa             |
| Produto G | 110                | Alta              |
| Produto H | 65                 | Média             |
| Produto I | 20                 | Baixa             |
| Produto J | 200                | Alta              |
### Explicação:
- **Produto A** tem 120 unidades em estoque, então é categorizado como "Alta".
- **Produto B** tem 75 unidades em estoque, então é categorizado como "Média".
- **Produto C** tem 45 unidades em estoque, então é categorizado como "Baixa".
- E assim por diante...

Essa tabela fictícia pode ser útil para você visualizar como o `CASE` categoriza os dados na coluna `categoria_estoque`.

`**O que é o alias?**` 
`**Qual foi a importancia dele nesses exmplos?**`
## **O que é o `alias`:**
Um `alias` é um nome temporário atribuído a uma tabela ou coluna em uma consulta SQL. Ele é usado para tornar os nomes das colunas ou tabelas mais curtos, mais claros ou para renomear uma coluna calculada.
### Sintaxe do `alias`:
- Para colunas:
    `SELECT coluna AS alias_nome FROM tabela;`
    
- Para tabelas:
    `SELECT coluna1, coluna2 FROM tabela AS alias_nome;`
    
Você pode usar a palavra-chave `AS` para definir o alias, mas ela é opcional em muitos sistemas de banco de dados.

### Importância do `alias` nos exemplos:
Nos exemplos anteriores, o alias foi usado de duas maneiras principais:

1. **Renomeando Colunas**:
    - No exemplo com `CASE`, o alias `categoria_estoque` foi usado para dar um nome à nova coluna que resulta da condição `CASE`.
    - Isso torna a saída mais clara, pois `categoria_estoque` descreve o conteúdo da coluna (a categoria do estoque) de forma compreensível.
3. **Facilitando a Leitura**:
    - Usar alias torna as consultas mais legíveis, especialmente em casos onde o nome original da coluna ou a expressão usada é longa ou complexa.
    - Sem o alias, a coluna resultante de uma expressão `CASE` ou de uma operação matemática pode ter um nome complicado ou indeterminado, dificultando a leitura e interpretação dos resultados.

### Exemplo Sem Alias:
`SELECT`      
	`nome, quantidade_estoque,`     
	`CASE`         
		`WHEN quantidade_estoque > 100 THEN 'Alta'`         
		`WHEN quantidade_estoque BETWEEN 50 AND 100 THEN 'Média'`         
		`ELSE 'Baixa'`     
	`END` 
`FROM produto;`
Sem o alias, a coluna com o resultado do `CASE` não teria um nome claro, o que pode causar confusão ao interpretar o resultado.
### Exemplo Com Alias:
`SELECT`      
	`nome, quantidade_estoque,`     
	`CASE`          
		`WHEN quantidade_estoque > 100 THEN 'Alta'`         
		`WHEN quantidade_estoque BETWEEN 50 AND 100 THEN 'Média'`         
		`ELSE 'Baixa'`     
	`END AS categoria_estoque` 
`FROM produto;`

Com o alias `categoria_estoque`, a consulta fica mais clara e os resultados mais fáceis de entender. Isso é particularmente importante em relatórios ou quando compartilhando os resultados com outras pessoas.