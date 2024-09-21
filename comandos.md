
# Comandos Postgresql


## Select

**SELECT * FROM aluno;**

Seleciona todos os registros e colunas da tabela 'aluno'.

**SELECT nome, nota1 FROM aluno;**

Seleciona apenas as colunas 'nome' e 'nota1' de todos os registros da tabela 'aluno'.

**SELECT nome, nota1 FROM aluno WHERE nota1 > 5;**

Seleciona 'nome' e 'nota1' de alunos cuja 'nota1' é maior que 5.

**SELECT nome, nota1 FROM aluno ORDER BY nota1 ASC;**

Seleciona 'nome' e 'nota1' e ordena os resultados pela 'nota1' em ordem crescente (ASC).

**SELECT nome, nota1 FROM aluno ORDER BY nota1 DESC;**

Seleciona 'nome' e 'nota1' e ordena os resultados pela 'nota1' em ordem decrescente (DESC).

**SELECT AVG(nota1) FROM aluno;**

Calcula a média (AVG) de 'nota1' de todos os alunos na tabela 'aluno'.

**SELECT MIN(nota1) FROM aluno;**

Retorna o menor valor (MIN) da coluna 'nota1' entre todos os alunos.

**SELECT SUM(nota1) FROM aluno;**

Calcula a soma total (SUM) de todas as notas da coluna 'nota1' dos alunos.

**SELECT COUNT(*) FROM aluno;**

Conta o número total de registros (COUNT) na tabela 'aluno'.

**SELECT nome FROM aluno UNION SELECT nome FROM professor;**

Seleciona os nomes dos alunos e professores, removendo duplicatas e retornando um conjunto único de nomes presentes nas duas tabelas.

## View

**CREATE VIEW vw_aluno AS
SELECT 
    id, 
    nome, 
    nota1, 
    nota2, 
    nota3, 
    nota4, 
    (nota1 + nota2 + nota3 + nota4) / 4.0 AS media
FROM aluno;**

**SELECT * FROM vw_aluno;**

**DROP VIEW vw_aluno;**


SELECT * FROM aluno WHERE nome LIKE  'A%';
SELECT * FROM aluno WHERE nome LIKE '%a';
