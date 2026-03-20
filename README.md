CREATE DATABASE produtos_limpeza;

USE produtos_limpeza;

CREATE TABLE Produto(
	id INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(50) NOT NULL,
    id_categoria int NOT NULL,
    dt_fabricacao DATE NOT NULL,
    dt_vencimento DATE NOT NULL,
    preco FLOAT NOT NULL,
    id_fornecedor INT NOT NULL,
    FOREIGN KEY(id_fornecedor) REFERENCES Fornecedor(id),
    FOREIGN KEY(id_categoria) REFERENCES Categoria(id)
);

CREATE TABLE Categoria(
	id INT PRIMARY KEY AUTO_INCREMENT,
    categoria VARCHAR(50) NOT NULL
);

CREATE TABLE Cliente(
	id INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(50) NOT NULL,
    id_endereco INT NOT NULL,
    telefone VARCHAR(12) NOT NULL,
    filiação VARCHAR(50) NOT NULL,
    id_status INT NOT NULL,
    limite_credito FLOAT NOT NULL,
    FOREIGN KEY(id_endereco) REFERENCES Endereco(id),
    FOREIGN KEY(id_status) REFERENCES Status(id)
);

CREATE TABLE Status(
	id INT PRIMARY KEY AUTO_INCREMENT,
    status VARCHAR(5)
);

CREATE TABLE Endereco(
	id INT PRIMARY KEY AUTO_INCREMENT,
    rua VARCHAR(30) NOT NULL,
    numero INT NOT NULL,
    cidade VARCHAR(30) NOT NULL,
    cep VARCHAR(15) NOT NULL,
    uf VARCHAR(15) NOT NULL
);

CREATE TABLE Pedido(
	id INT PRIMARY KEY AUTO_INCREMENT,
    data_pedido DATE NOT NULL,
    qtd_produtos INT NOT NULL,
    id_cliente INT,
    id_endereco INT,
    total FLOAT NOT NULL,
    FOREIGN KEY(id_cliente) REFERENCES Cliente(id),
    FOREIGN KEY(id_endereco) REFERENCES Endereco(id)
);

CREATE TABLE Produto_Pedido(
	id_produto INT,
    id_pedido INT,
    qtd_produto INT NOT NULL,
    FOREIGN KEY(id_produto) REFERENCES Produto(id),
    FOREIGN KEY(id_pedido) REFERENCES Pedido(id),
    PRIMARY KEY(id_produto, id_pedido)
);

CREATE TABLE Fornecedor(
	id INT PRIMARY KEY AUTO_INCREMENT,
    cnpj VARCHAR(15) NOT NULL,
    nome_fantasia VARCHAR(30) NOT NULL,
    telefone VARCHAR(12) NOT NULL,
    id_endereco INT,
    FOREIGN KEY(id_endereco) REFERENCES Endereco(id)
);
