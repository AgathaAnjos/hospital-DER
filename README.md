# 🏥 Sistema de Controle de Consultas Hospitalares (DER Completo)

Este projeto consiste em um **Sistema de Controle de Consultas Hospitalares**, com gerenciamento completo de **médicos, pacientes, especialidades, convênios, consultas, receitas e medicamentos**. O modelo é baseado em um **DER (Diagrama Entidade-Relacionamento)** que garante integridade, organização e rastreabilidade de dados clínicos.

---

## 🔹 Modelo de Dados (DER)

<img width="1347" height="570" alt="hospital_1" src="https://github.com/user-attachments/assets/4642cb9c-413c-46a9-b6a1-de4cf90ac830" />

## 🔹 Funcionalidades

- Cadastro e gerenciamento de **médicos** com múltiplas especialidades.
- Cadastro de **pacientes** e controle de suas consultas.
- Gestão de **convênios**, incluindo tempo de carência e aceitação.
- Registro completo de **consultas**, incluindo médico, paciente, especialidade e convênio.
- Controle de **receitas médicas**, com associação a **medicamentos** e instruções de uso.
- Relacionamentos complexos com integridade referencial garantida por **chaves primárias, estrangeiras e tabelas associativas**.

---

## 🔹 Modelo de Dados (DER) atualizado

<img width="1389" height="725" alt="hospital_2" src="https://github.com/user-attachments/assets/68d67c44-c450-4b78-9075-8f790cb70ef6" />

## 🔹 Script de Criação do Banco


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

