# Desafio-de-modelagem-e-implementac-a-o-de-um-banco-de-dados


- Veículo (ID, Placa, Modelo, Ano)
- Cliente (ID, Nome, Endereço, Telefone)
- Ordem de Serviço (ID, ID Veículo, ID Cliente, Data, Valor)
- Serviço (ID, Nome, Valor)
- Peça (ID, Nome, Valor)
- Ordem de Serviço-Serviço (ID, ID Ordem de Serviço, ID Serviço)
- Ordem de Serviço-Peça (ID, ID Ordem de Serviço, ID Peça)

Esquema Lógico


CREATE TABLE Veiculo (
  ID INT PRIMARY KEY,
  Placa VARCHAR(10),
  Modelo VARCHAR(50),
  Ano INT
);

CREATE TABLE Cliente (
  ID INT PRIMARY KEY,
  Nome VARCHAR(100),
  Endereço VARCHAR(200),
  Telefone VARCHAR(20)
);

CREATE TABLE Ordem_de_Servico (
  ID INT PRIMARY KEY,
  ID_Veiculo INT,
  ID_Cliente INT,
  Data DATE,
  Valor DECIMAL(10, 2),
  FOREIGN KEY (ID_Veiculo) REFERENCES Veiculo(ID),
  FOREIGN KEY (ID_Cliente) REFERENCES Cliente(ID)
);

CREATE TABLE Servico (
  ID INT PRIMARY KEY,
  Nome VARCHAR(100),
  Valor DECIMAL(10, 2)
);

CREATE TABLE Peca (
  ID INT PRIMARY KEY,
  Nome VARCHAR(100),
  Valor DECIMAL(10, 2)
);

CREATE TABLE Ordem_de_Servico_Servico (
  ID INT PRIMARY KEY,
  ID_Ordem_de_Servico INT,
  ID_Servico INT,
  FOREIGN KEY (ID_Ordem_de_Servico) REFERENCES Ordem_de_Servico(ID),
  FOREIGN KEY (ID_Servico) REFERENCES Servico(ID)
);

CREATE TABLE Ordem_de_Servico_Peca (
  ID INT PRIMARY KEY,
  ID_Ordem_de_Servico INT,
  ID_Peca INT,
  FOREIGN KEY (ID_Ordem_de_Servico) REFERENCES Ordem_de_Servico(ID),
  FOREIGN KEY (ID_Peca) REFERENCES Peca(ID)
);


Queries SQL

1. Recuperações simples com SELECT Statement


SELECT * FROM Veiculo;


2. Filtros com WHERE Statement


SELECT * FROM Ordem_de_Servico WHERE Valor > 100;


3. Crie expressões para gerar atributos derivados


SELECT *, Valor * 1.1 AS Valor_Com_Imposto FROM Ordem_de_Servico;


4. Defina ordenações dos dados com ORDER BY


SELECT * FROM Ordem_de_Servico ORDER BY Valor DESC;


5. Condições de filtros aos grupos – HAVING Statement


SELECT ID_Cliente, SUM(Valor) AS Total_Gasto
FROM Ordem_de_Servico
GROUP BY ID_Cliente
HAVING SUM(Valor) > 500;


6. Crie junções entre tabelas para fornecer uma perspectiva mais complexa dos dados


SELECT *
FROM Ordem_de_Servico
JOIN Veiculo ON Ordem_de_Servico.ID_Veiculo = Veiculo.ID
JOIN Cliente ON Ordem_de_Servico.ID_Cliente = Cliente.ID;

