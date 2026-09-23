-- Database: Aula05DB_livraria



-- DROP DATABASE IF EXISTS "Aula05DB_livraria";

/*

CREATE DATABASE "Aula05DB_livraria"
  WITH
  OWNER = postgres
  ENCODING = 'UTF8'
  LC_COLLATE = 'Portuguese_Brazil.1252'
  LC_CTYPE = 'Portuguese_Brazil.1252'
  LOCALE_PROVIDER = 'libc'
  TABLESPACE = pg_default
  CONNECTION LIMIT = -1
  IS_TEMPLATE = False; */ 


--criacao de tabelas
CREATE TABLE Clientes 
(
id_cli int,
nome_cli varchar(100),
tel numeric(11),
email_cli varchar(100),
constraint pk_Id_cli primary key (id_cli)
);


CREATE TABLE pedidos 
(
id_ped int,
data_ped date,
valor_ped numeric(7,2),
id_cli int,
constraint pk_Id_ped primary key (id_ped),
constraint fk_Id_cli foreign key (id_cli) references clientes (id_cli)
);


CREATE TABLE livros 
(
id_liv int,
nome_liv varchar(100),
editora_liv varchar(100),
autor_liv varchar(100),
constraint pk_Id_liv primary key (id_liv)
);


ALTER TABLE livros add column qtde_liv int; 


CREATE TABLE item_pedidos 
(
id_ite int,
id_ped int,
id_liv int,
qtde_liv int,
constraint pk_Id_ite primary key(id_ite),
constraint fk_Id_ped foreign key (id_ped) references pedidos (id_ped),
constraint fk_Id_liv foreign key (id_liv) references livros (id_liv)
);

CREATE TABLE pagamento 
(
id_pag int, 
id_ite int, 
tipo_pag varchar(100),
valor_pag numeric(7,2),
constraint pk_id_pag primary key (id_pag),
constraint fk_id_ite foreign key (id_ite) references item_pedidos (id_ite)
);


CREATE TABLE livros_falta
(
id_livf int,
qtde_livf numeric, 
valor_livf numeric(7,2),
id_liv int,
constraint pk_id_livf primary key (id_livf),
constraint fk_id_liv foreign key (id_liv) references livros (id_liv)
);


CREATE TABLE editoras 
(
id_edi int, 
nome_edi varchar(100),
email_edi varchar(100),
constraint pk_id_edi primary key (id_edi)
);


CREATE TABLE pedido_aquisicao
(
id_ped_aq int, 
id_livf int,
id_edi int,
qtde_ped_aq numeric,
valor_ped_aq numeric(7,2),
constraint pk_id_ped_aq primary key (id_ped_aq),
constraint fk_id_livf foreign key (id_livf) references livros_falta (id_livf),
constraint fk_id_edi foreign key (id_edi) references editoras (id_edi)
);