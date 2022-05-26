CREATE DATABASE db_home;

-- TABELA TESTE
CREATE TABLE Teste (
    Id int IDENTITY(1,1) NOT NULL PRIMARY KEY,
    Name nvarchar(255) NOT NULL,
);

INSERT INTO Teste (name)
VALUES ('Marion');


-- MINHA TABELA
CREATE TABLE MinhaTabela  
(  
    MeuDecimal  DECIMAL(5,2),
    MeuNumeric  NUMERIC(10,5)
);  
  
INSERT INTO MinhaTabela VALUES (123, 12345.12);  

SELECT MeuDecimal, MeuNumeric  
FROM MinhaTabela;


-- MINHA TABELA 2
CREATE TABLE MinhaTabela2  
(  
    MeuFloat	FLOAT,
    MeuReal	    REAL
);  
  
INSERT INTO MinhaTabela2 VALUES (123.45, 12345.678);  

SELECT MeuFloat, MeuReal  
FROM MinhaTabela2;


-- MINHA TABELA 3
CREATE TABLE MinhaTabela3  
(  
    MeuMoney		MONEY,
    MeuSmallMoney	SMALLMONEY
);  
 
INSERT INTO MinhaTabela3 VALUES (123, 12345);  

SELECT MeuMoney, MeuSmallMoney  
FROM MinhaTabela3;


-- DATE TIME
DECLARE @date 			date = getdate()
DECLARE @time 			time = getdate()
DECLARE @datetime 		datetime = getdate()
DECLARE @datetime2 		datetime2(4)= getdate()
DECLARE @smalldatetime 	smalldatetime = getdate()

SELECT	@datetime 		as datetime, 
		@datetime2 		as datetime2,
		@smalldatetime 	as smalldatetime,
		@date 		    as date, 
		@time 		    as time


-- DECLARANDO VARIÁVEIS
DECLARE @char char(5), 
        @varchar varchar(20)
SET     @char = 'GUTIERREZ'
SET     @varchar = 'GUTIERREZ'
SELECT  @char, @varchar

DECLARE @teste INT
SET     @teste = 10
SELECT  @teste 

DECLARE @g geography; 
SET     @g = geography::Point(47.65100, -122.34900, 4326)
SELECT  @g.ToString()


-- CRIANDO BANCO DE DADOS ESCOLA
CREATE DATABASE escola;


-- CREATE TABLE SINTAXE
CREATE TABLE Alunos 
(
    codigo CHAR(7) NOT NULL,
    nome VARCHAR(30) NOT NULL,
    dtNasc DATE,
    endereco VARCHAR(30),
    PRIMARY KEY (codigo)
);

CREATE TABLE Disciplinas 
(
    codigo CHAR(7) NOT NULL,
    nome VARCHAR(20) NOT NULL,
    anoCurso CHAR(4),
    depto INT,
    PRIMARY KEY (codigo)
);

CREATE TABLE Inscricoes 
(
    Inscr INT IDENTITY (20210001,1),
    Aluno CHAR(7) NOT NULL,
    Disc CHAR(7) NOT NULL,
    AnoLet CHAR(4),
    PRIMARY KEY (Inscr),
    FOREIGN KEY (Aluno) 	REFERENCES 	ALUNOS(Codigo),
    FOREIGN KEY (Disc) 	REFERENCES 	DISCIPLINAS(Codigo)
);


-- ALTERAR COLUNA
ALTER TABLE Alunos 
ALTER COLUMN nome VARCHAR(50) NOT NULL


SELECT * FROM Alunos, Disciplinas, Inscricoes


-- INSERT INTO ALUNOS
INSERT into Alunos (codigo, nome, dtNasc, endereco)
values (213509, 'Maria das Dores', '30/12/1995', 'Av. Alte Barroso 1500')

INSERT into Alunos (codigo, nome, dtNasc, endereco) 
values (213509, 'Paula Soares', '2020/04/01', 'Av. Alte Barroso 1500');

INSERT into Alunos (codigo, nome, dtNasc, endereco) 
values (213555, 'Maria da Dores', '2020/04/02', 'Av. Alte Barroso 1500');

INSERT into Alunos (codigo, nome, dtNasc, endereco) 
values (213506, 'Dione Gomes   ', '2020/04/03', 'Av. Alte Barroso 1500');

INSERT into Alunos (codigo, nome, dtNasc, endereco) 
values (213507, 'Jose Maria', '2020/04/04', 'Av. Alte Barroso 1500');


-- INSERT INTO DISCIPLINAS
INSERT into disciplinas (codigo, nome, anocurso, depto) 
values ('1', 'QGIS', '2020', 1)

INSERT into disciplinas (codigo, nome, anocurso, depto) 
values ('2', 'PHP', '2020', 1)


-- INSERT INTO INSCRICOES
INSERT INTO Inscricoes (aluno, Disc,anolet) 
Values ('213506', '1', '2020'); 

INSERT INTO Inscricoes (aluno, Disc,anolet) 
Values ('213507', '1', '2020');   

INSERT INTO Inscricoes (aluno, Disc,anolet) 
Values ('213509', '1', '2020'); 


-- ALTERAR UM VALOR DE UMA TABELA
UPDATE Alunos
SET nome = 'Marya Carry'
WHERE codigo = '113503' 

-- DELETAR DA TABELA
DELETE FROM Alunos
WHERE codigo = '213555'


-- EXERCÍCIO - 01]

    -- CRIANDO TABELA CALUNOS
CREATE TABLE Calunos (
    codigo  CHAR(7) NOT NULL,
    nome    VARCHAR(50) NOT NULL,
);

    -- POPULAR TABELA COM DADOS DE ALUNOS
INSERT  into    Calunos
SELECT          codigo, nome
FROM            Alunos

    --  CRIAR NOVO CAMPO
ALTER TABLE     Calunos
ADD             cad_email VARCHAR(30)

    -- INSERIR EMAIL
UPDATE          Calunos
SET             cad_email = TRIM(SUBSTRING(Calunos.nome, 1, 5)) + '@gmail.com'


SELECT * FROM Calunos