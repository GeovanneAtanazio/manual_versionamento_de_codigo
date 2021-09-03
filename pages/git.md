# O que é Git?

O Git é um *DVSC* *Open Source* criado em 2005 por Linus Torvalds. Hoje o Git é o *VSC* mais utilizado no mundo. 

## Instalação do Git

O Git está disponível para os três principais sistemas operacionais utilizados em *desktops* e *notebooks* — GNU/Linux, Windows e MacOS. O tutorial de instalação para todos os  sistemas operacionais compatíveis pode ser encontrado na página <https://git-scm.com/downloads>.

## Configurações iniciais

Após instalar o Git, a primeira coisa a ser feita é configurar o nome de usuário — para isso, basta utilizar o comando `git config --global user.name "Fulano de Tal"`, lembre-se de editar o comando com o nome de usuário desejado —  e o endereço de e-mail — para isso, basta utilizar o comando `git config --global user.email fulanodetal@exemplo.br`, lembre-se de editar o comando com o email do usuário desejado. Essas informações são importantes porque ficarão carimbadas de forma imutável nos *commits* criados.

Para conferir se o nome e o e-mail foram configurados corretamente, basta utilizar, respectivamente, os comandos: `console
git config user.name` e `console
git config user.email`.

## Obtendo um repositório

Há duas formas de começar a trabalhar em um projeto com o Git. A primeira, é fazendo um *clone* —  ação de copiar um projeto de algum repositório principal para o computador do desenvolvedor. O comando `git clone`, acompanhado do endereço do repositório principal, é o responsável por efetuar um *clone*. 

 Já a segunda, é transformar um diretório local que não está sob controle de versão em um repositório Git. Para isso, é preciso: 

 1. Entrar no diretório que se deseja versionar;
 2. Executar o comando  `git init` — ele criará um subdiretório chamado `.git` que contém todos os arquivos necessários para a criação do repositório local;
 3. Indicar para o Git que ele pode cuidar de todos os arquivos presentes no diretório com o comando `git add .`— é necessário que o diretório contenha, no mínimo, um arquivo; 
 4. Enviar o arquivo para o repositório local por meio do comando `git commit -m "primeiro commit"` — dentro das aspas é colocada uma mensagem que permite identificar facilmente o *commit*.
 5. Criar a *branch* principal do projeto. Uma *branch* é uma linha cronológica que organiza os *commits* —  todo repositório precisa de no mínimo uma *branch* que é a principal. Por padrão a *branch* principal é chamada de *main*. A criação dela é feita pela execução do comando `git branch -M main`.

Agora é preciso enviar os arquivos guardados no repositório local para um repositório remoto, ou seja, para o repositório principal. Para isso é preciso:

 1.  Criar o repositório principal no servidor remoto;
 2. Sincronizar o repositório local com o remoto com o comando `git remote add origin`, seguido do endereço do repositório principal;
 3. Enviar a *branch* principal, com o *commit* feito anteriormente, para o repositório principal. O comando que faz essa tarefa é o `git push -u origin main`.

Devido a complexidade de começar a trabalhar em um projeto Git pela segunda forma é comum, neste momento, não entender todos os conceitos. Não precisa se preocupar, eles serão revisitados e melhor explicados nas próximas seções. No momento, o mais importante é perceber que é mais simples o desenvolvedor criar o repositório principal no servidor remoto e em seguida cloná-lo para sua máquina.

## Gravações e remoções de alterações nos repositórios

Como explicado na seção "Tipos de *VCS*" um *DVCS* é constituído por  três partes: a área de trabalho, o repositório local e o repositório principal. No Git, os arquivos presentes na área de trabalho podem está em um dos seguintes estados:

 - Não rastreados: Arquivos que não possuem nenhum *snapshots*, ou seja, nunca tiveram algum estado registrados pelo Git ou salvo em um dos repositórios;
 - Rastreados: Arquivos que o Git conhece, ou seja, que tiveram seu último *snapshots* registrado pelo Git ou salvo em algum dos repositórios.
 
 É possível visualizar o estado dos arquivos que estão na área de trabalho utilizando o comando `git status`. 

Para começar a rastrear um novo arquivo, deve-se usar o comando `git add` seguido pelo nome do arquivo que se deseja rastrear. Na seção anterior foi mostrado comando `git add .`, ele faz com que todos os arquivos da área de trabalho sejam rastreados —  o comando `git add *` também tem a mesma finalidade.  

Caso tenha se arrependido de ter adicionado algum arquivo, basta utilizar o comando `git reset` seguido pelo nome do arquivo. Quando o nome não é informado, todos os arquivos adicionados voltarão a ser não rastreados — lembre-se que esse comando não descarta os arquivos ou as informações contidas nele.

O `git add` também serve para selecionar os arquivos que entrarão na área de *stage*, é nela que ficam todos os arquivos que irão constituir um *commit*.  Após selecionar os arquivos, chega o momento de *commitar*, ou seja, enviar os arquivos selecionados para o repositório local. Para isso, basta executar o comando `git commit -m "Nome do commit"` — dentro das aspas é colocada uma mensagem que permite identificar facilmente o *commit*. 

