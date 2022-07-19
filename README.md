NAVEGAR: [Tópico 101](#101) | [Tópico 102](#102) | [Tópico 103](#103) | [Tópico 104](#104) | [Tópico 101](#105) | [Tópico 106](#106) | [Tópico 107](#107) | [Tópico 108](#108) | [Tópico 109](#109) | [Tópico 110](#110) 

# Comandos LPIC-1

![Badge em Desenvolvimento](http://img.shields.io/static/v1?label=STATUS&message=EM%20DESENVOLVIMENTO&color=ORANGE&style=for-the-badge) ![GitHub Org's stars](https://img.shields.io/github/stars/camurcadolinux?style=social)

## Objetivos do site

Meu objetivo é expor todos os comandos utilizados na Certificação LPIC-1, promovida pela **Linux Professional Institute**.

## [Ver todos os tópicos da LPIC-1](TOPICOS.md)

## TÓPICO 101: ARQUITETURA DO SISTEMA<a name="101"></a>

### 101.1: Determinar e definir as configurações de hardware

_Driver (Windows) = Módulo(Linux)_

### - Comandos de Inspeção de Hardware:

**LSPCI**
```
lspci = Todos os dispositivos conectados às portas PCI.
lspci -v = Ver os detalhes dos dispositivos
lspci -s [IDENTIFICADOR] -v = Detalhes de um dispositivo indicado
```

**LSUSB**
```
lsusb = Todos os dispositivos conectados USB
lsusb -v = Ver os detalhes dos dispositivos
lsusb -d [BUS.DEVICE] -v = Detalhes do dispositivo conectado à porta USB indicada
```

**LSMOD**
```
lsmod = Exibir todos os módulos
lsmod | grep -i [NOME] = Buscar nome de um módulo na lista
```

**MODPROBE**
```
modprobe [NOME] = Carregar um módulo
modprobe -r [NOME] = Descarregar um módulo
```

**MODINFO**
```
modinfo [NOME] = Ver todos os detalhes de um módulo específico
```
