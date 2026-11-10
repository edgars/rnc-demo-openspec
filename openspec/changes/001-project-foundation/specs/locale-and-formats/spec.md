# Spec Delta

## Purpose

Locale, formatos de data e moeda, máscaras de entrada e os serviços de endereço que todo formulário de Mundial compartilha.

## ADDED Requirements

### Requirement: Locale e formatos
A aplicação SHALL usar o locale pt-BR: datas exibidas e digitadas como `DD/MM/YYYY`, valores exibidos com o símbolo `R$` e os separadores numéricos do locale.

#### Scenario: Uma data e um valor são exibidos
- **WHEN** uma lista ou formulário exibe uma data e um valor
- **THEN** a data segue `DD/MM/YYYY` e o valor vem prefixado com `R$` usando os separadores do locale pt-BR

### Requirement: Máscaras de entrada
Campos reconhecidos como CPF, telefone SHALL ser digitados através da sua máscara de entrada; um valor que não completa a máscara SHALL ser rejeitado ao salvar com mensagem inline.

#### Scenario: Um CPF é digitado
- **WHEN** o usuário digita dígitos em um campo CPF com máscara `###.###.###-##`
- **THEN** o campo exibe o valor formatado como `###.###.###-##` enquanto digita
- **AND** um valor incompleto é rejeitado ao salvar com mensagem inline

#### Scenario: Um telefone é digitado
- **WHEN** o usuário digita dígitos em um campo telefone com máscara `(##) ####-####`
- **THEN** o campo exibe o valor formatado como `(##) ####-####` enquanto digita
- **AND** um valor incompleto é rejeitado ao salvar com mensagem inline

