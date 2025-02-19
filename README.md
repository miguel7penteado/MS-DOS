<img width="150" height="150" align="left" style="float: left; margin: 0 10px 0 0;" alt="MS-DOS logo" src="https://github.com/Microsoft/MS-DOS/blob/master/msdos-logo.png">   

# MS-DOS v1.25 e v2.0 - Código fonte
Este repositório contém o código-fonte original e binários compilados para MS-DOS v1.25 e MS-DOS v2.0.

Estes são os mesmos arquivos [originalmente compartilhados no Computer History Museum em 25 de março de 2014]( http://www.computerhistory.org/atchm/microsoft-ms-dos-early-source-code/) e estão sendo (re ) publicado neste repositório para torná-los mais fáceis de encontrar, referência em escritos e trabalhos externos, e para permitir a exploração e experimentação para os interessados nos primeiros sistemas operacionais de PC.

# Licença
Todos os arquivos neste repositório são lançados sob a [Licença MIT (OSI)]( https://en.wikipedia.org/wiki/MIT_License) conforme o [arquivo LICENSE](https://github.com/Microsoft/MS -DOS/blob/master/LICENSE.md) armazenado na raiz deste repositório.

# Contribua!
Os arquivos de origem neste repositório são para referência histórica e serão mantidos estáticos, portanto, **não envie** solicitações de pull sugerindo quaisquer modificações nos arquivos de origem, mas sinta-se à vontade para bifurcar este repositório e experimentar 😊.

Se, no entanto, você quiser enviar conteúdo adicional não-fonte ou modificações em arquivos não-fonte (por exemplo, este README), envie via PR e analisaremos e consideraremos.

Este projeto adotou o [Código de Conduta de Código Aberto da Microsoft](https://opensource.microsoft.com/codeofconduct/). Para obter mais informações, consulte as [Perguntas frequentes sobre o código de conduta](https://opensource.microsoft.com/codeofconduct/faq/) ou entre em contato com [opencode@microsoft.com](mailto:opencode@microsoft.com) com quaisquer perguntas adicionais ou comentários.

# DOS 1.0 e 1.1
### A Revolução do PC

## O computador pessoal IBM
Em agosto de 1981, a IBM lançou seu Personal Computer (mais conhecido como PC) e o DOS 1.0. Era amplamente esperado que a Digital Research lançasse o CP/M-86 para o novo sistema (o que acabou acontecendo), mas, enquanto isso, havia o IBM Personal Computer DOS, afinal não muito diferente do CP/M. A IBM também anunciou o suporte UCSD p-System para o PC, mas apenas o DOS estava disponível no lançamento. O anúncio foi ansiosamente esperado e amplamente coberto pela imprensa .

Deve ser lembrado que com o primeiro IBM PC, o DOS era opcional. O PC veio com BASIC, que poderia atuar como um sistema operacional muito primitivo, embutido em sua ROM. O ROM BASIC poderia usar fita cassete como meio de armazenamento, embora esse método nunca tenha se tornado popular e as revisões posteriores do PC tenham removido completamente o suporte a cassetes.

O modelo de PC básico vinha com apenas 16 KB de RAM e sem drives de disco; a memória era expansível para 256 KB (bastante em 1981). O modelo equipado com uma unidade de disco veio com 64 KB de RAM, embora o próprio DOS precisasse de menos.

Deve-se notar que o DOS teoricamente seria capaz de rodar no modelo de PC básico com 16 KB de RAM. No entanto, isso não era uma opção na prática: o BIOS do PC carregava o setor de inicialização (de um disquete) no endereço 7C00h, que é 31KB, significando que não era possível inicializar o DOS em um PC com menos de 32KB de memória. Os aplicativos DOS naturalmente precisavam de memória adicional e podem ter requisitos de RAM do sistema significativamente maiores.

## Uma nota sobre os números de versão
A IBM foi inconsistente ao se referir aos números de versão do DOS. Por exemplo, ao inicializar o DOS, o usuário pode ver uma mensagem identificando o Personal Computer DOS como “Versão 3.00”. No entanto, a carta de anúncio da IBM para o mesmo produto se referia ao “DOS 3.0”. Essa inconsistência é refletida no texto a seguir; referências a, por exemplo, DOS 2.10 e DOS 2.1 são equivalentes.

## DOS 1.0
A primeira versão do DOS era quase mais interessante pelo que não podia fazer do que pelo pouco que podia. O DOS 1.0 podia ler e gravar disquetes de 160 KB, iniciar aplicativos .COM e .EXE e processar arquivos em lote (.BAT). Ele poderia manter o controle de data e hora (de forma alguma um recurso onipresente na época), embora ambos tivessem que ser inseridos manualmente toda vez que o DOS fosse iniciado. Um arquivo de lote chamado AUTOEXEC.BAT pode ser executado automaticamente na inicialização.

![](imagem/figura1.png)

Não havia suporte para discos rígidos, sem diretórios (todos os arquivos tinham que ser armazenados no diretório raiz de um disco), sem pipes ou redirecionamento, sem drivers de dispositivo carregáveis. A interface de programação do DOS também era muito limitada.

O interpretador de comandos (COMMAND.COM) suportava apenas sete comandos internos: DIR, COPY, ERASE, PAUSE, REM, RENAME e TYPE. Além disso, DATE e TIME foram implementados como comandos externos.

![](imagem/figura2.png)

Uma ferramenta de depuração interativa básica, DEBUG.COM, foi fornecida com o DOS. Não era fácil de usar, mas era bastante poderoso nas mãos de um usuário habilidoso. Um vinculador (LINK.EXE) também foi fornecido, mas as ferramentas de desenvolvimento capazes de produzir módulos de objeto vinculáveis ​​(como MASM) tiveram que ser adquiridas separadamente.

Para editar arquivos, foi fornecido um editor orientado a linhas muito rudimentar chamado EDLIN. EDLIN era um editor muito limitado, difícil de usar e pouco capaz. No entanto, permaneceu como o único editor enviado com o DOS por uma década, provavelmente para uma grande surpresa de seu autor original.

## BASIC

O DOS 1.0 foi talvez mais útil como veículo para Disk BASIC e Advanced BASIC. O ROM BASIC embutido no PC não podia usar discos; os comandos DOS BASIC.COM e BASICA.COM “atualizaram” a ROM BASIC e adicionaram suporte a disco, entre outras coisas.

![](imagem/figura3.png)

BASIC.COM e BASICA.COM junto com a ROM BASIC forneceram um ambiente completo que foi iniciado a partir do DOS, mas foi mais ou menos totalmente separado do DOS. De certa forma, o BASIC era um ambiente de desenvolvimento integrado (IDE) primitivo. O comando SYSTEM pode ser usado para retornar ao DOS.

Vários programas de demonstração escritos em BASIC foram fornecidos no disquete do DOS. Essas demonstrações foram projetadas para mostrar alguns dos recursos do IBM PC. Todas as demos exigiam pelo menos 32 KB de memória, algumas 48 KB e algumas utilizavam o Color Graphics Adapter (CGA).

![](imagem/figura4.png)

Como o ROM BASIC era um interpretador, os programas de demonstração eram efetivamente enviados na forma de fonte; os arquivos foram tokenizados e não armazenados como arquivos de texto simples para economizar espaço, mas eles podem ser listados e editados de dentro do ambiente BASIC.

![](imagem/figura5.png)

As demonstrações mostraram como tocar “música” no IBM PC, como enviar dados para a impressora (opcional), como realizar cálculos básicos e como exibir gráficos. Nos primeiros anos do IBM PC, o BASIC provou ser popular. Era relativamente fácil de usar, razoavelmente capaz e vinha embutido no sistema. Para automação simples, era uma ferramenta adequada.

É claro que o BASIC não era muito adequado para desenvolver processadores de texto ou planilhas. Uma vez que as melhores ferramentas de desenvolvimento se tornaram disponíveis, o BASIC foi usado cada vez menos e, eventualmente, a IBM o removeu das ROMs dos sucessores do PC.

## Detalhes técnicos

O núcleo do DOS consistia em cerca de 4.000 linhas de código assembly; nenhuma linguagem de alto nível foi usada. Havia três componentes principais: IBMBIO.COM, IBMDOS.COM e COMMAND.COM.

IBMBIO.COM ou “BIOS” era um componente de driver de baixo nível. Ao adaptar o DOS a uma nova plataforma de computador, o computador BIOS normalmente precisaria da maioria das alterações (e, idealmente, as alterações necessárias nos outros componentes seriam mínimas). O IBMBIO.COM continha o disco, o console e os drivers de impressora, e foi construído sobre o ROM BIOS.

O “DOS” propriamente dito, IBMDOS.COM, era o kernel do sistema operacional. Ele implementou a API DOS (Application Programming Interface) que pode ser chamada via INT 21h e algumas outras. Ele também incluiu o código de gerenciamento de arquivos e memória.

IBMBIO.COM e IBMDOS.COM juntos formaram o núcleo do DOS, mas quando a maioria dos usuários do DOS pensa em DOS, eles pensam em COMMAND.COM, o interpretador de comandos. COMMAND.COM é opcional e pode ser substituído por um workalike (como o 4DOS da JP Software) ou um aplicativo de propósito especial pode ser iniciado diretamente (por exemplo, discos de diagnóstico da IBM).

No entanto, na maioria dos sistemas, o COMMAND.COM foi carregado e forneceu a interface do usuário. É normalmente conhecido pelo prompt C:> , exceto que no DOS 1.0 não havia tal coisa. A unidade C não existia (a menos que o usuário tivesse mais de duas unidades de disquete instaladas) e o comando PROMPT não estava disponível, então o prompt era A> na maioria dos casos.

O COMMAND.COM usou uma divisão inovadora em três partes (inicialização, residente e transitória) para economizar memória. A parte de inicialização foi usada para processar o conteúdo do AUTOEXEC.BAT e foi descartada assim que seu trabalho foi concluído. A parte transiente era a maior e continha o processador de comandos, manipulava a entrada do usuário e implementava os comandos internos. Como os comandos internos não precisavam ser carregados do disco, eles eram executados rapidamente. No entanto, eles consumiam memória preciosa e, se um aplicativo exigisse mais, o COMMAND.COM descartava a parte transitória, deixando apenas a pequena parte residente na memória. Depois que o aplicativo for concluído, a parte residente do COMMAND.COM recarregará a parte transitória do disco.

## DOS versus CP/M

O DOS foi projetado para ser amplamente compatível com o CP/M, mas não era um clone dele. A compatibilidade com o CP/M trouxe recursos como a temida limitação de nome de arquivo 8.3, mas o DOS era de várias maneiras mais capaz do que o CP/M.

A diferente (e melhor) estratégia de alocação de arquivos já foi mencionada anteriormente.

O DOS forneceu uma forma muito rudimentar de independência de dispositivos, com o console (CON), impressora (PRN) e dispositivos de comunicação serial (AUX) sendo tratados como arquivos especiais. O usuário pode, assim, por exemplo, imprimir um arquivo copiando-o para o dispositivo PRN. Esse recurso foi claramente inspirado no UNIX (ou XENIX, como provavelmente foi o caso da Microsoft).

A interface de arquivo podia lidar com E/S de registro de tamanho variável, enquanto o CP/M era limitado a registros fixos de 128 bytes.

Além dos arquivos .COM estilo CP/M, o DOS também suportava arquivos .EXE relocáveis, um formato desenvolvido por Mark Zbikowski (daí a assinatura MZ no cabeçalho do arquivo .EXE). Enquanto os arquivos .COM eram limitados a um máximo de 64 KB combinados para código, pilha e dados, os arquivos .EXE não tinham essa limitação. Em um PC, um executável no formato .EXE poderia ocupar toda a memória disponível.

## DOS 1.1

A versão 1.1 foi uma atualização relativamente menor para o DOS, lançada junto com um Computador Pessoal atualizado em maio de 1982. O PC mais novo ostentava drives de disquetes de dupla face; O DOS simplesmente dobrou a capacidade do disco utilizando ambos os lados, passando de 160 KB para 320 KB. O próprio DOS 1.1, é claro, ainda era fornecido em discos de 160 KB para que pudesse ser usado no modelo de PC anterior.

Ao contrário da versão anterior, o DOS 1.1 não exigia que o usuário digitasse uma data válida. A tecla Enter pode ser usada para aceitar a data padrão, o que resultou em muitos arquivos datados de 1º de janeiro de 1980 – antes mesmo do PC existir.

![](imagem/figura6.png)

Internamente na Microsoft, o DOS 1.1 era na verdade a versão 1.25; o último era consistente com o versionamento 86-DOS original de Tim Paterson, mas talvez não fizesse muito sentido para a IBM. O DOS 1.1 (ou 1.25) foi importante por ser a primeira versão que a Microsoft licenciou para vários OEMs, entre outros COMPAQ e Zenith.

![](imagem/figura7.jpg)

O MS-DOS 1.25 não era exatamente o mesmo que o PC DOS 1.1; A Microsoft não forneceu todo o PC DOS e vários utilitários foram escritos pela IBM. Esses incluíam DISKCOPY, DISKCOMP, COMP (todos escritos por David Litton) e o comando MODE (escrito por Mel Hallerman, Ron Heiney e, na versão 1.1, também Ed Kiser). Os três primeiros eram relativamente genéricos, mas o MODE estava um pouco ligado ao modelo de hardware específico.

## Alterações da versão anterior

Não houve grandes diferenças entre o DOS 1.1 e 1.0. DATE e TIME agora eram comandos internos embutidos no COMMAND.COM. O familiar comando DEL foi adicionado como um alias para o comando ERASE e REN para RENAME.

O sistema operacional agora registrava os horários nas entradas do diretório, não apenas as datas. O utilitário LINK foi atualizado para a versão 1.1.

![](imagem/figura8.png)

Um novo utilitário EXE2BIN.EXE foi adicionado para converter arquivos de formato EXE em arquivos de formato binário simples ou .COM. BASIC e BASICA (Disk and Advanced BASIC) também foram atualizados para a versão 1.1, com algumas pequenas diferenças.

No geral, o DOS 1.1 era tecnicamente mais ou menos o mesmo que seu antecessor. Todas as grandes mudanças tiveram que esperar pela versão 2.0, e houve algumas.

## Referências
A Enciclopédia MS-DOS , editada por Ray Duncan, Microsoft Press, 1987. ISBN 1-55615-049-0

