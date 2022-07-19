# Comandos LPIC-1

![Badge em Desenvolvimento](http://img.shields.io/static/v1?label=STATUS&message=EM%20DESENVOLVIMENTO&color=GREEN&style=for-the-badge)

## Objetivos do site

Meu objetivo é expor todos os comandos utilizados na Certificação LPIC-1, promovida pela **Linux Professional Institute**.

## [Ver todos os tópicos da LPIC-1](TOPICOS.md)

## TÓPICO 101: ARQUITETURA DO SISTEMA

### 101.1: Determinar e definir as configurações de hardware

Driver     =  Módulo
(Windows)  =  (Linux)

Comandos de Inspeção de Hardware:

```
LSPCI
lspci = Todos os dispositivos conectados às portas PCI.
lspci -v = Ver os detalhes dos dispositivos
lspci -s [IDENTIFICADOR] -v = Detalhes de um dispositivo indicado

LSUSB
lsusb = Todos os dispositivos conectados USB
lsusb -v = Ver os detalhes dos dispositivos
lsusb -d [BUS.DEVICE] -v = Detalhes do dispositivo conectado à porta USB indicada
```
