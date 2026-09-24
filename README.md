# Lab-4-AWS-SimuLearn-Montando-Um-Banco-de-Dados-NoSQL-com-Amazon-DynamoDB-
Hands-on AWS Skill Builder focado em Amazon DynamoDB, modelagem NoSQL, Partition Key, Sort Key e consultas de dados.

<p align="center">
  <img src="./Etapa%201.png" width="500" />
</p>



## Visão Geral

Aqui o foco foi sair um pouco da infraestrutura e entrar em outra parte importante da Cloud: **dados**.
A proposta foi trabalhar com o Amazon DynamoDB, um banco de dados NoSQL totalmente gerenciado da AWS, 

Criando uma tabela, 
Estruturando os itens, 
Inserindo dados e 
Realizando consultas.

O objetivo para mim foi entender como pensar a estrutura de um banco NoSQL e como o DynamoDB organiza e consulta essas informações. 

Plataformas digitais precisam registrar cada detalhe do consumo dos usuários (qual vídeo foi assistido, o momento exato em que parou, preferências de idiomas e os tipos de dispositivos suportados). O grande desafio técnico é fazer isso mantendo alta escalabilidade e performance.


## O problema

Imagine uma plataforma de vídeo que precisa armazenar o histórico de reprodução de seus usuários.
Cada usuário pode assistir a vários vídeos e, para cada reprodução, podemos ter informações como:

* ID do usuário;
* ID do vídeo;
* Data e hora da última reprodução;
* Idioma preferido;
* Dispositivos suportados;
* Avaliação do conteúdo;
* Outras informações relacionadas à experiência daquele usuário.

O desafio é conseguir armazenar e consultar esse histórico de forma rápida e escalável.
É nesse cenário que entra o Amazon DynamoDB.

Em vez de pensar primeiro em tabelas e relacionamentos como fazemos em um banco relacional, no DynamoDB precisamos pensar principalmente em:
Como os dados serão acessados?

Essa foi uma das partes mais importantes que comecei a perceber durante o laboratório.

<p align="center">
  <img src="./Etapa%202.png" width="600" />
</p>


## O desafio do laboratório

O objetivo foi construir uma tabela NoSQL para armazenar o histórico de vídeos assistidos pelos usuários.

Durante o laboratório, precisei:

Entender o funcionamento de um banco NoSQL.
Criar uma tabela no Amazon DynamoDB.
Definir a chave de partição.
Definir a chave de classificação.
Inserir itens na tabela.
Trabalhar com diferentes tipos de atributos.
Realizar consultas utilizando a chave de classificação.
Criar manualmente um novo registro como parte do desafio prático.
Adicionar um atributo numérico de avaliação (rating).
Validar o resultado final do laboratório.


## O que eu precisei entender, compreender e fazer.

Primeiro fui entender como funciona um **Banco NoSQL**.

Durante o laboratório, comecei entendendo que o DynamoDB trabalha de uma forma diferente de um banco de dados relacional. Em vez de pensar primeiro em tabelas e relacionamentos, precisei pensar em como os dados seriam armazenados e principalmente como seriam consultados.

Na prática, aprendi que cada registro é um item e que os dados desse item são organizados por atributos. Também entendi o papel da Partition Key (userId), que identifica e organiza os dados de um usuário, e da Sort Key (lastDateWatched), que permite organizar os registros dentro dessa mesma chave.

Foi fazendo a criação da tabela, inserindo os itens e realizando as consultas que esse conceito começou a fazer sentido para mim. 
Ou seja, não fiquei apenas na teoria: **criei, inseri, consultei e validei os dados no DynamoDB**.


## A tabela utilizada no laboratório foi:

Um dos pontos que mais chamou minha atenção foi perceber que um item do DynamoDB não precisa seguir uma estrutura rígida como uma tabela relacional tradicional.

No laboratório, trabalhei com atributos como:

* userId
* Sort Key
* lastDateWatched
* videoId
* preferredLanguage
* supportedDeviceTypes

e, no desafio prático:
* rating

