# Construção cruzada, como fazer

Descrevendo como fazer cross build MS-DOS, sem usar máquinas virtuais ou ambiente DOS existente.

## Reconstruindo em GNU/Linux (x86 incluindo 64 bits)

Use doscomm e crossmakefile para construir em x86 GNU/Linux.
Certifique-se de que a libc de 32 bits e as ferramentas de compilação estejam instaladas antes de executar os comandos a seguir.

```
HIDOS/cross$ make
cc -no-pie -m32 -o doscomm doscomm.s
HIDOS/cross$ cd ../BUILD/
HIDOS/BUILD$ make -f ../cross/crossmakefile all
```
Use a opção -j para o comando make para fazer o make paralelo.

O arquivo NUL.MAP é criado, mas nunca usado.

## Reconstruindo em GNU/Linux (não x86)

Não testado.

Como o programa doscomm é escrito em linguagem assembly x86, use um compilador cruzado para tornar o doscomm binário.
Em seguida, use o comando qemu-i386 (emulador de usuário QEMU) para executar o binário doscomm.
A modificação do makefile pode ser necessária.

## Reconstruindo no Windows (32-bit x86)

Testado no Windows 2000 (x86).

Apenas para Windows 10.
A versão do Windows 11 de 32 bits não foi lançada.

Como o Windows de 32 bits pode executar aplicativos MS-DOS, ele pode executar o arquivo em lote de construção diretamente.
No entanto, a criação paralela provavelmente não é simples.

O programa doscomm pode funcionar em Windows de 32 bits.

## Construir no Windows (x86 de 64 bits)

Parcialmente testado.

O programa doscomm funciona em Windows de 64 bits.
No entanto, o crossmakefile precisa de um shell semelhante ao Unix e do comando make.
O Windows de 64 bits também oferece suporte ao subsistema Windows para Linux (WSL), mas o binário Linux de 32 bits parece não ser compatível com WSL1.

Usar o binário doscomm do Windows criado com MinGW do WSL GNU make parece bom.
Observe que o binário normal do Windows não pode ler links simbólicos, portanto, é necessário copiar os arquivos BUILD/ para um diretório diferente.
