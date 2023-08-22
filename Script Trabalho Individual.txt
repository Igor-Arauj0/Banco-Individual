create database trabalhoIndv;

--Primary key do cliente está no cartão porque o cartão precisa dos dados do cliente para ser usado.

create table clientes (
	client_cd_id serial, 
	client_tx_nome varchar(50) not null,
	client_dt_data_nasc date not null,
	client_tx_CPF varchar(11) not null,
	primary key(client_cd_id)
);

create table cartao (
    card_cd_id serial not null,
    card_tx_numero varchar(16) not null,
    fk_client_cd_id serial,
    card_tx_senha varchar(6) not null,
    card_dt_data_validade date not null,
    primary key (card_cd_id),
    foreign key (fk_client_cd_id) references clientes(client_cd_id)
);

alter table clientes rename to cliente;

INSERT INTO cliente (client_cd_id, client_tx_nome, client_dt_data_nasc, client_tx_CPF)
VALUES (1,'Igor Prata Mendes Araujo','2005-03-21','15798428796'),
 (2,'Pedro Henrique da Silva Santos','1995-06-29', '87941032568'),
 (3,'Isabela Garcia da Costa','1980-11-14', '74682015973');


insert into cartao (fk_client_cd_id, card_tx_numero,card_tx_senha, card_dt_data_validade)
values (1,'5139874602159873', '123456', '2026-12-10'), 
(2,'6281047538926107', '789098','2028-02-23'),
(3,'7392158642015378', '765432','2030-08-30');


select cliente, cartao from cliente inner join cartao 
on cliente.client_cd_id = cartao.fk_client_cd_id;

select * from cliente where client_tx_nome= 'Pedro Henrique da Silva Santos';

select cliente.client_tx_nome, cliente.client_tx_CPF, cartao.card_tx_numero, cartao.card_dt_data_validade
from cliente
join cartao on cliente.client_cd_id = cartao.fk_client_cd_id
order by cliente.client_cd_id desc;

select count(cartao.fk_client_cd_id), cartao
from cartao
group by cartao;

 