Também trabalhei com diferentes tipos de dados, incluindo String, Number e List.
Isso ajudou a tornar mais concreto o conceito de estrutura flexível do NoSQL.

Esse ponto foi especialmente importante para entender uma diferença fundamental entre bancos relacionais e NoSQL:
No DynamoDB, a forma como os dados são modelados está diretamente relacionada à forma como eles serão consultados.


## Serviços e tecnologias utilizados
* Amazon DynamoDB
* Banco de dados NoSQL totalmente gerenciado da AWS.

Neste laboratório utilizei o DynamoDB para:

* Criar a tabela;
* Definir as chaves;
* Inserir itens;
* Armazenar diferentes tipos de atributos;
* Consultar os registros;
* Testar filtros utilizando a chave de classificação.

## AWS Skill Builder / SimuLearn
* Ambiente utilizado para realizar o laboratório prático e validar as atividades propostas.


## Partition Key e Sort Key
**Partition Key — userId**

A userId identifica o usuário ao qual aquele registro pertence.
É a chave utilizada para determinar a partição lógica onde os dados serão armazenados.

## Sort Key — lastDateWatched
A lastDateWatched permite organizar os registros dentro da mesma chave de partição.

Assim, podemos pensar no modelo desta maneira:

userId
   │
   ├── lastDateWatched
   │       └── videoId
   │
   ├── lastDateWatched
   │       └── videoId
   │
   └── lastDateWatched
           └── videoId

Ou seja: **um usuário → vários registros de histórico → organizados pela data**.


## Resolvendo o problema

Depois de criar a tabela e inserir os registros, o próximo passo foi entender como consultar essas informações.
Utilizei uma operação de Query, trabalhando com a chave de partição e condições sobre a chave de classificação.

Um dos exercícios utilizou uma condição de comparação do tipo:
**Greater than (>)**. Isso permitiu buscar registros posteriores a determinado valor da chave de classificação.

Na prática, comecei a perceber uma coisa importante:

Não basta armazenar os dados; é preciso modelá-los pensando nas consultas que a aplicação precisará realizar.
Essa foi uma das principais lições deste laboratório.


<p align="center">
  <img src="./Etapa%203.png" width="600" />
</p>


## Mão na massa

Durante o laboratório, passei por algumas etapas principais.

1- Criação da tabela

Criei a tabela: UserVideoHistory
e defini: userId como Partition Key;
lastDateWatched como Sort Key.

2- Inserção dos dados

Depois da criação da tabela, inseri os registros disponibilizados pelo laboratório.
Os itens continham informações relacionadas ao histórico de reprodução dos usuários.

Entre os atributos trabalhados estavam:

* videoId;
* preferredLanguage;
* supportedDeviceTypes;
* lastDateWatched.

3- Trabalhando com diferentes tipos de dados

Uma parte interessante foi perceber que os atributos podem representar diferentes tipos de informação. Por exemplo:

* videoId → String
* rating → Number
* supportedDeviceTypes → List

Isso ajudou a visualizar na prática como o DynamoDB trabalha com os tipos de dados disponíveis.

4- Consultando os registros

Com a tabela preenchida, realizei consultas utilizando a operação Query.
O objetivo foi recuperar registros de um determinado usuário e aplicar uma condição sobre a Sort Key.

Foi aqui que a relação entre: Partition Key + Sort Key + Query
ficou muito mais clara para mim.

## Desafio prático — DIY

Depois das etapas guiadas, veio uma parte que gostei bastante do laboratório: o desafio prático.
Precisava criar manualmente um novo item utilizando um identificador de usuário próprio e adicionar um atributo numérico: **rating**

Essa etapa foi importante porque deixou de ser apenas: “faça exatamente isso”.

Passei a precisar aplicar o que tinha acabado de aprender.
Criei o registro, inseri os atributos solicitados, preenchi o formulário de validação e conferi se o resultado atendia aos requisitos do laboratório.

## Validação

Depois de concluir as etapas, realizei a validação do desafio no ambiente do SimuLearn.
O laboratório foi concluído com sucesso.
Essa etapa foi importante para confirmar que não apenas criei a tabela, mas também executei corretamente as operações solicitadas.

