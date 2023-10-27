
>## Módulo 01 - Sistemas Operacionais Linux

>### Problema 01
>
>###### Imagine que a Vanessa é uma administradora de sistemas em uma empresa de tecnologia. Ela recebeu a tarefa de criar uma nova conta de usuário para um novo membro da equipe. Vanessa precisa demonstrar seu conhecimento ao explicar o processo para seus colegas de trabalho.
>
>###### **Descreva o processo para criar um novo usuário no Linux, incluindo os comandos e opções utilizadas de forma mais detalhada possível.**

###### **Resolução:**

1. Para começar, inicie a máquina que contém o sistema Linux que você utiliza. Para este tutorial, será utilizada um SO Linux Ubuntu 22.04 virtualizado com VMware Workstation;

1. Realize a conexão com a máquina. Isso pode ser feito via:
    1. console da própria AWS;
    1. via SSH de uma outra máquina, esteja esta rodando em Linux ou qualquer outro Sistema Operacional;
    1. Inicialização da VM ou WSL;

1. Para criar o usuário novo, Vanessa acessou a máquina com seu usuário (que tem permissões para criar usuários). Assim sendo, para criar o usuário `andreiflancanova`, basta digitar:

```bash
sudo adduser andreiflancanova
```

4. Em seguida, basta digitar sua senha, e dessa forma, Vanessa criou o usuário `andreiflancanova`. Um ponto de atenção aqui é que o comando `adduser` cria o usuário e já cria na sequência um grupo e o diretório `/home/andreiflancanova`, como pode ser visto na imagem a seguir:

