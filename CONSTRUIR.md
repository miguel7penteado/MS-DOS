# Como Reconstruir ?

Ferramentas e scripts para reconstrução de MS-DOS com utilitários DEBUG, MASM, LINK e EXE2BIN.

## Estrutura dos Diretórios

- **ferramentas**/ contém ferramentas para construir MS-DOS com MASM versão 1.10 e LINK versão 2.00.
- **adições**/ contém arquivos de origem adicionais para a reconstrução do MS-DOS.
- **construir**/ contém um arquivo em lote, arquivos de entrada para EXE2BIN e links simbólicos para o código-fonte e utilitários (DEBUG, MASM, LINK e EXE2BIN).
- **maquina_virtual**/ contém uma máquina virtual simples para executar VM_IO.SYS.
- **compilação-cruzada**/ contém arquivos para construção cruzada.

## Como reconstruir

1. Prepare o ambiente DOS. (MS-DOS, FreeDOS e DOSBox são utilizáveis.)
2. Copie os arquivos do diretório BUILD/ para um sistema de arquivos acessível pelo DOS.
3. Mude o diretório de trabalho atual para o diretório BUILD/ e execute M.BAT no DOS. Os binários serão armazenados no diretório BUILD/BIN/.

See cross/HOWTO.md for cross build details.

## Reconstruído no MS-DOS 2.11

Se o MS-DOS tiver sido criado com êxito, você poderá até recriar o MS-DOS nele mesmo.
É necessário mais espaço em disco do que um disquete, mas o `PC_IO.EXE` atual não suporta discos rígidos.
Usar a máquina virtual HIDOS é fácil.
Especialmente, o hidoskvm é rápido.

## IO.SYS

O processo de construção gera os seguintes binários IO.SYS:

- `SKELIO.SYS`
- `PC_IO.EXE`
- `VM_IO.SYS`
- `DOS_IO.EXE`
- `98_IO.EXE`

`SKELIO.SYS` é o esqueleto do BIOS para o ALTOS ACS-86C.
Não testado.

`PC_IO.EXE` é compatível com BIOS para IBM PC.
Espera-se que funcione em PCjr compatível e JX também.
Ele pode ser inicializado apenas pelo código de inicialização `PC_BOOT.BIN`, pois é um binário relocável, incluindo o cabeçalho MZ.
Como o BIOS japonês JX usa algum espaço de memória adicional, o endereço dos drivers IO.SYS é corrigido durante o processo de inicialização.
A rotina de entrada do teclado converte teclas de função e teclas de seta em sequências de escape de 2 bytes manipuladas pelo DOSMES.ASM, que as diz como "equivalências VT52" por padrão.
Talvez os aplicativos esperem entrada compatível com PC DOS - o primeiro byte é NUL e o segundo byte é o código-chave do PC.
O BIOS também suporta o modo compatível com PC DOS.
Digitar ESC F10 alterna o modo.

`VM_IO.SYS` é BIOS para a máquina virtual HIDOS.
A máquina virtual carrega-o diretamente de um sistema de arquivos.
A entrada do teclado não é convertida.
Como as sequências de escape do VT100 são diferentes das "equivalências do VT52", insira a sequência de escape diretamente para edição de linha, como MU (ESC U) para copiar linha, MS (ESC S) para copiar um caractere, etc.

`DOS_IO.EXE` é BIOS para MS-DOS - DOS em DOS.
Em vez de chamar o ROM BIOS ou acessar dispositivos diretamente, ele chama o sistema host DOS.
Ele pode usar arquivos de imagem de disco para unidades.
`MSDOS.SYS` também é carregado no host.
É necessária pelo menos uma imagem ou disco do sistema de arquivos FAT12 que contenha `COMMAND.COM`.
Funciona no prompt de comando do Windows de 32 bits, MS-DOS, DOSBox e FreeDOS.

`98_IO.EXE` é BIOS para PC-98.
Ele pode ser inicializado apenas pelo código de inicialização `98_BOOT.BIN`, pois é um binário relocável, incluindo o cabeçalho MZ.
A rotina de entrada do teclado converte teclas de função como `PC_IO.EXE`, mas nenhum aplicativo usa PC DOS como entrada - o primeiro byte é NUL e o segundo byte é o código de chave PC-98.
Este BIOS não fornece o recurso KEY.TBL ou interface INT DCH.
Portanto, os aplicativos PC-98 DOS que usam a interface INT DCH ou outros serviços fornecidos pelo PC-98 MS-DOS não funcionam neste BIOS.
O suporte a disquetes de 1440KiB, 720KiB, 360KiB e 1232KiB foi implementado, mas não testado.

## Inicialize no PC

### Iniciando a partir do DOS existente (para depuração)

`PC_IO.EXE` pode ser executado em um ambiente DOS.

### Inicializando a partir do disquete

`PC_BOOT.BIN` é um arquivo binário do setor de inicialização para disquetes.
Para gravá-lo na unidade A:

```
A>DEBUG PC_BOOT.BIN
-W 100 0 0 1
-Q
A>
```

