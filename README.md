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

### - Diretórios com Informações de Hardware:

- Diretórios Raiz:

```
/sys
/proc
```

- Arquivos Principais:

```
/proc/cpuinfo - Informações do Processador
/proc/meminfo - Informações da Memória RAM
/proc/ioports - Portas I/O em uso
/proc/partitions - Lista de partições
/proc/uptime - Tempo que o computador está ligado
/proc/version - Versão do Linux utilizado
```

- Comandos para filtar informações:

```
cat - Exibe todo o arquivo
cat | grep [termo buscado ente aspas simples] - Buscar um termo (ex:  modelname)
```
### 101.2: Entender o processo de boot do GNU/Linux

### **BIOS x UEFI**

- BIOS | Basic Input Output System

```
- Mais antigo
- Primeiros 440 bytes do primeiro dispositivo de armazenamento contenham o estágio inicial do carregador de boot, chamado MBR (Master Boot Record)

PASSO-A-PASSO

1. POST: Identifica erros básicos de hardware
2. BIOS ativa monitor, teclado e dispositivos de armazenamento
3. BIOS carrega o primeiro estágio do bootloader a partir do MBR
4. O primeiro estágio chama o segundo estágio, que apresenta as opções de boot(GRUB) e carrega o Kernel
```
- UEFI | Unified Extensible Firmware Interface

```
- Mais moderno que a BIOS
- Lê tabela de partições
- Ignora o MBR e leva em consideração as definições armazenadas na NVRAM
  - Indicam a localização dos aplicativos EFI, que são os carregadores de boot ou ferramentas de diagnóstico.
- Sistemas de arquivos compatíveis:
  - FAT12
  - FAT16
  - FAT32
  - ISO-9660 (Mídias Ópticas)
  
  PASSO-A-PASSO
  
  1. POST: Identifica erros básicos de hardware
  2. BIOS ativa monitor, teclado e dispositivos de armazenamento
  3. BIOS lê o que está na NVRAM, localiza arquivos de partição ESP e executa o aplicativo EFI
  4. O primeiro estágio chama o segundo estágio, que apresenta as opções de boot(GRUB) e carrega o Kernel
  ```
- Comandos e arquivos de Informações:

```
dmesg - Lê os logs de inicialização
journalctl - Lê os logs de inicalização, mas aceita parâmetros
  --boot / --dmesg - Mesmo resultado do dmesg
  --user - Logs do usuário atual
  -b [numero] - Busca os logs do boot, sendo 0 o boot atual, e números negativos os boots anteriores
```
### 101.3: Alterar níveis de execução, desligar e reiniciar

- *SystemVinit ou SystemV - Mais antigo, mas ainda utilizado na inicialização*
    Baseado em RunLevels
    - 0 = Desligamento | /etc/rc0.d
    - 1, s, S, single = Modo de segurança | /etc/rc1.d
    - 2 = Multiusuário sem interface | /etc/rc2.d
    - 3 = Multiusuário sem interface | /etc/rc3.d
    - 4 = Personalização | /etc/rc4.d
    - 5 = Multiusuário com interface (padrão) | /etc/rc5.d
    - 6 = Reinicialização | /etc/rc6.d

    O arquivo */etc/inittab* define qual runlevel será inicializado no boot
    Sintaxe = id:N:initdefault:
    
- *SystemD*
  - Cada unidade é chamadas "unit" = Nome, tipo e arquivo de configuração
  - Cada "unidade" tem um sufixo. Os principais:
    - service = Recursos ativos do sistema, que podem ser inicializados e interrompindos
      - COMANDOS POSSÍVEIS:
        ```
        start
        stop
        status
        is-active (está ativo?)
        enable
        disable
        is-enable
        ```
    - socket = Recebe a solicitação
    - device = Associado ao hardware
    - mount = Unidade de montagem (etc/fstab)
    - automount = Unidade de montagem automática
    - snapshot = Estado salvo do gerenciador do SystemD
    - target = Unidade de agrupamento de unidades

  Para definir o runlevel padrão:
  ```
  systemctl set-default [runlevel]
  ```
  Os arquivos de configuração das unidades ficam em:
  ```
  /lib/systemctl/system
  ```
  Você também pode usar:
  ```
  systemctl list-unit-files --type=[tipo]
  ```
  PARA GERENCIAR ENERGIA VOCÊ PODE USAR:
  ```
  systemctl suspend
  systemctl hibernate
  ```
  PARA AJUSTES FINOS: ACPI (RECOMENDADO)

- *Upstart*