![so_linux_user_creation_001](https://i.imgur.com/n9dDvT8.png)

5. O próximo passo é definir a senha do usuário, assim como informações de nome (Full Name), número da sala (Room Number) e números de telefone do trabalho (Work Phone) e de casa (Home Phone). Para deixar alguma dessas informações em branco, basta pressionar `enter` para avançar No final do preenchimento das informações, basta digital `y` para confirmar as informações ou `n` para alterar.

![so_linux_user_creation_002](https://i.imgur.com/10BAkj6.png)

Após a criação do usuário com `adduser`, seu diretório irá aparecer dentro do diretório `home`, como pode ser visto após os comandos abaixo:

![so_linux_user_creation_003](https://i.imgur.com/lQolxlc.png)

>### Problema 02
>
<<<<<<< HEAD
<<<<<<< HEAD
>###### Em uma pequena cidade chamada Linuxville, vive o Lucas, um entusiasta de tecnologia. Ele está ajudando seu amigo Rafael a entender o funcionamento das permissões de arquivo no sistema Linux. Lucas decide contar uma história, explicando que os arquivos em Linux são como valiosos tesouros guardados em cofres. Cada cofre possui uma combinação única de permissões, representadas por símbolos especiais. Lucas usa essa analogia para explicar como as permissões de arquivo são representadas e qual o acesso que cada símbolo representa.
=======
>###### Em uma pequena cidade chamada Linuxville, vive o Lucas, um entusiasta de tecnologia. Ele está ajudando seu amigo Rafael a entender o funcionamento das permissões de arquivo no sistema Linux. Lucas decide contar uma história, explicando que os arquivos em Linux são como valiosos tesouros guardados em cofres. Cada cofre possui uma combinação única de permissões, representadas por símbolos especiais. Lucas usa essa analogia para explicar como as permissões de arquivo são representadas e qual o acesso que cada símbolo representa..
>>>>>>> 4c47e30 (FEAT: Adicionando Problema 02 do Projeto)
=======
>###### Em uma pequena cidade chamada Linuxville, vive o Lucas, um entusiasta de tecnologia. Ele está ajudando seu amigo Rafael a entender o funcionamento das permissões de arquivo no sistema Linux. Lucas decide contar uma história, explicando que os arquivos em Linux são como valiosos tesouros guardados em cofres. Cada cofre possui uma combinação única de permissões, representadas por símbolos especiais. Lucas usa essa analogia para explicar como as permissões de arquivo são representadas e qual o acesso que cada símbolo representa.
>>>>>>> 72e4fa6 (FEAT: Adicionando Problema 03 do Projeto)
>
>###### **Crie uma Pasta qualquer e 5 arquivos de texto. Em seguida define as permissões 400 para a pasta e todos os arquivos recursivamente. Use esse exemplo para explicar o que são as permissões de arquivo no Linux e como elas são representadas de forma mais detalhada possível.**

###### **Resolução:**

Para começar, vamos criar um diretório. Para isso, basta utilizar o comando:
<<<<<<< HEAD
=======

```bash
mkdir arquivos_problema_002
```
Agora acessamos o diretório onde vamos armazenar os arquivos utilizando:

```bash
cd arquivos_problema_002
```

Para criar os arquivos, usamos:

```bash
touch nome_do_arquivo.extensao
```

Podemos verificar o conteúdo atual do diretório utilizando o comando `ls-la`. Esse comando também traz a definição das permissões para cada um destes arquivos:

![file_permissions_001](https://i.imgur.com/YSRgGYh.png)

Observando as permissões para os arquivos criados, observa-se o padrão `-rw-rw-r--`
em que:
1. o primeiro caractere representa se o item é `d` (um diretório) ou `-` (um arquivo).

1. Os caracteres de 2 a 10 são agrupados em grupos de 3 caracteres, em que r (read) é a permissão de leitura, w (write) é a permissão de escrita e x (execute) é a permissão de execução do arquivo. Esta forma de relacionar permissões é chamada de __modo simbólico__.

1. Os caracteres de posições 2 a 4 representam permissões para o dono (owner) do arquivo;

1. Os caracteres de posições 5 a 7 representam permisões para o grupo ao qual o arquivo pertence;

1. Os caracteres de posições 8 a 10 representam permissões para os outros usuários e grupos;

Quando o sistema analisa as permissões de um arquivo para determinar quais informações fornecer quando você interage com um arquivo, ele executa uma série de verificações:

1. Ele primeiro verifica se o usuário atual é o usuário proprietário (u - owner user) do arquivo. Nesse caso, o usuário atual recebe as permissões do proprietário do usuário e nenhuma verificação adicional é realizada, sendo atribuídas as permissões dos caracteres 2 a 4;
1. Se o usuário atual não for o usuário proprietário do arquivo, é feita a validação de associação ao grupo do proprietário (g - owner group), para verificar se o seu usuário pertence ao grupo que é proprietário do arquivo. Nesse caso, seu usuário estará coberto pelo campo de permissões do proprietário do grupo, sendo atribuídas as permissões dos caracteres 5 a 7;

1. As permissões de "Outros" (o - others) são aplicadas quando o usuário que interage com o arquivo não é nem o proprietário e nem faz parte do grupo que é proprietário do arquivo. Nesse caso, seu usuário é considerado do tipo "Outros", sendo atribuídas as permissões dos caracteres 8 a 10;

1. Os três conjuntos de caracteres são mutuamente exclusivos: Você não pode ser coberto por mais de um deles nas configurações de permissão em um arquivo.

Assim sendo, a o padrão `-rw-rw-r--`, significa que:

1. Para o usuário proprietário, há a permissão de leitura (r) e escrita (w), mas não de execução (x);

1. Para o grupo do usuário proprietário, há a permissão de leitura (r) e escrita (w), mas não de execução (x);

1. Para outros quaiquer usuários, há somente a permissão de leitura (r);

Antes de continuar para definição da mudança de permissões, é importante apresentar o __modo octal__. Este modo funciona de forma semelhante ao modo simbólico, mas atribui permissões através de números, da seguinte forma:

1. 4 confere a permissão de *read* (r);
1. 2 confere a permissão de *write* (w);
1. 1 confere a permissão de *execute* (x);
1. Para conferir mais de uma permissão das listadas acima, basta somar os números. Por exemplo, 6 confere permissão de *read* e *write*, enquanto que 3 confere permissão de *write* e *execute*.

No modo octal, as permissões atuais corresponderiam a:
1. Para o usuário proprietário (u): *read* e *write*: 4+2 = 6;
1. Para o grupo do proprietário (g): *read* e *write*: 4+2 = 6;
1. Para usuários do tipo "outros" (o):  *read*: 4;

Assim, as permissões `-rw-rw-r--` no modo simbólico correspondem a permissões 664 no modo octal.

Uma vez entendidos estes conceitos, vamos ao objetivo que é atribuir permissões 400, isto é:
1. Para o usuário proprietário (u): Permitir somente leitura (4);
1. Para o grupo do proprietário (g): Sem nenhuma permissão (0);

1. Para usuários do tipo "outros" (o): Sem nenhuma permissão (0);

Conforme solicitado, para atribuir essa permissão aos arquivos de forma recursiva (isto é, atribuir permissões para arquivos dentro de uma pasta através de atribuição recursiva para a própria pasta), pode-se utilizar o comando 

```bash
chmod -R 400 arquivos_problema_002
```

Para ter permissão para essa operação, há que se ter um usuário administrador ou um usuário com permissões de escrita para o referido diretório. Para exercitar o uso do root, fez-se o login no usuário root para execução dessa operação.

A partir do comando `ls -la`, pode-se consultar as novas permissões do arquivo em formato simbólico, que ficaram sendo `-r--------`, como pode-se ver na imagem a seguir:

<<<<<<< HEAD
![file_permissions_001](https://i.imgur.com/5KdeEbH.png)
>>>>>>> 4c47e30 (FEAT: Adicionando Problema 02 do Projeto)

```bash
mkdir arquivos_problema_002
```
Agora acessamos o diretório onde vamos armazenar os arquivos utilizando:

```bash
cd arquivos_problema_002
```

Para criar os arquivos, usamos:

```bash
touch nome_do_arquivo.extensao
```

Podemos verificar o conteúdo atual do diretório utilizando o comando `ls-la`. Esse comando também traz a definição das permissões para cada um destes arquivos:

![file_permissions_001](https://i.imgur.com/YSRgGYh.png)

Observando as permissões para os arquivos criados, observa-se o padrão `-rw-rw-r--`
em que:
1. o primeiro caractere representa se o item é `d` (um diretório) ou `-` (um arquivo).

1. Os caracteres de 2 a 10 são agrupados em grupos de 3 caracteres, em que r (read) é a permissão de leitura, w (write) é a permissão de escrita e x (execute) é a permissão de execução do arquivo. Esta forma de relacionar permissões é chamada de __modo simbólico__.

1. Os caracteres de posições 2 a 4 representam permissões para o dono (owner) do arquivo;

1. Os caracteres de posições 5 a 7 representam permisões para o grupo ao qual o arquivo pertence;

1. Os caracteres de posições 8 a 10 representam permissões para os outros usuários e grupos;

Quando o sistema analisa as permissões de um arquivo para determinar quais informações fornecer quando você interage com um arquivo, ele executa uma série de verificações:

1. Ele primeiro verifica se o usuário atual é o usuário proprietário (u - owner user) do arquivo. Nesse caso, o usuário atual recebe as permissões do proprietário do usuário e nenhuma verificação adicional é realizada, sendo atribuídas as permissões dos caracteres 2 a 4;
1. Se o usuário atual não for o usuário proprietário do arquivo, é feita a validação de associação ao grupo do proprietário (g - owner group), para verificar se o seu usuário pertence ao grupo que é proprietário do arquivo. Nesse caso, seu usuário estará coberto pelo campo de permissões do proprietário do grupo, sendo atribuídas as permissões dos caracteres 5 a 7;

1. As permissões de "Outros" (o - others) são aplicadas quando o usuário que interage com o arquivo não é nem o proprietário e nem faz parte do grupo que é proprietário do arquivo. Nesse caso, seu usuário é considerado do tipo "Outros", sendo atribuídas as permissões dos caracteres 8 a 10;

1. Os três conjuntos de caracteres são mutuamente exclusivos: Você não pode ser coberto por mais de um deles nas configurações de permissão em um arquivo.

Assim sendo, a o padrão `-rw-rw-r--`, significa que:

1. Para o usuário proprietário, há a permissão de leitura (r) e escrita (w), mas não de execução (x);

1. Para o grupo do usuário proprietário, há a permissão de leitura (r) e escrita (w), mas não de execução (x);

1. Para outros quaiquer usuários, há somente a permissão de leitura (r);

Antes de continuar para definição da mudança de permissões, é importante apresentar o __modo octal__. Este modo funciona de forma semelhante ao modo simbólico, mas atribui permissões através de números, da seguinte forma:

1. 4 confere a permissão de *read* (r);
1. 2 confere a permissão de *write* (w);
1. 1 confere a permissão de *execute* (x);
1. Para conferir mais de uma permissão das listadas acima, basta somar os números. Por exemplo, 6 confere permissão de *read* e *write*, enquanto que 3 confere permissão de *write* e *execute*.

No modo octal, as permissões atuais corresponderiam a:
1. Para o usuário proprietário (u): *read* e *write*: 4+2 = 6;
1. Para o grupo do proprietário (g): *read* e *write*: 4+2 = 6;
1. Para usuários do tipo "outros" (o):  *read*: 4;

Assim, as permissões `-rw-rw-r--` no modo simbólico correspondem a permissões 664 no modo octal.

Uma vez entendidos estes conceitos, vamos ao objetivo que é atribuir permissões 400, isto é:
1. Para o usuário proprietário (u): Permitir somente leitura (4);
1. Para o grupo do proprietário (g): Sem nenhuma permissão (0);

1. Para usuários do tipo "outros" (o): Sem nenhuma permissão (0);

Conforme solicitado, para atribuir essa permissão aos arquivos de forma recursiva (isto é, atribuir permissões para arquivos dentro de uma pasta através de atribuição recursiva para a própria pasta), pode-se utilizar o comando 

```bash
chmod -R 400 arquivos_problema_002
```

Para ter permissão para essa operação, há que se ter um usuário administrador ou um usuário com permissões de escrita para o referido diretório. Para exercitar o uso do root, fez-se o login no usuário root para execução dessa operação.

A partir do comando `ls -la`, pode-se consultar as novas permissões do arquivo em formato simbólico, que ficaram sendo `-r--------`, como pode-se ver na imagem a seguir:

![file_permissions_002](https://i.imgur.com/5KdeEbH.png)

>### Problema 03
>
>###### Em uma cidade futurística chamada Adalandia, existe uma equipe de jovens DevOps liderada pela Andreza. Eles estão trabalhando em um novo projeto e precisam configurar um servidor web para hospedar sua aplicação. Andreza, como líder do time, guia seus colegas pelo processo de instalação e configuração do servidor Apache, compartilhando suas experiências passadas com a ferramenta e fornecendo orientações detalhadas para garantir uma configuração correta.
>
>###### **Descreva o processo para instalar e configurar o servidor Web Apache no Linux. O Objetivo é alterar a página Default do Apache para os seguintes caracteres:**
>```
>ADA + AdaTech + seu_nome = Sucesso! 
>```
>######Apenas esse texto deve ser renderizado na página padrão do servidor. Não esqueça de tirar um print e documentar tudo que foi feito até chegar a esse resultado.

###### **Resolução:**
1. Acesse o terminal;
1. Instale o servidor Apache através do comando: 
    ```bash
    sudo apt-get install apache2
    ```
1. Após a instalação, inicie o serviço do servidor Apache com:
    ```bash
    sudo systemctl start apache2
    ```
1. Uma preocupação importante quando do deploy de serviços Web é garantir que o servidor inicialize automaticamente com o boot da máquina. Para habilitar este recurso, utilize
    ```bash
    sudo systemctl enable apache2
    ```
    Os passos explicados acima podem ser vistos na imagem a seguir:

=======
![file_permissions_002](https://i.imgur.com/5KdeEbH.png)

>### Problema 03
>
>###### Em uma cidade futurística chamada Adalandia, existe uma equipe de jovens DevOps liderada pela Andreza. Eles estão trabalhando em um novo projeto e precisam configurar um servidor web para hospedar sua aplicação. Andreza, como líder do time, guia seus colegas pelo processo de instalação e configuração do servidor Apache, compartilhando suas experiências passadas com a ferramenta e fornecendo orientações detalhadas para garantir uma configuração correta.
>
>###### **Descreva o processo para instalar e configurar o servidor Web Apache no Linux. O Objetivo é alterar a página Default do Apache para os seguintes caracteres:**
>```
>ADA + AdaTech + seu_nome = Sucesso! 
>```
>######Apenas esse texto deve ser renderizado na página padrão do servidor. Não esqueça de tirar um print e documentar tudo que foi feito até chegar a esse resultado.

###### **Resolução:**
1. Acesse o terminal;
1. Instale o servidor Apache através do comando: 
    ```bash
    sudo apt-get install apache2
    ```
1. Após a instalação, inicie o serviço do servidor Apache com:
    ```bash
    sudo systemctl start apache2
    ```
1. Uma preocupação importante quando do deploy de serviços Web é garantir que o servidor inicialize automaticamente com o boot da máquina. Para habilitar este recurso, utilize
    ```bash
    sudo systemctl enable apache2
    ```
    Os passos explicados acima podem ser vistos na imagem a seguir:

>>>>>>> 72e4fa6 (FEAT: Adicionando Problema 03 do Projeto)
    ![apache2_install_001](https://i.imgur.com/4ijNCsl.png)

1. Para acessar o arquivo HTML que foi solicitado que seja alterado, deve-se acessar o caminho `/var/www/html`, através dos comandos a seguir:
    ![apache2_install_002](https://i.imgur.com/iNMiLjG.png)

1. Vamos usar o Vim para editar este arquivo, retornando somente a estrutura solicitada. Após editado o arquivo fica assim:
    ![apache2_install_003](https://i.imgur.com/UZYrerH.png)

1. Após isso, basta reiniciar o servidor com `sudo systemctl restart apache2` e as alterações já irão refletir.