Há momentos em que um *commit* precisa ser desfeito, existem diferentes formas de atingir esse objetivo, veja:

 - Para resetar o repositório local para o último *commit* sem altera os arquivos, apenas o *commit*, o comando utilizado é o `git reset` — para fazer a mesma ação descartando os arquivos o comando é o `git reset --hard`. 
 - Para resetar o repositório local para o *commit* anterior sem altera os arquivos, apenas o *commit*, o comando utilizado é o `git reset HARD~1` — para fazer a mesma ação descartando os arquivos o comando é o `git reset --hard HEAD~1`. 
 - Para resetar o repositório local para um *commit* específico sem descartar as alterações feitas, é preciso utilizar o comando utilizado é o `git reset` com o código identificador do *commit* — para ver o código dos *commits* basta utilizar o comando `git log --oneline`. Para fazer a mesma ação descartando os arquivos o comando é o `git reset --hard` com o código identificador do *commit*.

Outro cenário comum é quando se deseja fazer o *update* da área de trabalho, ou seja, quando já existe algum *commit* do arquivo e o mesmo sofreu alterações que estão somente na área de trabalho, mas há necessidade de descartá-las para ter na área de trabalho o arquivo fidedigno ao último *commit*. Nesses casos, utiliza-se o comando `git checkout` seguido pelo nome do arquivo — caso queira descartar as alterações feitas em todo os arquivos basta utilizar `git checkout *`.

Se não houver problemas  com o *commit* é possível enviá-lo para o repositório principal com o comando `git push` — o Git permite acumular *commits* no repositório local e utilizar o `git push` para submeter todos de uma só vez. 

O processo para desfazer um *commit* que está no repositório principal é semelhante ao utilizado para restaurar um *commit* local descartando os arquivos. O primeiro passo é executar o  comando `git reset --hard` com o código identificador do *commit*. Em seguida, utiliza-se o comando `git push --force` para forçar o *push* que descartará os *commits* posteriores ao indicado no comando.

Para atualizar o repositório local com os arquivos do repositório remoto basta executar o comando `git pull`. Esse comando, no Git, além de fazer o *push*, também faz o *update* da área de trabalho. Por isso, para que ele funcione, é preciso que tanto na área de trabalho quanto no repositório local não exista nenhuma alteração conflitante com o código recebido via *pull* — caso exista, o Git indicará no arquivo os trechos conflitantes para que o desenvolvedor possa escolher qual código deve ser mantido e, em seguida, efetuar o *commit* da versão escolhida.

Mover ou excluir um arquivo rastreado do diretório também  não é uma tarefa complexa. Para mover o comando utilizado é o`git mv` sucedido pelo nome caminho para o arquivo de origem e o caminho para o diretório de destino. Já para excluir o comando utilizado é o`git rm`sucedido pelo nome do arquivo que será descartado.

## Utilizando branchs

Todo repositório tem que ter no mínimo uma *branch*, a principal — por padrão chamada de *main*. *Branch* é uma linha cronológica que organiza os *commits*.

Não inserir *commits* diretamente *main* é uma boa prática adotada mundialmente. Normalmente, os desenvolvedores codificam de forma isolada. Para isso, eles ramificam a *main*, ou seja, cada um bifurca a *branch* principal para que o código desenvolvido seja feito em uma *branch* particular, que não interfere no trabalho feito pelos outros desenvolvedores. 

O comando `git checkout -b` sucedido por um nome, cria uma *branch* com o nome informado no repositório local. Para criá-la no repositório principal, basta executar `git push origin` seguido pelo nome da *branch* criada com o comando anterior.

O Git também permite navegar facilmente entre as *branchs* já criadas. O comando comando `git checkout` acompanhado pelo nome de uma *branch* altera o conteúdo da área de trabalho do desenvolvedor para o conteúdo guardado pela *branch* selecionada.

Seguindo a boa prática, a *main* só recebe *commits* por meio de *merge*. O *merge* ocorre quando o desenvolvedor está seguro que o código feito por ele pode ser mescladas com o código presentes na *main*.

Para efetuar o *merge*, o desenvolvedor deve entrar na *main* e executar o comando `git merge`, seguido pelo nome da *branch* que tem o código que o desenvolvedor deseja trazes para a *main*. Essa lógica pode ser aplicada para fazer o *merge* entre qualquer *branch*.

O comando `git merge` atua apenas no repositório local. Para enviar o *merge* para um repositório  principal é preciso rodar o comando `git push`.

## Criando tags

O Git tem a habilidade de marcar pontos específicos na história como sendo importantes.Existem dois tipos de tag, são elas: 

 - Tag leve: Apenas aponta para um *commit* em especifico. É utilizada para destacar *commits*;
 - Tag anotada: Armazenam detalhes sobre o estado do repositório naquele momento. É utilizada para identificar *releases* — quando um recurso ou conjunto deles se torna disponível para todos ou alguns clientes.

Para criar uma tag leve basta utilizar o comando `git tag -a v1.0` —  lembre-se de editar o comando com o número da versão. Já para criar uma tag anotada, utiliza-se o comando `git tag -a v1.0 -m "primeira release"` —  lembre-se de editar o comando com o número da versão e uma mensagem, respectivamente. Os dois comandos mostrados, criam tags apenas no repositório local. O comando utilizado para enviá-las ao repositório principal  é o `git push origin` seguido pelo nome da tag que  deseja enviar.

Para listar todas as tags do repositório basta utilizar o comando `git tag`. Porém, se o desejo é visualizar informações de um tag, basta utilizar o comando `git tag show` seguido pelo nome da tag que deseja ver as informações.

## Visualizar os *logs*

O Git possui um registro de *logs*. Para visualizar basta utilizar o comando `git log` — se preferir uma visualização mais resumida, utilize o comando `git log --oneline`. 