# 🏥 Sistema de Controle de Consultas Hospitalares (DER Completo)

Este projeto consiste em um **Sistema de Controle de Consultas Hospitalares**, com gerenciamento completo de **médicos, pacientes, especialidades, convênios, consultas, receitas e medicamentos**. O modelo é baseado em um **DER (Diagrama Entidade-Relacionamento)** que garante integridade, organização e rastreabilidade de dados clínicos.

---

## Modelo de Dados (DER)

<img width="1347" height="570" alt="hospital_1" src="https://github.com/user-attachments/assets/4642cb9c-413c-46a9-b6a1-de4cf90ac830" />

## Funcionalidades

- Cadastro e gerenciamento de **médicos** com múltiplas especialidades.
- Cadastro de **pacientes** e controle de suas consultas.
- Gestão de **convênios**, incluindo tempo de carência e aceitação.
- Registro completo de **consultas**, incluindo médico, paciente, especialidade e convênio.
- Controle de **receitas médicas**, com associação a **medicamentos** e instruções de uso.
- Relacionamentos complexos com integridade referencial garantida por **chaves primárias, estrangeiras e tabelas associativas**.

---

## Modelo de Dados (DER) atualizado

<img width="1389" height="725" alt="hospital_2" src="https://github.com/user-attachments/assets/68d67c44-c450-4b78-9075-8f790cb70ef6" />

## Script de Criação do Banco


Médicos {
	crm integer pk increments unique
	nome varchar
	telefone integer
	aceita-whatsapp boolean
	email varchar
	id_especialidade integer unique
	enfermeiro varchar
}

Especialidade {
	id_especialidade integer pk increments unique >* Médicos.id_especialidade
	nome_especialidade varchar
	status integer
}

Consultas {
	id_consulta integer pk increments unique
	crm_médico integer > Médicos.crm
	cpf_paciente integer
	id_especialidade integer > Especialidade.id_especialidade
	id_convênio integer > Convênio.id_convênio
	data_hora datetime
	valor_consulta integer
	id_receita integer
}

Paciente {
	CPF integer pk increments unique > Consultas.cpf_paciente
	RG integer
	nome varchar
	email integer
	telefone integer
	aceita_whatsapp boolean
	id_convenio integer
	id_paciente integer > Quarto.id_paciente
}

Convênio {
	id_convênio integer pk increments unique > Paciente.id_convenio
	aceita_convênio boolean
	tempo_carência integer
}

Receita {
	id_receita integer pk increments unique > Consultas.id_receita
	data_emissão datetime
	id_consulta integer > Consultas.id_consulta
	id_medicamento integer
}

Medicaçao {
	id_medicamento integer pk increments unique > Receita.id_medicamento
	nome_medicamento varchar
}

Enfermeiro {
	id_enfermeiro integer pk increments unique > Médicos.enfermeiro
	nome varchar
	coren integer
	cpf integer
}

Quarto {
	id_quarto integer pk increments unique
	id_paciente integer > Paciente.id
	info_paciente varchar
	tipo_quarto varchar
	valor_quarto integer
	descrição_quarto varchar
}

Internação {
	id_paciente integer pk increments unique *> Paciente.id_paciente
	data_hora datetime
	data_entrada date
	previsão_alta date
	efetiva_alta integer
	descrição_procedimento integer
	id_quarto integer > Quarto.id_quarto
	tipo_quarto varchar > Quarto.tipo_quarto
	crm_médico integer > Médicos.crm
	coren_enfermeiro integer > Enfermeiro.coren
}


## Modelo de Dados (DER) - Pt. 4

<img width="1389" height="725" alt="hospital_1" src="https://github.com/user-attachments/assets/45612a6d-d6ea-43ee-a8a1-e858f05f91e5" />

## Script de Criação do Banco


Médicos {
	crm integer pk increments unique
	nome varchar
	telefone integer
	aceita-whatsapp boolean
	email varchar
	id_especialidade integer
	enfermeiro varchar
	em_atividade boolean
}

Especialidade {
	id_especialidade integer pk increments unique >* Médicos.id_especialidade
	nome_especialidade varchar
	status integer
}

Consultas {
	id_consulta integer pk increments unique
	crm_médico integer > Médicos.crm
	cpf_paciente integer
	id_especialidade integer > Especialidade.id_especialidade
	id_convênio integer > Convênio.id_convênio
	data_hora datetime
	valor_consulta integer
	id_receita integer
}

