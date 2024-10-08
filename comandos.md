
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

SELECT nome, (CASE 
	   WHEN nota1 >= 5 THEN 'aprovado'
	   WHEN nota1 < 5 THEN 'reprovado'
	END) onibus
FROM Aluno

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

**SELECT nome, (CASE 
	   WHEN nota1 >= 5 THEN 'aprovado'
	   WHEN nota1 < 5 THEN 'reprovado'
	END) aprovado
FROM Aluno**

Esse comando seleciona o nome dos alunos e, com base no valor da nota1, utiliza a estrutura CASE para criar uma nova coluna chamada aprovado. Se a nota1 for maior ou igual a 5, o valor da nova coluna será 'aprovado'; se for menor que 5, será 'reprovado'.

**SELECT COALESCE(nome, '') FROM aluno;**

O comando seleciona a coluna nome da tabela aluno e utiliza a função COALESCE para substituir valores nulos.

**SELECT NULLIF( nota1, 5) as nota_nullif FROM aluno;**

Esse comando compara o valor da coluna nota1 da tabela aluno com o número 5. Se o valor de nota1 for igual a 5, o resultado será NULL.

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

## Index

**CREATE INDEX teste ON aluno (nome)**

Esse comando cria um índice chamado teste na coluna nome da tabela aluno. O índice melhora o desempenho das consultas que filtram ou ordenam os resultados com base na coluna nome, tornando essas operações mais rápidas.

## Function

**CREATE OR REPLACE FUNCTION calcular_media(
    n1 DECIMAL(5,2), 
    n2 DECIMAL(5,2), 
    n3 DECIMAL(5,2), 
    n4 DECIMAL(5,2)
)
RETURNS DECIMAL(5,2) AS $$
BEGIN
    RETURN (n1 + n2 + n3 + n4) / 4.0;
END;
$$ LANGUAGE plpgsql;**

CREATE OR REPLACE FUNCTION calcular_media: Cria uma função chamada calcular_media. Se a função já existir, ela será substituída.
RETURNS DECIMAL(5, 2): Define que a função retorna um valor do tipo DECIMAL(5, 2).
n1, n2, n3, n4: Esses são os parâmetros de entrada da função, representando as notas do aluno.
RETURN (n1 + n2 + n3 + n4) / 4: A função calcula a média somando as quatro notas e dividindo por 4, retornando o resultado.

## Trigger

**CREATE OR REPLACE FUNCTION trigger_calcular_media()
RETURNS TRIGGER AS $$
BEGIN
    -- Calcula a média das notas nota1, nota2, nota3, nota4 e armazena no campo media
    NEW.media := calcular_media(NEW.nota1, NEW.nota2, NEW.nota3, NEW.nota4);
    RETURN NEW;  -- Retorna o novo registro com o valor da média calculada
END;
$$ LANGUAGE plpgsql;**

CREATE OR REPLACE FUNCTION trigger_calcular_media(): Cria uma função de trigger chamada trigger_calcular_media que será executada antes de cada inserção na tabela aluno.
NEW.media := calcular_media(NEW.nota1, NEW.nota2, NEW.nota3, NEW.nota4);: Utiliza a função calcular_media para calcular a média das notas do novo registro que está sendo inserido. O valor é atribuído ao campo media do registro.
RETURN NEW;: Retorna o registro atualizado com a média calculada.

**CREATE TRIGGER trigger_before_insert_media
BEFORE INSERT ON aluno
FOR EACH ROW
EXECUTE FUNCTION trigger_calcular_media();**

CREATE TRIGGER trigger_before_insert_media: Cria uma trigger chamada trigger_before_insert_media.
BEFORE INSERT ON aluno: A trigger será executada antes de uma inserção na tabela aluno.
FOR EACH ROW: A trigger será executada para cada linha (registro) que for inserida.
EXECUTE FUNCTION trigger_calcular_media(): Define que a função trigger_calcular_media será chamada sempre que a trigger for ativada.
