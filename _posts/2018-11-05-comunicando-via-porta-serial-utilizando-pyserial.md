---
layout: post
published: true
show-avatar: true
comments: true
title: Comunicando via porta serial utilizando pySerial
tags:
  - python
  - serial
  - pyserial
---
Muitas vezes precisamos comunicar com outros dispositivos e periféricos. Pra quem já tem alguma intimidade com o Arduino ou outra plataforma embarcada sabe que é uma necessidade, que as vezes apenas um monitor serial não pode solucionar.

Desenvolver a comunicação traz muita flexibilidade para o programador, como a vantagem de poder desenvolver o próprio sistema de supervisão ou dar um tratamento mais sofisticado para os dados adquiridos.
Por **Python** nos trazer uma linguagem de fácil prototipação, tenho usado cada vez nos projetos e hoje vou falar um pouco sobre a popular biblioteca multiplataforma de comunicação serial, a [pySerial](https://pythonhosted.org/pyserial).

Eu tive muito sucesso com ela em sistemas operacionais Linux, já em Windows a performance dela ficou bem precária para comunicação em alta velocidade.

## Overview

a pySerial fornece um módulo chamado `serial`, que encapsula o acesso à porta serial. O módulo automaticamente seleciona a implementação nativa de acordo com o ambiente à ser utilizado.

## Instalação

A instalação do módulo pode ser feita através do `pip`, de maneira muito fácil:
```shell
pip install pyserial
```

## Primeiros passos

A utilização da porta serial consiste em algus passos simples:
1. _Configurar_ a porta;
2. _Abrir_ a porta;
3. E está pronta para usar.

> Não esquecendo de fechar a porta após o uso.

### Abrindo a porta

Há várias maneiras de fazer os primeiros passos, e deixarei o detalhamento para a [documentação oficial](https://pythonhosted.org/pyserial/shortintro.html).

Minha preferencia é sempre por configurar e abrir diretamente no construtor, assim:

```python
import serial
ser = serial.Serial('COM3', 9600)	#Configurando e abrindo a porta
ser.write(b'hello')
s = ser.read()
ser.close()
```

utilizando o laço `with`, não precisamos nos preocupar com o fechamento da porta (_Python 3_):

```python
import serial
with serial.Serial('COM3', 9600) as porta: 	
	porta.write(b'hello')
    linha = porta.readline()
```

### Utilizando a porta:

Uma das funções que eu considero mais bacanas, principalmente na leitura é a função `readline` da classe `Serial`. Ela permite bloquear (ou não) a tarefa que esta realizando a leitura até receber o caracter de quebra de linha.

```python
linha = ser.readline()
linha_str = linha.decode('utf-8') 	# Converte o array de bytes recebido para String
```

É possível ler byte a byte com a função `read`, retornando um objeto do tipo _bytes_.

Podemos checar se tem algo no buffer de entrada ou saída com a propriedade `in_waiting` ou `out_waiting`.
```python
	if ser.in_waiting > 0:
    	c = ser.read()
```

Para enviar algo, podemos usar a função `write`, passando como parâmetro uma instância de _bytes_ ou _bytearray_. Para converter um String para bytes, podemos usar a função `encode`, algo como:
```python
ser.write("Ola mundo".encode('utf-8'))
```

## Have fun!

### Anexo: Comandos úteis:

Mini terminal pySerial:
`python -m serial.tools.miniterm <port_name>`

Lista de portas seriais disponíveis:
`python -m serial.tools.list_ports`

