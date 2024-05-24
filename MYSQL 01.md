Tabelas: Armazenam dados em linhas e colunas, organizando as informações de maneira estruturada.

Views: São consultas pré-definidas que retornam resultados como se fossem tabelas, úteis para simplificar consultas complexas ou ocultar dados sensíveis.

Procedures: São blocos de código SQL que podem aceitar parâmetros e executar uma série de operações, podendo ser reutilizáveis.

Functions: Semelhantes às procedures, mas retornam um valor específico e são usadas principalmente em consultas SQL.

Índices: Estruturas que melhoram o desempenho das consultas ao agilizar a busca por registros específicos em uma tabela.

Triggers: São ações automáticas que ocorrem em resposta a eventos específicos, como a inserção, atualização ou exclusão de registros em uma tabela.

Sequences: Geram números sequenciais automaticamente, úteis para criar chaves primárias únicas ou identificadores exclusivos.

Índices Compostos: Índices que envolvem múltiplas colunas em uma tabela para melhorar o desempenho de consultas complexas.

Chaves Estrangeiras (Foreign Keys): Restrições que estabelecem uma relação entre duas tabelas, garantindo a integridade referencial dos dados.

Visões Materializadas (Materialized Views): São visões que armazenam fisicamente os resultados de uma consulta, sendo atualizadas periodicamente para refletir alterações nos dados originais.

Sinônimos: São apelidos para objetos de banco de dados, facilitando o acesso a esses objetos sem precisar especificar o esquema ou nome completo.

Partições: Divisões lógicas ou físicas de uma tabela em subconjuntos menores, o que pode melhorar o desempenho e facilitar a administração de grandes conjuntos de dados.

Triggers de Auditoria: Triggers específicas para registrar e auditar alterações em dados sensíveis, como quem fez a alteração e quando.

Índices Bitmap: Índices otimizados para consultas que envolvem múltiplas colunas com baixa cardinalidade, como em campos booleanos ou enumerações.



Criando um BD: exemplo [create database alura_curso;] ou [CREATE SCHEMA `alura` DEFAULT CHARACTER SET utf8 ;]

        CREATE {DATABASE | SCHEMA} [IF NOT EXISTS] db_name
            [create_option] ...

        create_option: [DEFAULT] {
            CHARACTER SET [=] charset_name
        | COLLATE [=] collation_name
        | ENCRYPTION [=] {'Y' | 'N'}
        }

Apagando um BD: [drop database alura_curso;]

Comandos via linha de comando mysql:
        mysql> USE jogoteca;
        Database changed
        mysql> select * from jogos;
        +----+-----------------+----------------+---------+
        | id | nome            | categoria      | console |
        +----+-----------------+----------------+---------+
        |  1 | Tetris          | Puzzle         | Atari   |
        |  2 | God of War      | Hack and Slash | PS2     |
        |  3 | Mortal Kombat I | Luta           | PS2     |
        |  4 | Need for Speed  | HCorrida       | PC      |
        +----+-----------------+----------------+---------+
        4 rows in set (0.00 sec)

        mysql> SELECT DATABASE();
        +------------+
        | DATABASE() |
        +------------+
        | jogoteca   |
        +------------+
        1 row in set (0.00 sec)


Criando tabelas:
    create table `sucos`.`tbCliente`     -- base.Tabela
    (CPF varchar(11),          -- Colunas
    NOME varchar(100),
    ENDERECO1 varchar(150),
    ENDERECO2 varchar(150),
    BAIRRO varchar(50),
    CIDADE varchar(50),
    ESTADO varchar(50),
    CEP varchar(8),
    IDADE SMALLINT,
    SEXO varchar(1),
    LIMITE_CREDITO FLOAT,
    VOLUME_COMPRA FLOAT,
    PRIMEIRA_COMPRA BIT(1))


Apagando tabelas:
    DROP TABLE `sucos`.`tbcliente3`;


Inserindo conteudo na tabela:
use sucos;

insert into tbproduto (
PRODUTO, NOME, EMBALAGEM,TAMANHO, SABOR,PRECO_LISTA) values (
'1037797','Clean - 2 Litros - Laranja', 'lata', '2 Litros','Laranja',16.01);
insert into tbproduto (
PRODUTO, NOME, EMBALAGEM,TAMANHO, SABOR,PRECO_LISTA) values (
'1000889','Sabor da montanha- 700 ml - Uva', 'Garrafa', '700 ml','Uva',6.31);

select * from tbproduto;



Atualizando conteudo na tabela:
UPDATE tbproduto SET EMBALAGEM = 'PET', PRECO_LISTA = 10.00 WHERE PRODUTO = '1037797';

Excluindo conteudo na tabela:
DELETE FROM tbproduto where PRODUTO = '1000889';

Criando chave primária:
ALTER TABLE tbproduto add primary key (PRODUTO);

Criando nova coluna:
ALTER TABLE tbcliente add column (DATA_NASCIMENTO DATE);


tipo data: '1989-02-01'

insert into tbcliente (CPF, NOME, ENDERECO1, ENDERECO2, BAIRRO, CIDADE, ESTADO, CEP, IDADE, SEXO, LIMITE_CREDITO, VOLUME_COMPRA, PRIMEIRA_COMPRA, DATA_NASCIMENTO) 
value ('12311120011', 'Ramon Tester', 'Rua testes', 'Numero 19', 'POSSE', 'RJ', 'RJ', '2332123', '35', 'M', 10000.00, 2000, 0, '1989-02-01')

Selects:
select * from tbproduto;
select CPF, NOME, SEXO from tbcliente;
select CPF, NOME, SEXO from tbcliente LIMIT 2;
select CPF as CLI_CPF, NOME as CLI_NOME, SEXO from tbcliente;

Filtrando registros:
select * from tbproduto where EMBALAGEM = 'PET';
select * from tbproduto where SABOR = 'Laranja' AND EMBALAGEM = 'PET';
update tbproduto set EMBALAGEM = 'PETT' where SABOR = 'Laranja' AND EMBALAGEM = 'PET';
select * from tbproduto where SABOR = 'Laranja' OR EMBALAGEM = 'PET';   OR = OU


Calculando em filtro:
select * from tbcliente where IDADE = 22;
select * from tbcliente where IDADE > 22;
select * from tbcliente where IDADE >= 22; Maior e Igual
select * from tbcliente where IDADE <= 22;
select * from tbcliente where IDADE < 22;
select * from tbcliente where IDADE <> 22;  Diferente
select * from tbcliente where IDADE BETWEEN 22 and 23;  entre

FLOAT(1.2222) não funciona com =

Filtro com data:
select * from tbcliente where DATA_NASCIMENTO > '1995-01-13';
select * from tbcliente where YEAR(DATA_NASCIMENTO) = 1995;


# Exemplo de consulta

select JSON_EXTRACT(doc, "$.government.HeadOfState") as HeadOfState,
SUM( JSON_EXTRACT(doc, "$.geography")) as geography,  # Somar
AVG( JSON_EXTRACT(doc, "$.geography")) as geography from countryinfo  # MEDIA
WHERE JSON_EXTRACT(doc, "$.geography")) LIKE ('%exempl%)  # Quando (filtro)
AND JSON_EXTRACT(doc, "$.geography"))  >= 10000000 # e quando (filtro)
GROUP BY JSON_EXTRACT(doc, "$.geofraphgy.Continent") # Agrupando por
ORDER BY 2; # Ordene