Paciente {
	CPF integer pk increments unique > Consultas.cpf_paciente
	RG integer
	nome varchar
	email integer
	telefone integer
	aceita_whatsapp boolean
	id_convenio integer
	id_paciente integer > Quarto.id_paciente
}

Convênio {
	id_convênio integer pk increments unique > Paciente.id_convenio
	aceita_convênio boolean
	tempo_carência integer
}

Receita {
	id_receita integer pk increments unique > Consultas.id_receita
	data_emissão datetime
	id_consulta integer > Consultas.id_consulta
	id_medicamento integer
}

Medicaçao {
	id_medicamento integer pk increments unique > Receita.id_medicamento
	nome_medicamento varchar
}

Enfermeiro {
	id_enfermeiro integer pk increments unique > Médicos.enfermeiro
	nome varchar
	coren integer
	cpf integer
}

Quarto {
	id_quarto integer pk increments unique
	id_paciente integer > Paciente.id
	info_paciente varchar
	tipo_quarto varchar
	valor_quarto integer
	descrição_quarto varchar
}

Internação {
	id_paciente integer pk increments unique *> Paciente.id_paciente
	data_hora datetime
	data_entrada date
	previsão_alta date
	efetiva_alta integer
	descrição_procedimento integer
	id_quarto integer > Quarto.id_quarto
	tipo_quarto varchar > Quarto.tipo_quarto
	crm_médico integer > Médicos.crm
	coren_enfermeiro integer > Enfermeiro.coren
}


## Script de Criação do Banco - Pt. 5


Médicos {
	crm integer pk increments unique
	nome varchar
	telefone integer
	aceita-whatsapp boolean
	email varchar
	id_especialidade integer
	enfermeiro varchar
	em_atividade boolean
}

Especialidade {
	id_especialidade integer pk increments unique >* Médicos.id_especialidade
	nome_especialidade varchar
	status integer
}

Consultas {
	id_consulta integer pk increments unique
	crm_médico integer > Médicos.crm
	cpf_paciente integer
	id_especialidade integer > Especialidade.id_especialidade
	id_convênio integer > Convênio.id_convênio
	data_hora datetime
	valor_consulta integer
	id_receita integer
}

Paciente {
	CPF integer pk increments unique > Consultas.cpf_paciente
	RG integer
	nome varchar
	email integer
	telefone integer
	aceita_whatsapp boolean
	id_convenio integer
	id_paciente integer > Quarto.id_paciente
}

Convênio {
	id_convênio integer pk increments unique > Paciente.id_convenio
	aceita_convênio boolean
	tempo_carência integer
}

Receita {
	id_receita integer pk increments unique > Consultas.id_receita
	data_emissão datetime
	id_consulta integer > Consultas.id_consulta
	id_medicamento integer
}

Medicaçao {
	id_medicamento integer pk increments unique > Receita.id_medicamento
	nome_medicamento varchar
}

Enfermeiro {
	id_enfermeiro integer pk increments unique > Médicos.enfermeiro
	nome varchar
	coren integer
	cpf integer
}

Quarto {
	id_quarto integer pk increments unique
	id_paciente integer > Paciente.id
	info_paciente varchar
	tipo_quarto varchar
	valor_quarto integer
	descrição_quarto varchar
}

Internação {
	id_paciente integer pk increments unique *> Paciente.id_paciente
	data_hora datetime
	data_entrada date
	previsão_alta date
	efetiva_alta integer
	descrição_procedimento integer
	id_quarto integer > Quarto.id_quarto
	tipo_quarto varchar > Quarto.tipo_quarto
	crm_médico integer > Médicos.crm
	coren_enfermeiro integer > Enfermeiro.coren
}

INSERT INTO Especialidade (nome_especialidade, status)
VALUES 
('Pediatria', 1),

('Clínica Geral', 1),

('Gastrenterologia', 1),

('Dermatologia', 1),

('Cardiologia', 1),

('Ortopedia', 1),

('Neurologia', 1);

INSERT INTO Medicos (nome, telefone, aceita_whatsapp, email, id_especialidade, enfermeiro, em_atividade)
VALUES
('Dr. João Silva', 11987654321, TRUE, 'joao.silva@hospital.com', 1, 'Enf. Carla', TRUE),

('Dra. Mariana Souza', 11976543210, TRUE, 'mariana.souza@hospital.com', 2, 'Enf. Pedro', TRUE),

('Dr. Carlos Lima', 11965432109, FALSE, 'carlos.lima@hospital.com', 3, 'Enf. Ana', TRUE),