<p align="center">
  <img src="./Etapa%204.png" width="600" />
</p>



## O que eu aprendi

Este laboratório me ajudou a entender o DynamoDB de uma forma muito mais prática.
Alguns conceitos ficaram especialmente claros:

* NoSQL não significa simplesmente "sem estrutura". Existe estrutura.
A diferença é que o modelo é pensado de outra maneira e pode ser mais flexível em relação aos atributos dos itens.

* A modelagem começa pelas consultas
No DynamoDB, precisamos pensar: “Como vou consultar esses dados?”. antes de simplesmente criar uma estrutura.

* Partition Key é fundamental . A escolha da Partition Key influencia diretamente a forma como os dados serão distribuídos e acessados.

* Sort Key permite organizar e consultar dentro da mesma partição
No laboratório, isso fez bastante sentido ao trabalhar com o histórico de reprodução por usuário e data.

* DynamoDB é um serviço gerenciado. Não precisei administrar servidores de banco de dados.

A AWS cuida da infraestrutura necessária para o serviço, permitindo que o foco fique na aplicação e nos dados.


## Um ponto que quero levar para os próximos labs

Uma coisa que ficou muito clara para mim é que não devo pensar no DynamoDB como se fosse simplesmente um banco relacional com outro nome.

A lógica é diferente. No modelo relacional, muitas vezes começamos pensando em:
tabelas → relacionamentos → normalização → consultas

No DynamoDB, precisamos dar muito mais atenção a:
padrões de acesso → chaves → distribuição → performance

Essa mudança de pensamento é uma parte importante do meu aprendizado em Cloud.

## O que este laboratório acrescenta à minha jornada Cloud

Até aqui, meus estudos vinham passando por vários componentes da AWS relacionados à infraestrutura, computação, rede e armazenamento.
Neste laboratório, entrei mais diretamente na parte de dados.
E isso é importante para a minha formação em Cloud porque uma aplicação na nuvem não é apenas: servidor + rede.

Também temos: computação + rede + armazenamento + banco de dados + segurança + monitoramento + custos.

O DynamoDB foi mais uma peça desse quebra-cabeça.

## Evidências do laboratório

Abaixo estão alguns registros das etapas realizadas durante o laboratório:

* Criação e configuração da tabela
* Estrutura e itens da tabela
* Consulta dos registros
* Desafio prático — DIY
* Validação do laboratório

## Principais conceitos praticados
Amazon DynamoDB
        │
        ├── NoSQL
        ├── Partition Key
        ├── Sort Key
        ├── Items
        ├── Attributes
        ├── String
        ├── Number
        ├── List
        ├── Query
        └── Modelagem orientada a padrões de acesso

## Resultado

Mais um laboratório concluído na minha jornada prática com AWS.
Neste Lab 4, meu principal objetivo não foi apenas aprender a clicar e criar uma tabela.
Foi começar a entender como pensar dados dentro da AWS.
A prática com o DynamoDB me mostrou que aprender Cloud também significa entender o que acontece com os dados que as aplicações precisam armazenar, consultar e escalar.

Estudar → praticar → entender → documentar.
É assim que estou construindo minha jornada em Cloud.

## Sobre a autora

Sou Eliana Diniz, profissional em transição de carreira para a área de Cloud Computing.
Minha jornada combina minha experiência anterior com Análise de Dados e meu atual direcionamento para AWS e Cloud Engineering.

Neste momento, estou construindo minha base em Cloud por meio de estudos, certificações e principalmente laboratórios práticos, documentando aquilo que realmente executo. Meu objetivo é transformar conhecimento teórico em experiência prática e continuar avançando na direção de Cloud Engineer.

* LinkedIn: linkedin.com/in/eliana-diniz
* GitHub: github.com/Dinizasilva
* E-mail: eliana.dinizsilva@gmail.com


## Sobre a Trilha AWS Skill Builder
Lab 4 — AWS SimuLearn: Montando um Banco de Dados NoSQL

* Prática realizada. Conhecimento construído. Próximo laboratório.

