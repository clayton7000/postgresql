
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

**SELECT * FROM aluno WHERE nome LIKE  'A%';**

Seleciona todos os registros da tabela aluno onde o nome começa com a letra 'A'. O operador LIKE busca padrões, e o % significa "qualquer sequência de caracteres".

**SELECT * FROM aluno WHERE nome LIKE '%a';**

Seleciona todos os registros da tabela aluno onde o nome termina com a letra 'a'. O % antes da letra 'a' representa qualquer sequência de caracteres anterior.

**SELECT DISTINCT nota1 FROM aluno;**

Seleciona apenas os valores únicos (sem duplicatas) da coluna nota1 na tabela aluno.

**SELECT * FROM aluno LIMIT 10;**

Seleciona os primeiros 10 registros da tabela aluno, limitando o número de resultados retornados.

**SELECT * FROM aluno OFFSET 2 LIMIT 10;**

Pula os dois primeiros registros (OFFSET 2) e seleciona os próximos 10 registros da tabela aluno.

**SELECT * FROM aluno WHERE nota1 in(6,7);**

Seleciona todos os registros da tabela aluno onde o valor da coluna nota1 é igual a 6 ou 7. O operador IN verifica se o valor pertence a uma lista específic

**SELECT * FROM aluno WHERE nota1 not in(6,7);**

Seleciona todos os registros da tabela aluno onde o valor da coluna nota1 não é 6 ou 7.

**SELECT * FROM turma JOIN professor on turma.materia=professor.materia;**

Faz uma junção (INNER JOIN) entre as tabelas turma e professor, retornando apenas os registros onde a coluna materia é igual em ambas as tabelas.

**SELECT turma.nome, professor.nome FROM turma INNER JOIN professor on turma.materia = professor.materia;**

Seleciona os nomes da turma e do professor para todas as matérias que existem em ambas as tabelas, utilizando um INNER JOIN para relacionar as colunas materia.

**SELECT turma.nome, professor.nome FROM turma LEFT JOIN professor on turma.materia = professor.materia;**

Seleciona os nomes da turma e do professor para todas as turmas, retornando todos os registros da tabela turma, mesmo que não haja uma correspondência na tabela professor. Registros sem correspondência no professor terão valores nulos.

**SELECT turma.nome, professor.nome FROM turma RIGHT JOIN professor on turma.materia = professor.materia;**

Seleciona os nomes da turma e do professor, retornando todos os registros da tabela professor, mesmo que não haja uma correspondência na tabela turma. Registros sem correspondência na turma terão valores nulos.

**SELECT turma.nome, professor.nome FROM turma FULL OUTER JOIN professor on turma.materia = professor.materia;**

Seleciona os nomes da turma e do professor, retornando todos os registros tanto da tabela turma quanto da tabela professor, independentemente de haver uma correspondência entre elas. Registros sem correspondência em uma das tabelas terão valores nulos.

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

Cria uma view chamada vw_aluno, que é uma "tabela virtual" baseada nos dados da tabela aluno.

**SELECT * FROM vw_aluno;**

Seleciona todos os registros e colunas da view vw_aluno, que contém as informações dos alunos (id, nome, notas e a média calculada).

**DROP VIEW vw_aluno;**

Remove a view vw_aluno do banco de dados, sem afetar os dados da tabela aluno.