Nota: contém o bloco de parâmetros do BIOS (BPB) para o formato 720KiB.
Para usar um formato diferente de um disquete, modifique o `PC_BOOT.ASM` e construa, ou copie os primeiros 3 bytes (JMP) e do deslocamento de byte 3EH, como segue:

```
A>DEBUG PC_BOOT.BIN
-L 800 0 0 1
-M 803 83D 103
-W 100 0 0 1
-Q
```

Em seguida, renomeie `PC_IO.EXE` para `IO.SYS` e copie `IO.SYS`, `MSDOS.SYS` e `COMMAND.COM` para o disco.

O código de inicialização provavelmente não é compatível com outro DOS.
Ele carrega apenas `IO.SYS`, então `IO.SYS` carrega `MSDOS.SYS`.

## Inicialize no PC-98

Igual ao PC, exceto pelo uso de `98_IO.EXE` em vez de `PC_IO.EXE` para `IO.SYS`.

## Inicialize em uma máquina virtual HIDOS

O `VM_IO.SYS` é para a máquina virtual HIDOS.
Copie `VM_IO.SYS`, `MSDOS.SYS` e `COMMAND.COM` para uma imagem de disco.
Em seguida, inicie o comando hidosvm/hidosvm ou hidosvm/hidoskvm com o nome do arquivo de imagem de disco.

A máquina virtual HIDOS tem uma arquitetura muito simples e NÃO é compatível com PC.
Consulte hidosvm/hidosvm.txt para obter detalhes.

## Inicialize no DOS

O `DOS_IO.EXE` é IO.SYS implementado como um aplicativo DOS.
Seu parâmetro de linha de comando é o nome do arquivo MSDOS.SYS seguido pela lista de unidades que consiste no nome do arquivo de imagem FAT12 ou no nome da unidade (por exemplo, A :).
Um dispositivo de caractere `EXIT$` é instalado para sair do ambiente DOS.
Escrever um dígito (0 a 9) no dispositivo sai do DOS com o código de saída especificado pelo dígito.

Exemplos: inicie o DOS montando a imagem FDD.IMG na unidade A:

```
A>DOS_IO.EXE MSDOS.SYS FDD.IMG
```

Inicie o DOS usando as unidades A e B como estão:

```
A>DOS_IO.EXE MSDOS.SYS A: B:
```

Saia do DOS:

```
A>ECHO 0 > \DEV\EXIT$
```

## Status atual

| Nome do Arquivo   | Reconstroi ?        | Roda ?                     |
| ----------------- | ------------------- | -------------------------- |
| CHKDSK.COM        | OK                  | OK (on MS-DOS)             |
| COMMAND.COM       | OK                  | OK (on MS-DOS)             |
| DEBUG.COM         | OK                  | OK                         |
| DISKCOPY.COM      | OK                  | OK (on MS-DOS)             |
| EDLIN.COM         | OK                  | OK                         |
| EXE2BIN.EXE       | OK                  | OK                         |
| FC.EXE            | OK                  | OK                         |
| FIND.EXE          | OK                  | OK                         |
| FORMAT.COM        | OK                  | OK                         |
| HRDDRV.SYS        | OK                  | Not for PCs                |
| IO.SYS            | OK                  | OK                         |
| MORE.COM          | OK                  | OK                         |
| MSDOS.SYS         | OK                  | OK                         |
| PROFIL.COM        | OK                  |                            |
| PRINT.COM         | OK                  | OK (resident on MS-DOS)    |
| RECOVER.COM       | OK                  | OK (on MS-DOS)             |
| SORT.EXE          | OK                  | OK                         |
| SYS.COM           | OK                  | OK (on MS-DOS)             |

## Bugs

###MSDOS.SYS

A variável `CARPOS` só é atualizada em IO.ASM.
Portanto, a variável não será atualizada se os aplicativos usarem saída bruta ou INT 29H.
DEBUG.COM e COMMAND.COM parecem estar bem com esta implementação.
O comportamento é semelhante ao PC DOS, como segue:

- AH=02H or 09H (INT 21H) updates `CARPOS` and expands (horizontal) tabs.
- AH=06H does not update `CARPOS` and does not expand tabs.
- Cooked mode CON output acts like AH=02H or AH=09H.
- Raw mode CON output acts like AH=06H.

###IO.SYS

Ao contrário de outros DOS, se apenas uma unidade de disquete for encontrada, B: não existe.

###COMMAND.COM

O comando `CLS` imprime a sequência de escape ANSI (`ESC [2 J`).
A tela não é limpa porque atualmente a chave ANSI não está habilitada em IO.SYS.
A versão IBM parece chamar ROM BIOS diretamente do COMMAND.COM.

O comando `DIR /P` pausa por 23 linhas, definido como LINPERPAG em COMEQU.ASM.
Não é bom se a tela tiver menos de 24 linhas.

### CHKDSK.COM

O comando `CHKDSK` mostra a mensagem de aviso "Provável disco não-DOS." para discos de 1440 KiB.
Isso ocorre porque o comando espera FAT ID >= F8H, mas os discos de 1440 KB têm FAT ID F0H.