('Dra. Fernanda Costa', 11954321098, TRUE, 'fernanda.costa@hospital.com', 4, 'Enf. Lucas', TRUE),

('Dr. Roberto Almeida', 11943210987, FALSE, 'roberto.almeida@hospital.com', 5, 'Enf. Julia', TRUE),

('Dra. Paula Mendes', 11932109876, TRUE, 'paula.mendes@hospital.com', 6, 'Enf. Rafael', TRUE),

('Dr. Eduardo Rocha', 11921098765, TRUE, 'eduardo.rocha@hospital.com', 7, 'Enf. Camila', TRUE),

('Dra. Laura Fernandes', 11910987654, TRUE, 'laura.fernandes@hospital.com', 1, 'Enf. Bruno', TRUE),

('Dr. Henrique Martins', 11909876543, FALSE, 'henrique.martins@hospital.com', 2, 'Enf. Sofia', TRUE),

('Dra. Renata Ribeiro', 11998765432, TRUE, 'renata.ribeiro@hospital.com', 3, 'Enf. Thiago', TRUE);

INSERT INTO Paciente (CPF, RG, nome, email, telefone, aceita_whatsapp, id_convenio)
VALUES
(11111111111, 12345678, 'Ana Paula', 'ana.paula@email.com', 11987654321, TRUE, 1),

(22222222222, 23456789, 'Carlos Eduardo', 'carlos.edu@email.com', 11976543210, FALSE, 2),

(33333333333, 34567890, 'Mariana Lima', 'mariana.lima@email.com', 11965432109, TRUE, 3),

(44444444444, 45678901, 'João Pedro', 'joao.pedro@email.com', 11954321098, TRUE, 1),

(55555555555, 56789012, 'Fernanda Rocha', 'fernanda.rocha@email.com', 11943210987, FALSE, 2),

(66666666666, 67890123, 'Lucas Martins', 'lucas.martins@email.com', 11932109876, TRUE, 3),

(77777777777, 78901234, 'Paula Fernandes', 'paula.fernandes@email.com', 11921098765, TRUE, 4),

(88888888888, 89012345, 'Eduardo Ribeiro', 'eduardo.ribeiro@email.com', 11910987654, FALSE, 4),

(99999999999, 90123456, 'Renata Costa', 'renata.costa@email.com', 11909876543, TRUE, 1),

(10101010101, 12345670, 'Thiago Souza', 'thiago.souza@email.com', 11998765432, TRUE, 2),

(12121212121, 23456701, 'Sofia Almeida', 'sofia.almeida@email.com', 11987654320, TRUE, 3),

(13131313131, 34567012, 'Bruno Lima', 'bruno.lima@email.com', 11976543211, FALSE, 4),

(14141414141, 45670123, 'Camila Rocha', 'camila.rocha@email.com', 11965432100, TRUE, 1),

(15151515151, 56701234, 'Rafael Martins', 'rafael.martins@email.com', 11954321090, TRUE, 2),

(16161616161, 67812345, 'Julia Fernandes', 'julia.fernandes@email.com', 11943210980, TRUE, 3);


INSERT INTO Convenio (aceita_convênio, tempo_carência)
VALUES
(TRUE, 30),

(TRUE, 60),

(FALSE, 0),

(TRUE, 90);


INSERT INTO Medicaçao (nome_medicamento)
VALUES
('Dipirona'),

('Paracetamol'),

('Ibuprofeno'),

('Amoxicilina'),

('Omeprazol'),

('Ranitidina'),

('Loratadina'),

('Metformina'),

('Losartana'),

('Cloridrato de Sertralina');


INSERT INTO Receita (data_emissão, id_medicamento)
VALUES
('2019-01-10', 1),

('2019-01-10', 2),

('2020-05-20', 3),

('2020-05-20', 4),

('2018-08-15', 5),

('2018-08-15', 6),

('2021-02-11', 7),

('2021-02-11', 8),

('2016-07-19', 9),

('2016-07-19', 10);



INSERT INTO Consultas (crm_médico, cpf_paciente, id_especialidade, id_convênio, data_hora, valor_consulta, id_receita)
VALUES
(101, 11111111111, 1, 1, '2015-02-10 09:00', 200, 1),

(102, 22222222222, 2, 2, '2016-03-15 10:30', 250, 2),

(103, 33333333333, 3, 3, '2017-06-20 14:00', 300, 3),

(104, 44444444444, 4, 1, '2018-07-22 08:30', 220, 4),

