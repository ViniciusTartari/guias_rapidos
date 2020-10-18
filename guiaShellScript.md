# Guia shell script

Referência rápida do shell do Unix/Linux/Mac, com várias tabelas que resumem comandos, operadores, opções, conceitos, exemplos, dicas e listagens. Nada de texto, só tabelas. Bom para guardar, imprimir, ter sempre à mão para tirar dúvidas.

_Guia baseado no material de [Aurelio Marinho Jargas](https://aurelio.net/shell/), com algumas alterações._

## O que é shell

Shell é a linha de comando do Linux (e UNIX). É o shell quem interpreta a linha de comandos digitada pelo usuário no terminal e chama os programas desejados.

Além de executar comandos do sistema, o shell também tem seus próprios comandos, como IF, FOR e WHILE, e também possui variáveis e funções. Tudo isso para tornar um pouco mais "esperta" e flexível essas chamadas de comandos feitas pelo usuário.

Como estas são as características de uma linguagem de programação, o shell é uma ferramenta muito poderosa para desenvolver scripts e códigos rápidos para automatizar tarefas do dia-a-dia.

Para os que vêm do mundo MSDOS, pense no shell como um Batch (dos arquivos .BAT). O shell é como um Batch (muito) melhorado.

Mas não se engane, o shell não é um brinquedo.

Assim como serve para fazer scripts de 5 ou 10 linhas, ele é versátil e completo o suficiente para que GRANDES programas sejam feitos nele. A interação natural com o sistema operacional e seus programas multiplica os poderes do shell.

Interfaces interativas com o usuário, programas de cálculos, CGI, instaladores de software, manipulação de banco de dados, rotinas de backup, tudo isso pode ser feito em shell!

Here we go!

## Operadores

| Operadores Aritméticos             |                                         |
| ---------------------------------- | --------------------------------------- |
| `+`                                | Adição                                  |
| `-`                                | Subtração                               |
| `*`                                | Multiplicação                           |
| `/`                                | Divisão                                 |
| `%`                                | Módulo                                  |
| `**`                               | Exponenciação                           |
| **Operadores de Atribuição**       |                                         |
| `=`                                | Atribui valor a uma variável            |
| `+=`                               | Incrementa a variável por uma constante |
| `-=`                               | Decrementa a variável por uma constante |
| `*=`                               | Multiplica a variável por uma constante |
| `/=`                               | Divide a variável por uma constante     |
| `%=`                               | Resto da divisão por uma constante      |
| `++`                               | Incrementa em 1 o valor da variável     |
| `--`                               | Decrementa em 1 o valor da variável     |
| **Operadores Relacionais**         |                                         |
| `==`                               | Igual                                   |
| `!=`                               | Diferente                               |
| `>`                                | Maior                                   |
| `>=`                               | Maior ou Igual                          |
| `<`                                | Menor                                   |
| `<=`                               | Menor ou Igual                          |
| **Operadores Lógicos**             |                                         |
| `&&`                               | E lógico (AND)                          |
| `                                  |                                         | ` | OU lógico (OR) |
| **Operadores de BIT**              |                                         |
| `<<`                               | Deslocamento à esquerda                 |
| `>>`                               | Deslocamento à direita                  |
| `&`                                | E de bit (AND)                          |
| `                                  | `                                       | OU de bit (OR) |
| `^`                                | OU exclusivo de bit (XOR)               |
| `~`                                | Negação de bit                          |
| `!`                                | NÃO de bit (NOT)                        |
| **Operadores de BIT (atribuição)** |                                         |
| `<<=`                              | Deslocamento à esquerda                 |
| `>>=`                              | Deslocamento à direita                  |
| `&=`                               | E de bit                                |
| `                                  | =`                                      | OU de bit |
| `^=`                               | OU exclusivo de bit                     |

## Redirecionamento

| Operador | Ação                                                                        |
| -------- | --------------------------------------------------------------------------- |
| `<`      | Redireciona a entrada padrão (STDIN)                                        |
| `>`      | Redireciona a saída padrão (STDOUT)                                         |
| `2>`     | Redireciona a saída de erro (STDERR)                                        |
| `>>`     | Redireciona a saída padrão, anexando                                        |
| `2>>`    | Redireciona a saída de erro, anexando                                       |
| `        | `                                                                           | Conecta a saída padrão com a entrada padrão de outro comando |
| `2>&1`   | Conecta a saída de erro na saída padrão                                     |
| `>&2`    | Conecta a saída padrão na saída de erro                                     |
| `>&-`    | Fecha a saída padrão                                                        |
| `2>&-`   | Fecha a saída de erro                                                       |
| `3<>arq` | Conecta o descritor de arquivos 3 ao arquivo 'arq'                          |
| `<`      | Alimenta a entrada padrão (Here Document)                                   |
| `<<-FIM` | Alimenta a entrada padrão, cortando TABs                                    |
| `<(cmd)` | A saída do comando 'cmd' é um arquivo: diff <(cmd1) <(cmd2)                 |
| `>(cmd)` | A entrada do comando 'cmd' é um arquivo: tar cf >(bzip2 -c >file.tbz) \$dir |

## Variáveis especiais

| Variável | Parâmetros Posicionais                                   |
| -------- | -------------------------------------------------------- |
| `$0`     | Parâmetro número 0 (nome do comando ou função)           |
| `$1`     | Parâmetro número 1 (da linha de comando ou função)       |
| `...`    | Parâmetro número N ...                                   |
| `$9`     | Parâmetro número 9 (da linha de comando ou função)       |
| `${10}`  | Parâmetro número 10 (da linha de comando ou função)      |
| `...`    | Parâmetro número NN ...                                  |
| `$#`     | Número total de parâmetros da linha de comando ou função |
| `$*`     | Todos os parâmetros, como uma string única               |
| `$@`     | Todos os parâmetros, como várias strings protegidas      |
| Variável | Miscelânia                                               |
| `$$`     | Número PID do processo atual (do próprio script)         |
| `$!`     | Número PID do último job em segundo plano                |
| `$_`     | Último argumento do último comando executado             |
| `$?`     | Código de retorno do último comando executado            |

## Expansão de variáveis

| Sintaxe              | Expansão Condicional                                           |
| -------------------- | -------------------------------------------------------------- |
| `${var:-texto}`      | Se var não está definida, retorna 'texto'                      |
| `${var:=texto}`      | Se var não está definida, defina-a com 'texto'                 |
| `${var:?texto}`      | Se var não está definida, retorna o erro 'texto'               |
| `${var:+texto}`      | Se var está definida, retorna 'texto', senão retorna o vazio   |
| Sintaxe              | Expansão de Strings                                            |
| `${var}`             | É o mesmo que \$var, porém não ambíguo                         |
| `${#var}`            | Retorna o tamanho da string                                    |
| `${!var}`            | Executa o conteúdo de $var (igual 'eval \$$var')               |
| `${!texto*}`         | Retorna os nomes de variáveis começadas por 'texto'            |
| `${var:N}`           | Retorna o texto a partir da posição 'N'                        |
| `${var:N:tam}`       | Retorna 'tam' caracteres a partir da posição 'N'               |
| `${var#texto}`       | Corta 'texto' do início da string                              |
| `${var##texto}`      | Corta 'texto' do início da string (\* guloso)                  |
| `${var%texto}`       | Corta 'texto' do final da string                               |
| `${var%%texto}`      | Corta 'texto' do final da string (\* guloso)                   |
| `${var/texto/novo}`  | Substitui 'texto' por 'novo', uma vez                          |
| `${var//texto/novo}` | Substitui 'texto' por 'novo', sempre                           |
| `${var/#texto/novo}` | Se a string começar com 'texto', substitui 'texto' por 'novo'  |
| `${var/%texto/novo}` | Se a string terminar com 'texto', substitui 'texto' por 'novo' |
| `${var^}`            | Converte para maiúscula o primeiro caractere                   |
| `${var^^}`           | Converte para maiúscula todos os caracteres                    |
| `${var,}`            | Converte para minúscula o primeiro caractere                   |
| `${var,,}`           | Converte para minúscula todos os caracteres                    |
| `${var~}`            | Inverte maiúscula/minúscula do primeiro caractere              |
| `${var~~}`           | Inverte maiúscula/minúscula de todos os caracteres             |

## Blocos e agrupamentos

| Sintaxe    | Descrição                                                        | Exemplo     |
| ---------- | ---------------------------------------------------------------- | ----------- |
| `"..."`    | Protege uma string, mas reconhece \$, \ e \` como especiais      | "abc"       |
| `'...'`    | Protege uma string completamente (nenhum caractere é especial)   | 'abc'       |
| `$'...'`   | Protege uma string completamente, mas interpreta \n, \t, \a, etc | \$'abc\n'   |
| `...`      | Executa comandos numa subshell, retornando o resultado           | `ls`        |
| `{...}`    | Agrupa comandos em um bloco                                      | { ls ; }    |
| `(...)`    | Executa comandos numa subshell                                   | ( ls )      |
| `$(...)`   | Executa comandos numa subshell, retornando o resultado           | \$( ls )    |
| `((...))`  | Testa uma operação aritmética, retornando 0 ou 1                 | ((5 > 3))   |
| `$((...))` | Retorna o resultado de uma operação aritmética                   | \$((5+3))   |
| `[...]`    | Testa uma expressão, retornando 0 ou 1 (alias do comando 'test') | [ 5 -gt 3 ] |
| `[[...]]`  | Testa uma expressão, retornando 0 ou 1 (podendo usar && e \|\|)  | [[ 5 > 3 ]] |

## if, for, select, while, until, case

| if                                                       |
| -------------------------------------------------------- |
| `if COMANDO then ... elif COMANDO then ... else ... fi ` |

| for / select                                                |
| ----------------------------------------------------------- |
| `for VAR in LISTA do ... done `ou `for ((exp1;exp2;exp3)) ` |

| **while / until**            |
| ---------------------------- |
| `while COMANDO do ... done ` |

| **case**                                                              |
| --------------------------------------------------------------------- |
| `case $VAR in txt1) ... ;; txt2) ... ;; txtN) ... ;; *) ... ;; esac ` |

## Opções do comando test ou [

| Comparação Numérica       |                                         |
| ------------------------- | --------------------------------------- |
| `-lt`                     | É menor que (LessThan)                  |
| `-gt`                     | É maior que (GreaterThan)               |
| `-le`                     | É menor igual (LessEqual)               |
| `-ge`                     | É maior igual (GreaterEqual)            |
| `-eq`                     | É igual (EQual)                         |
| `-ne`                     | É diferente (NotEqual)                  |
| **Comparação de Strings** |                                         |
| `=`                       | É igual                                 |
| `!=`                      | É diferente                             |
| `-n`                      | É não nula                              |
| `-z`                      | É nula                                  |
| **Operadores Lógicos**    |                                         |
| `!`                       | NÃO lógico (NOT)                        |
| `-a`                      | E lógico (AND)                          |
| `-o`                      | OU lógico (OR)                          |
| **Testes em arquivos**    |                                         |
| `-b`                      | É um dispositivo de bloco               |
| `-c`                      | É um dispositivo de caractere           |
| `-d`                      | É um diretório                          |
| `-e`                      | O arquivo existe                        |
| `-f`                      | É um arquivo normal                     |
| `-g`                      | O bit SGID está ativado                 |
| `-G`                      | O grupo do arquivo é o do usuário atual |
| `-k`                      | O sticky-bit está ativado               |
| `-L`                      | O arquivo é um link simbólico           |
| `-O`                      | O dono do arquivo é o usuário atual     |
| `-p`                      | O arquivo é um named pipe               |
| `-r`                      | O arquivo tem permissão de leitura      |
| `-s`                      | O tamanho do arquivo é maior que zero   |
| `-S`                      | O arquivo é um socket                   |
| `-t`                      | O descritor de arquivos N é um terminal |
| `-u`                      | O bit SUID está ativado                 |
| `-w`                      | O arquivo tem permissão de escrita      |
| `-x`                      | O arquivo tem permissão de execução     |
| `-nt`                     | O arquivo é mais recente (NewerThan)    |
| `-ot`                     | O arquivo é mais antigo (OlderThan)     |
| `-ef`                     | O arquivo é o mesmo (EqualFile)         |

## Escapes especiais para usar no prompt (PS1)

| Escape | Lembrete      | Expande para...                                         |
| ------ | ------------- | ------------------------------------------------------- |
| \a     | _Alerta_      | Alerta (bipe)                                           |
| \d     | _Data_        | Data no formato "Dia-da-semana Mês Dia" (Sat Jan 15)    |
| \e     | _Escape_      | Caractere Esc                                           |
| \h     | _Hostname_    | Nome da máquina sem o domínio (dhcp11)                  |
| \H     | _Hostname_    | Nome completo da máquina (dhcp11.empresa)               |
| \j     | _Jobs_        | Número de jobs ativos                                   |
| \l     | _Tty_         | Nome do terminal corrente (ttyp1)                       |
| \n     | _Newline_     | Linha nova                                              |
| \r     | _Return_      | Retorno de carro                                        |
| \s     | _Shell_       | Nome do shell (basename \$0)                            |
| \t     | _Time_        | Horário no formato 24 horas HH:MM:SS                    |
| \T     | _Time_        | Horário no formato 12 horas HH:MM:SS                    |
| \@     | _At_          | Horário no formato 12 horas HH:MM am/pm                 |
| \A     | _At_          | Horário no formato 24 horas HH:MM                       |
| \u     | _Usuário_     | Login do usuário corrente                               |
| \v     | _Versão_      | Versão do Bash (2.00)                                   |
| \V     | _Versão_      | Versão+subversão do Bash (2.00.0)                       |
| \w     | _Working Dir_ | Diretório corrente, caminho completo (\$PWD)            |
| \W     | _Working Dir_ | Diretório corrente, somente o último (basename \$PWD)   |
| \!     | _Histórico_   | Número do comando corrente no histórico                 |
| \#     | _Número_      | Número do comando corrente                              |
| \$     | _ID_          | Mostra "#" se for root, "\$" se for usuário normal      |
| \nnn   | _Octal_       | Caractere cujo octal é nnn                              |
| \\     | _Backslash_   | Barra invertida \ literal                               |
| \[     | _Escapes_     | Inicia uma seqüência de escapes (tipo códigos de cores) |
| \]     | _Escapes_     | Termina uma seqüência de escapes                        |

## Escapes reconhecidos pelo comando _echo_

| Escape | Lembrete    | Descrição                       |
| ------ | ----------- | ------------------------------- |
| \a     | _Alerta_    | Alerta (bipe)                   |
| \b     | _Backspace_ | Caractere Backspace             |
| \c     | _EOS_       | Termina a string                |
| \e     | _Escape_    | Caractere Esc                   |
| \f     | _Form feed_ | Alimentação                     |
| \n     | _Newline_   | Linha nova                      |
| \r     | _Return_    | Retorno de carro                |
| \t     | _Tab_       | Tabulação horizontal            |
| \v     | _Vtab_      | Tabulação vertical              |
| \\     | _Backslash_ | Barra invertida \ literal       |
| \nnn   | _Octal_     | Caractere cujo octal é nnn      |
| \xnn   | _Hexa_      | Caractere cujo hexadecimal é nn |

## Formatadores do comando _date_

| Formato | Descrição                                    |
| ------- | -------------------------------------------- |
| `%a`    | Nome do dia da semana abreviado (Dom..Sáb)   |
| `%A`    | Nome do dia da semana (Domingo..Sábado)      |
| `%b`    | Nome do mês abreviado (Jan..Dez)             |
| `%B`    | Nome do mês (Janeiro..Dezembro)              |
| `%c`    | Data completa (Sat Nov 04 12:02:33 EST 1989) |
| `%y`    | Ano (dois dígitos)                           |
| `%Y`    | Ano (quatro dígitos)                         |
| `%m`    | Mês (01..12)                                 |
| `%d`    | Dia (01..31)                                 |
| `%j`    | Dia do ano (001..366)                        |
| `%H`    | Horas (00..23)                               |
| `%M`    | Minutos (00..59)                             |
| `%S`    | Segundos (00..60)                            |
| `%s`    | Segundos desde 1º de Janeiro de 1970         |
| `%%`    | Um % literal                                 |
| `%t`    | Um TAB                                       |
| `%n`    | Uma quebra de linha                          |

## Formatadores do comando _printf_

| Formato | Descrição                          |
| ------- | ---------------------------------- |
| `%d`    | Número decimal                     |
| `%o`    | Número octal                       |
| `%x`    | Número hexadecimal (a-f)           |
| `%X`    | Número hexadecimal (A-F)           |
| `%f`    | Número com ponto flutuante         |
| `%e`    | Número em notação científica (e+1) |
| `%E`    | Número em notação científica (E+1) |
| `%s`    | String                             |

## Letras identificadoras de arquivos no comando _ls -l_

| Letra | Lembrete  | Tipos de Arquivo (primeiro caractere)                                |
| ----- | --------- | -------------------------------------------------------------------- |
| -     | -         | Arquivo normal                                                       |
| d     | Directory | Diretório                                                            |
| l     | Link      | Link simbólico                                                       |
| b     | Block     | Dispositivo de blocos (HD)                                           |
| c     | Char      | Dispositivo de caracteres (modem serial)                             |
| s     | Socket    | Socket mapeado em arquivo (comunicação de processos)                 |
| p     | Pipe      | FIFO ou Named Pipe (comunicação de processos)                        |
| Letra | Lembrete  | Permissões do Arquivo (próximos nove caracteres)                     |
| -     | -         | Permissão desativada                                                 |
| r     | Read      | Acesso de leitura                                                    |
| w     | Write     | Acesso de escrita                                                    |
| x     | eXecute   | Acesso de execução (ou acesso ao diretório)                          |
| X     | eXecute   | Acesso ao diretório somente                                          |
| s     | Set ID    | Usuário/grupo para execução (SUID, SGID) - permissão 'x' ativada     |
| S     | Set ID    | Usuário/grupo para execução (SUID, SGID) - permissão 'x' desativada  |
| t     | sTicky    | Usuários só apagam seus próprios arquivos - permissão 'x' ativada    |
| T     | sTicky    | Usuários só apagam seus próprios arquivos - permissão 'x' desativada |

## Curingas para nomes de arquivo (glob)

| Curinga  | Casa com...                                  | Exemplo              |
| -------- | -------------------------------------------- | -------------------- |
| `*`      | Qualquer coisa                               | `*.txt`              |
| `?`      | Um caractere qualquer                        | `arquivo-??.zip`     |
| `[...]`  | Qualquer um dos caracteres listados          | `[Aa]rquivo.txt`     |
| `[^...]` | Qualquer um caractere, exceto os listados    | `[^A-Z]*.txt`        |
| `{...}`  | Qualquer um dos textos separados por vírgula | `arquivo.{txt,html}` |

## Curingas para os itens do comando _case_

| Curinga  | Casa com...                               | Exemplo                                 |
| -------- | ----------------------------------------- | --------------------------------------- |
| `*`      | Qualquer coisa                            | `*.txt) echo ;;`                        |
| `?`      | Um caractere qualquer                     | `arquivo-??.zip) echo ;;`               |
| `[...]`  | Qualquer um dos caracteres listados       | `[0-9]) echo ;;`                        |
| `[^...]` | Qualquer um caractere, exceto os listados | `[^0-9]) echo ;;`                       |
| `...     | ...`                                      | Qualquer um dos textos separados por \| | `txt | html) echo ;;` |

## Sinais para usar com _trap/kill/killall_

| #   | Linux  | Cygwin | SystemV | AIX     | HP-UX  | Solaris | BSD/Mac |
| --- | ------ | ------ | ------- | ------- | ------ | ------- | ------- |
| 1   | HUP    | HUP    | HUP     | HUP     | HUP    | HUP     | HUP     |
| 2   | INT    | INT    | INT     | INT     | INT    | INT     | INT     |
| 3   | QUIT   | QUIT   | QUIT    | QUIT    | QUIT   | QUIT    | QUIT    |
| 4   | ILL    | ILL    | ILL     | ILL     | ILL    | ILL     | ILL     |
| 5   | TRAP   | TRAP   | TRAP    | TRAP    | TRAP   | TRAP    | TRAP    |
| 6   | ABRT   | ABRT   | IOT     | LOST    | ABRT   | ABRT    | ABRT    |
| 7   | BUS    | EMT    | EMT     | EMT     | EMT    | EMT     | EMT     |
| 8   | FPE    | FPE    | FPE     | FPE     | FPE    | FPE     | FPE     |
| 9   | KILL   | KILL   | KILL    | KILL    | KILL   | KILL    | KILL    |
| 10  | USR1   | BUS    | BUS     | BUS     | BUS    | BUS     | BUS     |
| 11  | SEGV   | SEGV   | SEGV    | SEGV    | SEGV   | SEGV    | SEGV    |
| 12  | USR2   | SYS    | SYS     | SYS     | SYS    | SYS     | SYS     |
| #   | Linux  | Cygwin | SystemV | AIX     | HP-UX  | Solaris | BSD/Mac |
| 13  | PIPE   | PIPE   | PIPE    | PIPE    | PIPE   | PIPE    | PIPE    |
| 14  | ALRM   | ALRM   | ALRM    | ALRM    | ALRM   | ALRM    | ALRM    |
| 15  | TERM   | TERM   | TERM    | TERM    | TERM   | TERM    | TERM    |
| 16  | -      | URG    | USR1    | URG     | USR1   | USR1    | URG     |
| 17  | CHLD   | STOP   | USR2    | STOP    | USR2   | USR2    | STOP    |
| 18  | CONT   | TSTP   | CHLD    | TSTP    | CHLD   | CHLD    | TSTP    |
| 19  | STOP   | CONT   | PWR     | CONT    | PWR    | PWR     | CONT    |
| 20  | TSTP   | CHLD   | WINCH   | CHLD    | VTALRM | WINCH   | CHLD    |
| 21  | TTIN   | TTIN   | URG     | TTIN    | PROF   | URG     | TTIN    |
| 22  | TTOU   | TTOU   | IO      | TTOU    | IO     | IO      | TTOU    |
| 23  | URG    | IO     | STOP    | IO      | WINCH  | STOP    | IO      |
| 24  | XCPU   | XCPU   | TSTP    | XCPU    | STOP   | TSTP    | XCPU    |
| #   | Linux  | Cygwin | SystemV | AIX     | HP-UX  | Solaris | BSD/Mac |
| 25  | XFSZ   | XFSZ   | CONT    | XFSZ    | TSTP   | CONT    | XFSZ    |
| 26  | VTALRM | VTALRM | TTIN    | -       | CONT   | TTIN    | VTALRM  |
| 27  | PROF   | PROF   | TTOU    | MSG     | TTIN   | TTOU    | PROF    |
| 28  | WINCH  | WINCH  | VTALRM  | WINCH   | TTOU   | VTALRM  | WINCH   |
| 29  | IO     | LOST   | PROF    | PWR     | URG    | PROF    | INFO    |
| 30  | PWR    | USR1   | XCPU    | USR1    | LOST   | XCPU    | USR1    |
| 31  | SYS    | USR2   | XFSZ    | USR2    | -      | XFSZ    | USR2    |
| 32  | -      | -      | -       | PROF    | -      | WAITING | -       |
| 33  | -      | -      | -       | DANGER  | -      | LWP     | -       |
| 34  | -      | -      | -       | VTALRM  | -      | FREEZE  | -       |
| 35  | -      | -      | -       | MIGRATE | -      | THAW    | -       |
| 36  | -      | -      | -       | PRE     | -      | CANCEL  | -       |
| 37  | -      | -      | -       | -       | -      | LOST    | -       |

## Códigos de retorno de comandos

| Código | Significado                                    | Exemplo                  |
| ------ | ---------------------------------------------- | ------------------------ |
| 0      | Nenhum erro, execução terminou OK              | echo                     |
| 1      | A maioria dos erros comuns na execução         | echo \$((1/0))           |
| 2      | Erro de uso em algum 'builtin' do Shell        | -                        |
| 126    | Comando não executável (sem permissão)         | touch a ; ./a            |
| 127    | Comando não encontrado ("command not found")   | echooo                   |
| 128    | O parâmetro para o 'exit' não é um decimal     | exit 1.0                 |
| 128+n  | 128 + código do sinal que o matou              | kill -9 \$PPID #exit 137 |
| 130    | O programa interrompido com o Ctrl+C (128 + 2) | -                        |
| 255    | Parâmetro para o 'exit' não está entre 0 e 255 | exit -1                  |

## Códigos de cores (ANSI)

| Cor      | Letra | Fundo |
| -------- | ----- | ----- |
| Preto    | 30    | 40    |
| Vermelho | 31    | 41    |
| Verde    | 32    | 42    |
| Amarelo  | 33    | 43    |
| Azul     | 34    | 44    |
| Rosa     | 35    | 45    |
| Ciano    | 36    | 46    |
| Branco   | 37    | 47    |

| Atributo   | Valor |
| ---------- | ----- |
| Reset      | 0     |
| Negrito    | 1     |
| Sublinhado | 4     |
| Piscando   | 5     |
| Reverso    | 7     |

| Exemplos:                    |               |
| ---------------------------- | ------------- |
| ESC                          | `<N>`;`<N>` m |
| Texto normal (desliga cores) | `ESC[m`       |
| Negrito                      | `ESC[1m`      |
| Amarelo                      | `ESC[33;1m`   |
| Fundo azul, letra cinza      | `ESC[44;37m`  |
| Vermelho piscando            | `ESC[31;5m`   |

Na linha de comando:

`echo -e '\e[33;1m amarelo \e[m'`  
`echo -e '\033[33;1m amarelo \033[m'`

![img](https://aurelio.net/shell/canivete/zzcores.gif)

## Os metacaracteres das expressões regulares

| Meta | Nome         | Descrição                                                      |
| ---- | ------------ | -------------------------------------------------------------- |
| .    | Ponto        | Curinga de um caractere                                        |
| []   | Lista        | Casa qualquer um dos caracteres listados                       |
| [^]  | Lista negada | Casa qualquer caractere, exceto os listados                    |
| ?    | Opcional     | O item anterior pode aparecer ou não (opcional)                |
| \*   | Asterisco    | O item anterior pode aparecer em qualquer quantidade           |
| +    | Mais         | O item anterior deve aparecer no mínimo uma vez                |
| {,}  | Chaves       | O item anterior deve aparecer na quantidade indicada {mín,máx} |
| ^    | Circunflexo  | Casa o começo da linha                                         |
| \$   | Cifrão       | Casa o fim da linha                                            |
| \b   | Borda        | Limita uma palavra (letras, números e sublinhado)              |
| \    | Escape       | Escapa um meta, tirando seu poder                              |
| \|   | Ou           | Indica alternativas (usar com o grupo)                         |
| ()   | Grupo        | Agrupa partes da expressão, é quantificável e multinível       |
| \1   | Retrovisor   | Recupera o conteúdo do grupo 1                                 |
| \2   | Retrovisor   | Recupera o conteúdo do grupo 2 (segue até o \9)                |
| .\*  | Curinga      | Casa qualquer coisa, é o tudo e o nada                         |
| ??   | Opcional NG  | Idem ao opcional comum, mas casa o mínimo possível             |
| \*?  | Asterisco NG | Idem ao asterisco comum, mas casa o mínimo possível            |
| +?   | Mais NG      | Idem ao mais comum, mas casa o mínimo possível                 |
| {}?  | Chaves NG    | Idem às chaves comuns, mas casa o mínimo possível              |

## Metacaracteres que são diferentes nos aplicativos

| Programa | Opc | Mais | Chaves | Borda | Ou  | Grupo |
| -------- | --- | ---- | ------ | ----- | --- | ----- |
| awk      | ?   | +    | -      | -     | \|  | ()    |
| ed       | \?  | \+   | \{,\}  | \b    | \|  | \(\)  |
| egrep    | ?   | +    | {,}    | \b    | \|  | ()    |
| emacs    | ?   | +    | -      | \b    | \|  | \(\)  |
| expect   | ?   | +    | -      | -     | \|  | ()    |
| find     | ?   | +    | -      | \b    | \|  | \(\)  |
| gawk     | ?   | +    | {,}    | \<\>  | \|  | ()    |
| grep     | \?  | \+   | \{,\}  | \b    | \|  | \(\)  |
| mawk     | ?   | +    | -      | -     | \|  | ()    |
| perl     | ?   | +    | {,}    | \b    | \|  | ()    |
| php      | ?   | +    | {,}    | \b    | \|  | ()    |
| python   | ?   | +    | {,}    | \b    | \|  | ()    |
| sed      | \?  | \+   | \{,\}  | \<\>  | \|  | \(\)  |
| vim      | \=  | \+   | \{,}   | \<\>  | \|  | \(\)  |

## Caracteres ASCII imprimíveis (ISO-8859-1) - texto

```text
$ zzascii
32        64  @     96  `    162  ¢    194  Â    226  â
33  !     65  A     97  a    163  £    195  Ã    227  ã
34  "     66  B     98  b    164  ¤    196  Ä    228  ä
35  #     67  C     99  c    165  ¥    197  Å    229  å
36  $     68  D    100  d    166  ¦    198  Æ    230  æ
37  %     69  E    101  e    167  §    199  Ç    231  ç
38  &     70  F    102  f    168  ¨    200  È    232  è
39  '     71  G    103  g    169  ©    201  É    233  é
40  (     72  H    104  h    170  ª    202  Ê    234  ê
41  )     73  I    105  i    171  «    203  Ë    235  ë
42  *     74  J    106  j    172  ¬    204  Ì    236  ì
43  +     75  K    107  k    173       205  Í    237  í
44  ,     76  L    108  l    174  ®    206  Î    238  î
45  -     77  M    109  m    175  ¯    207  Ï    239  ï
46  .     78  N    110  n    176  °    208  Ð    240  ð
47  /     79  O    111  o    177  ±    209  Ñ    241  ñ
48  0     80  P    112  p    178  ²    210  Ò    242  ò
49  1     81  Q    113  q    179  ³    211  Ó    243  ó
50  2     82  R    114  r    180  ´    212  Ô    244  ô
51  3     83  S    115  s    181  µ    213  Õ    245  õ
52  4     84  T    116  t    182  ¶    214  Ö    246  ö
53  5     85  U    117  u    183  ·    215  ×    247  ÷
54  6     86  V    118  v    184  ¸    216  Ø    248  ø
55  7     87  W    119  w    185  ¹    217  Ù    249  ù
56  8     88  X    120  x    186  º    218  Ú    250  ú
57  9     89  Y    121  y    187  »    219  Û    251  û
58  :     90  Z    122  z    188  ¼    220  Ü    252  ü
59  ;     91  [    123  {    189  ½    221  Ý    253  ý
60  <     92  \    124  |    190  ¾    222  Þ    254  þ
61  =     93  ]    125  }    191  ¿    223  ß    255  ÿ
62  >     94  ^    126  ~    192  À    224  à
63  ?     95  _    161  ¡    193  Á    225  á
```

## Caracteres ASCII imprimíveis (ISO-8859-1) - imagem

![img](https://aurelio.net/shell/canivete/ascii.gif)

## Códigos prontos para copiar e colar

| Condicionais com o IF                                                                    |
| ---------------------------------------------------------------------------------------- |
| `if [ -f "$arquivo" ]; then echo 'Arquivo encontrado'; fi`                               |
| `if [ ! -d "$dir" ]; then echo 'Diretório não encontrado'; fi`                           |
| `if [ $i -gt 5 ]; then echo 'Maior que 5'; else echo 'Menor que 5'; fi`                  |
| `if [ $i -ge 5 -a $i -le 10 ]; then echo 'Entre 5 e 10, incluindo'; fi`                  |
| `if [ $i -eq 5 ]; then echo '=5'; elif [ $i -gt 5 ]; then echo '>5'; else echo '<5'; fi` |
| `if [ "$USER" = 'root' ]; then echo 'Oi root'; fi`                                       |
| `if grep -qs 'root' /etc/passwd; then echo 'Usuário encontrado'; fi`                     |
| **Condicionais com o E (&&) e OU (\|\|)**                                                |
| `[ -f "$arquivo" ] && echo 'Arquivo encontrado'`                                         |
| `[ -d "$dir" ]                                                                           |  | echo 'Diretório não encontrado'` |
| `grep -qs 'root' /etc/passwd && echo 'Usuário encontrado'`                               |
| `cd "$dir" && rm "$arquivo" && touch "$arquivo" && echo 'feito!'`                        |
| `[ "$1" ] && param=\$1                                                                   |  | param='valor padrão'` |
| `[ "$1" ] && param=${1:-valor padrão}`                                                   |
| `[ "$1" ]                                                                                |  | { echo "Uso: \$0 parâmetro" ; exit 1 ; }` |
| **Adicionar 1 à variável \$i**                                                           |
| `i=$(expr $i + 1)`                                                                       |
| `i=$((i+1))`                                                                             |
| `let i=i+1`                                                                              |
| `let i+=1`                                                                               |
| `let i++`                                                                                |
| **Loop de 1 à 10**                                                                       |
| `for i in 1 2 3 4 5 6 7 8 9 10; do echo $i; done`                                        |
| `for i in $(seq 10); do echo $i; done`                                                   |
| `for ((i=1;i<=10;i++)); do echo $i; done`                                                |
| `i=1 ; while [ $i -le 10 ]; do echo $i ; i=$((i+1)) ; done`                              |
| `i=1 ; until [ $i -gt 10 ]; do echo $i ; i=$((i+1)) ; done`                              |
| **Loop nas linhas de um arquivo ou saída de comando**                                    |
| `cat /etc/passwd                                                                         | while read LINHA; do echo "\$LINHA"; done` |
| `grep 'root' /etc/passwd                                                                 | while read LINHA; do echo "\$LINHA"; done` |
| `while read LINHA; do echo "$LINHA"; done < /etc/passwd`                                 |
| `while read LINHA; do echo "$LINHA"; done < <(grep 'root' /etc/passwd)`                  |
| **Curingas nos itens do comando case**                                                   |
| `case "$dir" in /home/*) echo 'dir dentro do /home';; esac`                              |
| `case "\$user" in root                                                                   | joao | maria) echo "Oi \$user";; \*) echo "Não te conheço";; esac` |
| `case "$var" in ?) echo '1 letra';; ??) echo '2 letras';; ??*) echo 'mais de 2';; esac`  |
| `case "$i" in [0-9]) echo '1 dígito';; [0-9][0-9]) echo '2 dígitos';; esac`              |
| **Caixas do Dialog**                                                                     |
| `dialog --calendar 'abc' 0 0 31 12 1999`                                                 |
| `dialog --checklist 'abc' 0 0 0 item1 'desc1' on item2 'desc2' off`                      |
| `dialog --fselect /tmp 0 0`                                                              |
| `(echo 50; sleep 2; echo 100)                                                            | dialog --gauge 'abc' 8 40 0` |
| `dialog --infobox 'abc' 0 0`                                                             |
| `dialog --inputbox 'abc' 0 0`                                                            |
| `dialog --passwordbox 'abc' 0 0`                                                         |
| `dialog --menu 'abc' 0 0 0 item1 'desc1' item2 'desc2'`                                  |
| `dialog --msgbox 'abc' 8 40`                                                             |
| `dialog --radiolist 'abc' 0 0 0 item1 'desc1' on item2 'desc2' off`                      |
| `dialog --tailbox /tmp/arquivo.txt 0 0`                                                  |
| `dialog --textbox /tmp/arquivo.txt 0 0`                                                  |
| `dialog --timebox 'abc' 0 0 23 59 00`                                                    |
| `dialog --yesno 'abc' 0 0`                                                               |
| **Dica1:** `dialog ... && echo 'Apertou OK/Yes'                                          |  | echo 'Apertou Cancel/No'` |
| **Dica2:** `resposta=$(dialog --stdout --TIPODACAIXA 'abc' ...)`                         |

## Atalhos da linha de comando (_set -o emacs_)

| Atalho | Descrição                                     | Tecla Similar |
| ------ | --------------------------------------------- | ------------- |
| Ctrl+A | Move o cursor para o início da linha          | Home          |
| Ctrl+B | Move o cursor uma posição à esquerda          | ←             |
| Ctrl+C | Envia sinal EOF() para o sistema              |               |
| Ctrl+D | Apaga um caractere à direita                  | Delete        |
| Ctrl+E | Move o cursor para o fim da linha             | End           |
| Ctrl+F | Move o cursor uma posição à direita           | →             |
| Ctrl+H | Apaga um caractere à esquerda                 | Backspace     |
| Ctrl+I | Completa arquivos e comandos                  | Tab           |
| Ctrl+J | Quebra a linha                                | Enter         |
| Ctrl+K | Recorta do cursor até o fim da linha          |               |
| Ctrl+L | Limpa a tela (igual ao comando clear)         |               |
| Ctrl+N | Próximo comando                               |               |
| Ctrl+P | Comando anterior                              |               |
| Ctrl+Q | Destrava a shell (veja Ctrl+S)                |               |
| Ctrl+R | Procura no histórico de comandos              |               |
| Ctrl+S | Trava a shell (veja Ctrl+Q)                   |               |
| Ctrl+T | Troca dois caracteres de lugar                |               |
| Ctrl+U | Recorta a linha inteira                       |               |
| Ctrl+V | Insere caractere literal                      |               |
| Ctrl+W | Recorta a palavra à esquerda                  |               |
| Ctrl+X | Move o cursor para o início/fim da linha (2x) | Home/End      |
| Ctrl+Y | Cola o trecho recortado                       |               |

## Comandos gerais úteis

| Comando    | Função                | Opções úteis                             |
| ---------- | --------------------- | ---------------------------------------- |
| **cat**    | _Mostra arquivo_      | -n, -s                                   |
| **cut**    | _Extrai campo_        | -d -f, -c                                |
| **date**   | _Mostra data_         | -d, +'...'                               |
| **diff**   | _Compara arquivos_    | -u, -Nr, -i, -w                          |
| **echo**   | _Mostra texto_        | -e, -n                                   |
| **find**   | _Encontra arquivos_   | -name, -iname, -type f, -exec, -or       |
| **fmt**    | _Formata parágrafo_   | -w, -u                                   |
| **grep**   | _Encontra texto_      | -i, -v, -r, -qs, -n, -l, -w -x, -A -B -C |
| **head**   | _Mostra início_       | -n, -c                                   |
| **od**     | _Mostra caracteres_   | -a, -c, -o, -x                           |
| **paste**  | _Paraleliza arquivos_ | -d, -s                                   |
| **printf** | _Mostra texto_        | _nenhuma_                                |
| **rev**    | _Inverte texto_       | _nenhuma_                                |
| **sed**    | _Edita texto_         | -n, -f, s/isso/aquilo/, p, d, q, N       |
| **seq**    | _Conta números_       | -s, -f                                   |
| **sort**   | _Ordena texto_        | -n, -f, -r, -k -t, -o                    |
| **tac**    | _Inverte arquivo_     | _nenhuma_                                |
| **tail**   | _Mostra final_        | -n, -c, -f                               |
| **tee**    | _Arquiva fluxo_       | -a                                       |
| **tr**     | _Transforma texto_    | -d, -s, A-Z a-z                          |
| **uniq**   | _Remove duplicatas_   | -i, -d, -u                               |
| **wc**     | _Conta letras_        | -c, -w, -l, -L                           |
| **xargs**  | _Gerencia argumentos_ | -n, -i                                   |

---

## Miniman

O miniman é uma versão rápida e resumida das páginas de manual(_man_), com tabelas que listam somente as opções mais utilizadas dos comandos mais utilizados.

### cat

| Opção | Lembrete | Descrição                                               |
| ----- | -------- | ------------------------------------------------------- |
| -n    | Number   | Numera as linhas (Formato: Espaços, Número, TAB, Linha) |
| -s    | Squeeze  | Remove as linhas em branco excedentes                   |

### cut

| Opção | Lembrete  | Descrição                                      |
| ----- | --------- | ---------------------------------------------- |
| -d    | Delimiter | Escolhe o delimitador (o padrão é o TAB)       |
| -f    | Field     | Mostra estes campos (veja tabela seguinte)     |
| -c    | Chars     | Mostra estes caracteres (veja tabela seguinte) |

| -f e -c | Abrange     | Significa                                   |
| ------- | ----------- | ------------------------------------------- |
| 2,5     | 2 5         | O segundo e o quinto                        |
| 2-5     | 2 3 4 5     | Do segundo ao quinto                        |
| 2-      | 2 3 4 5 …   | Do segundo em diante                        |
| -5      | 1 2 3 4 5   | Até o quinto                                |
| 2,5-    | 2 5 6 7 …   | O segundo e do quinto em diante             |
| 2,3,5-8 | 2 3 5 6 7 8 | O segundo, o terceiro e do quinto ao oitavo |

### date

| Opção | Lembrete | Descrição                                              |
| ----- | -------- | ------------------------------------------------------ |
| -d    | Date     | Especifica a data (Ex.: tomorrow, 2 days ago, 5 weeks) |
| +%?   |          | Formato da data – veja tabela seguinte (Ex.: %Y-%m-%d) |

| Formato | Descrição do caractere de formatação         |
| ------- | -------------------------------------------- |
| %a      | Nome do dia da semana abreviado (Dom..Sáb)   |
| %A      | Nome do dia da semana (Domingo..Sábado)      |
| %b      | Nome do mês abreviado (Jan..Dez)             |
| %B      | Nome do mês (Janeiro..Dezembro)              |
| %c      | Data completa (Sat Nov 04 12:02:33 EST 1989) |
| %y      | Ano (dois dígitos)                           |
| %Y      | Ano (quatro dígitos)                         |
| %m      | Mês (01..12)                                 |
| %d      | Dia (01..31)                                 |
| %j      | Dia do ano (001..366)                        |
| %H      | Horas (00..23)                               |
| %M      | Minutos (00..59)                             |
| %S      | Segundos (00..60)                            |
| %s      | Segundos desde 1º de Janeiro de 1970         |
| %%      | Um % literal                                 |
| %t      | Um TAB                                       |
| %n      | Uma quebra de linha                          |

### diff

| Opção | Lembrete    | Descrição                                             |
| ----- | ----------- | ----------------------------------------------------- |
| -u    | Unified     | Formato unificado (com contexto e os sinais de + e -) |
| -C    | Context     | Indica a quantidade de linhas usadas para o contexto  |
| -r    | Recursive   | Varre todo o diretório                                |
| -N    | New file    | Considera arquivos não-encontrados como vazios        |
| -i    | Ignore case | Ignora a diferença entre maiúsculas e minúsculas      |
| -w    | White space | Ignora a diferença de linhas e espaços em branco      |

### echo

| Opção | Lembrete | Descrição                                             |
| ----- | -------- | ----------------------------------------------------- |
| -n    | Newline  | Não quebra a linha no final                           |
| -e    | Escape   | Interpreta os escapes especiais (ver tabela seguinte) |

| Escape | Lembrete  | Descrição                       |
| ------ | --------- | ------------------------------- |
| \a     | Alert     | Alerta (bipe)                   |
| \b     | Backspace | Caractere Backspace             |
| \c     | EOS       | Termina a string                |
| \e     | Escape    | Caractere Esc                   |
| \f     | Form feed | Alimentação                     |
| \n     | Newline   | Linha nova                      |
| \r     | Return    | Retorno de carro                |
| \t     | Tab       | Tabulação horizontal            |
| \v     | Vtab      | Tabulação vertical              |
| \\     | Backslash | Barra invertida \ literal       |
| \nnn   | Octal     | Caractere cujo octal é nnn      |
| \xnn   | Hexa      | Caractere cujo hexadecimal é nn |

### find

| Opção     | Descrição                                                       |
| --------- | --------------------------------------------------------------- |
| -name     | Especifica o nome do arquivo (ou _parte_ dele)                  |
| -iname    | Ignora a diferença entre maiúsculas e minúsculas no nome        |
| -type     | Especifica o tipo do arquivo (f=arquivo, d=diretório, l=link)   |
| -mtime    | Mostra os arquivos modificados há N dias                        |
| -size     | Mostra os arquivos que possuem o tamanho especificado           |
| -user     | Mostra os arquivos de um usuário específico                     |
| -ls       | Mostra os arquivos no mesmo formato do comando ls               |
| -printf   | Formatação avançada para mostrar os nomes dos arquivos          |
| -exec     | Executa um comando com os arquivos encontrados                  |
| -ok       | Executa um comando com os arquivos encontrados, com confirmação |
| -and, -or | E, OU lógico para as condições                                  |
| -not      | Inverte a lógica da expressão                                   |

| Detalhes das opções -exec e -ok                                                   |
| --------------------------------------------------------------------------------- |
| A string {} representa o nome do arquivo encontrado                               |
| O comando deve ser passado sem aspas                                              |
| O comando deve ser terminado por um ponto-e-vírgula escapado \;                   |
| Tem que ter um espaço antes do ponto-e-vírgula escapado                           |
| Mover os arquivos .txt para .txt.old: find . -name '\*.txt' -exec mv {} {}.old \; |

### fmt

| Opção | Lembrete | Descrição                                         |
| ----- | -------- | ------------------------------------------------- |
| -w    | Width    | Define o número máximo de colunas (o padrão é 75) |
| -u    | Uniform  | Remove espaços excedentes                         |

### grep

| Opção | Lembrete    | Descrição                                            |
| ----- | ----------- | ---------------------------------------------------- |
| -i    | Ignore case | Ignora a diferença entre maiúsculas e minúsculas     |
| -v    | Invert      | Mostra as linhas que não casam com o padrão          |
| -r    | Recursive   | Varre subdiretórios também                           |
| -q    | Quiet       | Não mostra as linhas que encontrar (usar com o test) |
| -s    | Silent      | Não mostra os erros (usar com o test)                |
| -n    | Number      | Mostra também o número da linha                      |
| -c    | Count       | Conta o número de linhas encontradas                 |
| -l    | Filename    | Mostra apenas o nome o arquivo que casou             |
| -w    | Word        | O padrão é uma palavra inteira, e não parte dela     |
| -x    | Full line   | O padrão é uma linha inteira, e não parte dela       |
| -A    | After       | Mostre N linhas de contexto depois do padrão         |
| -B    | Before      | Mostre N linhas de contexto antes do padrão          |
| -C    | Context     | Mostre N linhas de contexto antes e depois do padrão |

| As identidades do grep |                                             |
| ---------------------- | ------------------------------------------- |
| grep                   | Procura por uma expressão regular básica    |
| egrep ou grep -E       | Procura por uma expressão regular estendida |
| fgrep ou grep -F       | Procura por uma string                      |

| Metacaracteres              |                                  |
| --------------------------- | -------------------------------- |
| Expressão regular básica    | ^ \$ . \* [ \? \+ \| \( \) \{ \} |
| Expressão regular estendida | ^ \$ . \* [ ? + \| ( ) { }       |

### head

| Opção | Lembrete | Descrição                                       |
| ----- | -------- | ----------------------------------------------- |
| -n    | Lines    | Mostra as N primeiras linhas (o padrão é 10)    |
| -c    | Char     | Mostra os N primeiros caracteres (incluindo \n) |

### od

| Opção | Lembrete | Descrição                        |
| ----- | -------- | -------------------------------- |
| -a    | Name     | Mostra os nomes dos caracteres   |
| -c    | ASCII    | Mostra os caracteres ASCII       |
| -o    | Octal    | Mostra os códigos em octal       |
| -x    | Hexa     | Mostra os códigos em hexadecimal |

### paste

| Opção | Lembrete  | Descrição                                |
| ----- | --------- | ---------------------------------------- |
| -d    | Delimiter | Escolhe o delimitador (o padrão é o TAB) |
| -s    | Serial    | Transforma todas as linhas em apenas uma |

### printf

| Formato | Lembrete | Descrição                          |
| ------- | -------- | ---------------------------------- |
| %d      | Decimal  | Número decimal                     |
| %o      | Octal    | Número octal                       |
| %x      | Hexa     | Número hexadecimal (a-f)           |
| %X      | Hexa     | Número hexadecimal (A-F)           |
| %f      | Float    | Número com ponto flutuante         |
| %e      |          | Número em notação científica (e+1) |
| %E      |          | Número em notação científica (E+1) |
| %s      | String   | String                             |

### sed

| Opção | Lembrete   | Descrição                                |
| ----- | ---------- | ---------------------------------------- |
| -n    | Not print  | Só mostra a linha caso usado o comando p |
| -e    | Expression | Especifica os comandos de edição         |
| -f    | File       | Lê os comandos de edição de um arquivo   |

| Comando | Lembrete   | Ação                                   |
| ------- | ---------- | -------------------------------------- |
| s///    | Substitute | Troca um texto por outro               |
| p       | Print      | Mostra a linha na saída                |
| l       | List       | Mostra a linha na saída, com \t, \a, … |
| d       | Delete     | Apaga a linha                          |
| q       | Quit       | Sai do sed                             |
| r       | Read       | Lê o conteúdo de um arquivo            |
| N       | Next line  | Junta a próxima linha com a atual      |

| Endereço     | Abrange…                                          |
| ------------ | ------------------------------------------------- |
| 1            | A primeira linha                                  |
| 1,5          | Da primeira linha até a quinta                    |
| 5,\$         | Da quinta linha até a última                      |
| /sed/        | A(s) linha(s) que contém a palavra “sed”          |
| 5,/sed/      | Da quinta linha até a linha que contém “sed”      |
| /sed/,/grep/ | Da linha que contém “sed” até a que contém “grep” |
| 1,5!         | Todas as linhas, exceto da primeira a quinta      |
| /sed/!       | A(s) linha(s) que não contém a palavra “sed”      |

| s/// | Exemplo      | Descrição                                                   |
| ---- | ------------ | ----------------------------------------------------------- |
| g    | s/a/b/g      | Modificador Global, para trocar todas as ocorrências        |
| p    | s/a/b/gp     | Modificador Print, para mostrar o texto substituído         |
| &    | s/./& /      | Expande para todo o trecho casado na primeira parte         |
| \1   | s/\(.\)/\1 / | Expande para o conteúdo do primeiro grupo marcado com \(…\) |

### seq

| Opção | Lembrete  | Descrição                                  |
| ----- | --------- | ------------------------------------------ |
| -s    | Separator | Define o separador (o padrão é \n)         |
| -f    | Format    | Define o formato do número (o padrão é %g) |

### sort

| Opção | Lembrete    | Descrição                                         |
| ----- | ----------- | ------------------------------------------------- |
| -n    | Numeric     | Ordena numericamente (o padrão é alfabeticamente) |
| -r    | Reverse     | Reverte a ordenação (de Z para A, de 9 para 0)    |
| -f    | Ignore case | Ignora a diferença entre maiúsculas e minúsculas  |
| -k    | Key         | Ordena pela coluna N (a primeira é 1)             |
| -t    | Separator   | Escolhe o separador para o -k (o padrão é o TAB)  |
| -o    | Output      | Grava a saída no arquivo especificado             |

### tail

| Opção | Lembrete | Descrição                                     |
| ----- | -------- | --------------------------------------------- |
| -n    | Lines    | Mostra as N últimas linhas (o padrão é 10)    |
| -c    | Char     | Mostra os N últimos caracteres (incluindo \n) |
| -f    | Follow   | Monitora o arquivo ad infinitum               |

### tee

| Opção | Lembrete | Descrição                                           |
| ----- | -------- | --------------------------------------------------- |
| -a    | Append   | Anexa ao final do arquivo (o padrão é sobrescrever) |

### tr

| Opção | Lembrete   | Descrição                                                 |
| ----- | ---------- | --------------------------------------------------------- |
| -s    | Squeeze    | Espreme caracteres iguais consecutivos para apenas um     |
| -d    | Delete     | Apaga todos os caracteres listados                        |
| -c    | Complement | Inverte a lista de caracteres (-c 0-9 é similar a [^0-9]) |

| Argumento | Engloba         |
| --------- | --------------- |
| abc       | “a” e “b” e “c” |
| a7z       | “a” e “7” e “z” |
| a-z       | de “a” até “z”  |
| 0-7       | de zero a sete  |

### uniq

| Opção | Lembrete    | Descrição                                        |
| ----- | ----------- | ------------------------------------------------ |
| -i    | Ignore case | Ignora a diferença entre maiúsculas e minúsculas |
| -d    | Duplicate   | Mostra apenas as linhas que são repetidas        |
| -u    | Unique      | Mostra apenas as linhas que não são repetidas    |

### wc

| Opção | Lembrete | Descrição                               |
| ----- | -------- | --------------------------------------- |
| -c    | Char     | Conta o número de caracteres (bytes)    |
| -w    | Word     | Conta o número de palavras              |
| -l    | Line     | Conta o número de linhas                |
| -L    | Longest  | Mostra o tamanho da linha mais comprida |

## xargs

| Opção | Lembrete | Descrição                               |
| ----- | -------- | --------------------------------------- |
| -n    | Number   | Use N argumentos por linha de comando   |
| -i    | Replace  | Troca a string {} pelo argumento da vez |

---

## Exemplos

By: _Traversy Media - [Brad Traversy github](https://github.com/bradtraversy)_

```bash
# ECHO COMMAND
echo Hello World!

# VARIABLES
# Uppercase by convention
# Letters, numbers, underscores
NAME="Bob"
echo "My name is $NAME"
echo "My name is ${NAME}"

# USER INPUT
read -p "Enter your name: " NAME
echo "Hello $NAME, nice to meet you!"

# SIMPLE IF STATEMENT
if [ "$NAME" == "Brad" ]
then
  echo "Your name is Brad"
fi

# IF-ELSE
if [ "$NAME" == "Brad" ]
then
  echo "Your name is Brad"
else
  echo "Your name is NOT Brad"
fi

# ELSE-IF (elif)
if [ "$NAME" == "Brad" ]
then
  echo "Your name is Brad"
elif [ "$NAME" == "Jack" ]
then
  echo "Your name is Jack"
else
  echo "Your name is NOT Brad or Jack"
fi

# COMPARISON
NUM1=31
NUM2=5
if [ "$NUM1" -gt "$NUM2" ]
then
  echo "$NUM1 is greater than $NUM2"
else
  echo "$NUM1 is less than $NUM2"
fi

########
# val1 -eq val2 Returns true if the values are equal
# val1 -ne val2 Returns true if the values are not equal
# val1 -gt val2 Returns true if val1 is greater than val2
# val1 -ge val2 Returns true if val1 is greater than or equal to val2
# val1 -lt val2 Returns true if val1 is less than val2
# val1 -le val2 Returns true if val1 is less than or equal to val2
########

# FILE CONDITIONS
FILE="test.txt"
if [ -e "$FILE" ]
then
  echo "$FILE exists"
else
  echo "$FILE does NOT exist"
fi

########
# -d file   True if the file is a directory
# -e file   True if the file exists (note that this is not particularly portable, thus -f is generally used)
# -f file   True if the provided string is a file
# -g file   True if the group id is set on a file
# -r file   True if the file is readable
# -s file   True if the file has a non-zero size
# -u    True if the user id is set on a file
# -w    True if the file is writable
# -x    True if the file is an executable
########

#CASE STATEMENT
read -p "Are you 21 or over? Y/N " ANSWER
case "$ANSWER" in
  [yY] | [yY][eE][sS])
    echo "You can have a beer :)"
    ;;
  [nN] | [nN][oO])
    echo "Sorry, no drinking"
    ;;
  *)
    echo "Please enter y/yes or n/no"
    ;;
esac

# SIMPLE FOR LOOP
NAMES="Brad Kevin Alice Mark"
for NAME in $NAMES
  do
    echo "Hello $NAME"
done

# FOR LOOP TO RENAME FILES
FILES=$(ls *.txt)
NEW="new"
for FILE in $FILES
  do
    echo "Renaming $FILE to new-$FILE"
    mv $FILE $NEW-$FILE
done

# WHILE LOOP - READ THROUGH A FILE LINE BY LINE
LINE=1
while read -r CURRENT_LINE
  do
    echo "$LINE: $CURRENT_LINE"
    ((LINE++))
done < "./new-1.txt"

# FUNCTION
function sayHello() {
  echo "Hello World"
}
sayHello

# FUNCTION WITH PARAMS
function greet() {
  echo "Hello, I am $1 and I am $2"
}

greet "Brad" "36"

# CREATE FOLDER AND WRITE TO A FILE
mkdir hello
touch "hello/world.txt"
echo "Hello World" >> "hello/world.txt"
echo "Created hello/world.txt"
```
