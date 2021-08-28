# O que é Git-Flow

O Git-Flow é um *workflow* criado em 2010 por Vincent Driessen. Ele auxilia tanto no *Continuous Integration*(*CI*) quanto no *Continuous Delivery*(*CD*) ou no *Continuous Deployment*(*CD*)  do *software* por meio de um modelo que atribui funções bem específicas para diferentes *branchs* e define quando elas devem interagir.

## Como funciona

O Git-Flow é apenas uma ideia abstrata do fluxo de trabalho Git, ou seja, ele dita que tipos de *branch* configurar e como fazer o *merge*. A seguir serão listadas as *branchs* básicas — *main* e *develop* — as *branchs* de suporte — *feature*, *release*, *hotfix*, *bugfix* e *support* — e seus respectivos objetivos. 

### *main*

Contém todo código já testado e versionado que será colocado em ambientes de homologação ou produção. É conveniente marcar todos os *commits* na ramificação *main* com uma *tag*  que indique o número de versão do projeto.

### *develop*

É utilizada para integração dos recursos desenvolvidos. Ela é uma ramificação da *main* que é feita logo no início do projeto.

### *feature*

*Branchs* ramificadas da *develop* e utilizadas para desenvolver — o Git-Flow exige que cada nova funcionalidade esteja contido em uma *branch* e seja desenvolvido nela. Por conta disso, é comum um repositório possuir várias *branchs* do tipo *feature*. 

Para identificar cada uma das *features*, atribui-se o nome da funcionalidade que será desenvolvida no nome da *branch*.  Por exemplo, a *branch* `feature/login`, foi criada para desenvolver a funcionalidade de *login*. Assim, apesar de existir várias *branchs* de *feature*, só existe uma utilizada para desenvolver a funcionalidade *login*, indicada no nome.

Quando a funcionalidade está pronta, o desenvolvedor pode fazer o *merge* da sua *feature* na *develop*. As *features* não devem nunca interagir direto com a ramificação *main*.

### *release*

Uma vez que a *develop* adquiriu recursos suficientes para um lançamento, é feita uma ramificação dela para criar a *branch* do tipo *release*. Após sua criação, nenhuma nova funcionalidade deve ser desenvolvida, só é permitido fazer atualizações de segurança, geração de documentação e outras tarefas relacionadas ao lançamento.

Quando estiver pronta para ser lançada, é feito dois *merges* da *release*. O primeiro, é feito para a *develop*. Dessa forma, as futuras *features* criadas poderão dispor do que foi feito na *release*. Já o segundo, é feito para a *main*. Essa ação significa que o código  está apto para ser colocado em ambientes de homologação ou até mesmo de produção.

Ao trabalhar com a *branch* *release* é comum adicionar ao seu nome o numero da versão do projeto — por exemplo `release/1.0`. Outra boa prática é, após fazer o *merge* da *release* na *main*, criar uma *tag* que indique o número de versão do projeto.

### *hotfix*

Trata-se de uma ramificação da *main* utilizada para corrigir com rapidez *bugs* do ambiente de produção. Essa é a única *branch* que deve ser bifurcada diretamente da *main* a qualquer momento.

Assim que a correção é feita, deve-se fazer dois *merges* da *hotfix*. O primeiro, é feito para a *develop*. Dessa forma, a correção dos *bugs* estarão disponíveis para as próximas *features* criadas. Já a segunda, é feito para a *main*. Esse *merge* tem o objetivo de lançar a correção do *bug* no ambiente de homologação ou até mesmo de produção.

Ao utilizar uma *branch* *hotfix*é recomendável adicionar ao seu nome alguma referencia que indique o *bug* solucionado — por exemplo `hotfix/cadastro_datas_futuras`. Outra boa prática é, após fazer o *merge* da *hotfix* para a *main*, criar uma *tag* que indique o número de versão do projeto na *main*.

### *bugfix*

As vezes, *bugs* são identificados na *develop* ou na *release*. Nesse caso se cria uma *branch* do tipo *bugfix*. Após finalizar a correção é feito o *merge* da *bugfix* para a *branch* que a originou — seja ela a *develop* ou a  *release*. 

### *support*

*Branchs* do tipo *support* não são abordadas pelo Git-Flow, mas são essenciais quando existe a necessidade de manter várias versões do mesmo projeto. 

É muito importante adicionar ao nome da *suport* o numero da versão do projeto — por exemplo `support/1.0`.