(105, 55555555555, 5, 2, '2019-09-10 11:00', 280, 5),

(106, 66666666666, 6, 3, '2020-01-15 15:00', 260, 6),

(107, 77777777777, 7, 4, '2021-03-18 09:45', 240, 7),

(108, 88888888888, 1, 4, '2015-04-10 10:15', 210, 8),

(109, 99999999999, 2, 1, '2016-05-12 13:30', 230, 9),

(110, 10101010101, 3, 2, '2017-06-14 16:00', 270, 10),

-- repetir para completar 20 consultas, garantindo que alguns pacientes tenham mais de uma consulta
(101, 11111111111, 1, 1, '2018-02-10 09:00', 200, 1),

(102, 22222222222, 2, 2, '2019-03-15 10:30', 250, 2),

(103, 33333333333, 3, 3, '2020-06-20 14:00', 300, 3),

(104, 44444444444, 4, 1, '2021-07-22 08:30', 220, 4),

(105, 55555555555, 5, 2, '2016-09-10 11:00', 280, 5),

(106, 66666666666, 6, 3, '2017-01-15 15:00', 260, 6),

(107, 77777777777, 7, 4, '2018-03-18 09:45', 240, 7),

(108, 88888888888, 1, 4, '2019-04-10 10:15', 210, 8),

(109, 99999999999, 2, 1, '2020-05-12 13:30', 230, 9),

(110, 10101010101, 3, 2, '2021-06-14 16:00', 270, 10);


INSERT INTO Quarto (id_paciente, info_paciente, tipo_quarto, valor_quarto, descrição_quarto)
VALUES
(11111111111, 'Paciente Ana Paula', 'Apartamento', 500, 'Quarto individual com banheiro privativo'),

(22222222222, 'Paciente Carlos Eduardo', 'Quarto Duplo', 300, 'Quarto compartilhado com 2 camas'),

(33333333333, 'Paciente Mariana Lima', 'Enfermaria', 150, 'Quarto coletivo com 4 camas'),

(44444444444, 'Paciente João Pedro', 'Apartamento', 500, 'Quarto individual com banheiro privativo'),

(55555555555, 'Paciente Fernanda Rocha', 'Quarto Duplo', 300, 'Quarto compartilhado com 2 camas'),

(66666666666, 'Paciente Lucas Martins', 'Enfermaria', 150, 'Quarto coletivo com 4 camas'),

(77777777777, 'Paciente Paula Fernandes', 'Apartamento', 500, 'Quarto individual com banheiro privativo');


INSERT INTO Enfermeiro (nome, coren, cpf)
VALUES
('Carla Souza', 12345, 11111111111),

('Pedro Lima', 23456, 22222222222),

('Ana Rocha', 34567, 33333333333),

('Lucas Fernandes', 45678, 44444444444),

('Julia Martins', 56789, 55555555555),

('Rafael Almeida', 67890, 66666666666),

('Camila Costa', 78901, 77777777777),

('Bruno Ribeiro', 89012, 88888888888),

('Sofia Oliveira', 90123, 99999999999),

('Thiago Santos', 11223, 10101010101);


INSERT INTO Internação (id_paciente, data_hora, data_entrada, previsão_alta, efetiva_alta, descrição_procedimento, id_quarto, tipo_quarto, crm_médico, coren_enfermeiro)
VALUES
(11111111111, '2015-02-10 09:00', '2015-02-10', '2015-02-15', 1, 'Cirurgia', 1, 'Apartamento', 101, 12345),

(22222222222, '2016-03-15 10:00', '2016-03-15', '2016-03-20', 1, 'Observação', 2, 'Quarto Duplo', 102, 23456),

(11111111111, '2017-04-20 08:00', '2017-04-20', '2017-04-25', 1, 'Exame', 1, 'Apartamento', 101, 34567),

(33333333333, '2018-05-12 11:00', '2018-05-12', '2018-05-18', 1, 'Cirurgia', 3, 'Enfermaria', 103, 45678),

(44444444444, '2019-06-18 14:00', '2019-06-18', '2019-06-25', 1, 'Observação', 1, 'Apartamento', 104, 56789),

(55555555555, '2020-07-22 09:00', '2020-07-22', '2020-07-30', 1, 'Exame', 2, 'Quarto Duplo', 105, 67890),

(66666666666, '2021-08-15 10:30', '2021-08-15', '2021-08-22', 1, 'Cirurgia', 3, 'Enfermaria', 106, 78901);



