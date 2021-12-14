<a href="https://www.linux.org/" target="_blank" rel="noreferrer"> <img src="https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white" alt="linux" width="1000" height="100"/> </a> 

<h2>Projetos Digital Innovation One</h2>

- <h3> Comandos e anotações</h3> 

git init >> Inicia um novo repositório git;

git add Controller.php >> Adiciona um  arquivo a "staging area";

git add . >> Adiciona todos os arquivos do repositório a "staging area";

git commit -m "mensagem" >> Faz um commit;

git commit -am "mensagem" >> Adicionar arquivo a "staging area" e fazer commit ao mesmo tempo;

git commit  --amend >> Alterar último commit;

git commit --amend -m "Mensagem" >> Fazer commit alterando o último.

-------------------------------------------------------------------------------------------

git log >> Mostra histórico de commits;

git log --author >> Filtrar commits por autor;

git log --grep="termo de busca" >> Filtrar commits por palavras chave;

git log --oneline >> Filtrar commits mostrando apenas uma linha para cada um deles;

git log --graph -- oneline --decorate --all >> Log de todas as branchs apontando para o "HEAD".

--------------------------------------------------------------------------------------------

git diff Controller.php >> Compara arquivos de "working directory";

git diff --staged Controller.php >> Compara arquivos do "working directory" com arquivos da "staging area".

--------------------------------------------------------------------------------------------

git rm Controller.php >> Remover arquivos;

git mv Controller.php NovoController.php >> Renomear arquivos;

git mv Controller.php novoController/NovoController.php >> Mover arquivos.

--------------------------------------------------------------------------------------------

git checkout --Controller.php >> Restaura a última versão do arquivo em "working directory"

git reset HEAD Controller.php >> Remover arquivo da "staging area" e enviar para "working directory"

--------------------------------------------------------------------------------------------

git clean -n >> verificar os arquivos que desejamos remover do "working directory"

git clean -f >> forçar remoção de arquivos do "working directory"

--------------------------------------------------------------------------------------------

git checkout 3cb747f --Controller.php >> Recuperar um arquivo específico

--------------------------------------------------------------------------------------------

Desfazendo commits:

git reset --soft  3cb747f

git reset --mixed 3cb747f

git reset --hard 3cb747f

-----------------------------------------------------------------------------------------------

 - <h3> Tutorial de Git e GitHub </h3>
 
<h4> O que é Git? </h4>

Git é um sistema de código aberto e gratuito para controle de versão, criado em 2005 por Linus Torvalds enquanto desenvolvia o Kernel do Linux. Controle de versão é um sistema que permite gravar alterações em arquivos ao longo do tempo, portanto, podemos visualizar versões específicas desses arquivos posteriormente.

Geralmente, acontece de termos muitos desenvolvedores trabalhando numa mesma base de códigos, então um sistema de controle de versão como o Git é necessário para diminuir conflitos entre o código de cada desenvolvedor.

<h4> O que é GitHub? </h4>

Se você vai utilizar Git, é necessário armazenar seu repositório em algum lugar. Existem duas formas de se fazer isso, offline, no seu próprio computador, ou online, em alguma plataforma como GitHub, BitBucket ou GitLab.

É exatamente para isso que o GitHub serve, para armazenar seus repositórios, ele é o “Google Drive dos códigos”.

<h4> Configuração do ambiente </h4>

Primeiramente, é necessário possuir o Git instalado no seu computador e uma conta no GitHub. Você pode baixar o Git no site oficial, basta selecionar o seu sistema operacional e seguir o guia de instalação.

No Linux, recomenda-se instalar o Git via gerenciador de pacotes, nesse caso, você pode ir até essa página e executar no seu terminal o comando específico da sua distribuição.

Depois de instalar o Git, é necessário configurar o seu nome e e-mail que serão exibidos em seus commits, para isso é só digitar no terminal os comandos abaixo:

git config --global user.name "Bruno"
git config --global user.email "bruno.desouzaads@gmail.com"
Observação: Caso você esteja no Windows, não se esqueça de utilizar o git bash, pois ele simula um ambiente Unix, facilitando a forma de se trabalhar com Git.

Agora iremos criar uma chave de SSH, com ela provaremos ao GitHub que nós somos os donos da nossa conta. Caso já tenha uma chave SSH, podemos verificar seu diretório .ssh listando o conteúdo:

<h6>cd ~/.ssh
ls</h6>

Caso o comando ls retorne algo com a extensão .pub, você não precisa executar o comando ssh-keygen. Caso contrário, digite esse comando no seu terminal:
ssh-keygen -t rsa -b 4096 -C "bruno.desouzaads@gmail.com"
O comando acima irá pedir um nome do arquivo para salvar a chave, não escreva nada e aperte enter (será gerada uma com o nome id_rsa). Depois, informe uma senha (passphrase) e confirme ela. Pronto, você gerou uma chave SSH.

Vamos agora adicionar a chave ao ssh-agent, um programa que fará a autenticação da sua máquina local, com o servidor remoto, que nesse caso seria o GitHub, execute então o comando ssh-agent:

<h6>eval $(ssh-agent -s)</h6>
A mensagem Agent pid 1234 será exibida.


Executar o comando ssh-add, onde o id_rsa é o nome da sua chave SSH, informe a passphrase utilizada no comando ssh-keygen:

<h6>ssh-add ~/.ssh/id_rsa</h6>

A mensagem Identity added : id_rsa (bruno.desouzaads@gmail.com) será exibida.

Adicionando a chave SSH à sua conta no GitHub
Primeiramente, você deve criar uma conta no GitHub.

No diretório ~/.ssh existem dois arquivos, id_rsa e id_rsa.pub. O com a extensão .pub é a chave pública, ou seja, a chave que você irá informar ao GitHub. O arquivo sem o .pub é a sua chave privada.

Digite o seguinte comando no terminal para exibir o conteúdo da chave gerada:

</h6>cat ~/.ssh/id_rsa.pub</h6>

Copie todo o conteúdo para a sua área de transferência (lembre-se de copiar desde “ssh-rsa” até o seu e-mail).

Acesse a página de SSH and GPG keys no GitHub para associar a nova chaves SSH a sua conta. Clique então no botão New SSH Key.

O título você pode escolher um (ex: chave bruno.desouzaads@gmail.com), e em Key, você informará o conteúdo que copiou anteriormente.

Clique em Add SSH Key para salvar. Pronto, sua configuração está feita.
![header](https://user-images.githubusercontent.com/88558377/146067047-e59116de-f847-49b7-8567-074cad9a34d9.jpg)

<h4>Fluxo de trabalho 1</h4>
Geralmente, o fluxo de trabalho com Git e GitHub é realizando um fork de um determinado repositório de outra pessoa. Dessa forma, vamos criar uma cópia deste repositório no nosso perfil. Após fazer o clone do fork para a nossa máquina local, podemos realizar alterações, e publicar as alterações feitas em seu repositório fork no GitHub. Por fim, poremos criar um pull request do seu fork para o repositório principal (upstream).

<h4>Fork</h4>
Vamos começar realizando o fork de um repositório base no GitHub. Veja nosso repositório artigo-tutorial-git e clique no botão Fork no canto superior direito. Ao clicar, será feita uma cópia do repositório do Buteco em seu perfil no GitHub.

Agora em seus repositórios você tera uma cópia de artigo-tutorial-git. Lembre-se, você não está no repositório principal, você está no seu, as alterações feitas ali, não terão impacto no principal.

Você deve criar um Pull Request para enviar suas alterações, que é o que iremos ver daqui a pouco.

<h4>Git Clone</h4>
Vamos clonar o repositório para a sua máquina local para que você possa realizar alterações. Na página do seu repositório no GitHub, existe um botão chamado Code, clique nele, selecione a opção SSH, e depois clique no botão de copiar.

![header](https://user-images.githubusercontent.com/88558377/146068183-b8d1bd6f-df6a-42e6-a1a8-2acb522ebd07.jpg)

Agora abra o seu terminal no local que deseja baixar o repositório, e execute (use o endereço que você copiou):

<h6>git clone git@github.com:buteco-tech/artigo-tutorial-git.git</h6>
Será pedido para que você informe a sua passphrase de quando criou a sua chave SSH. Após, o clone do repositório você terá uma nova pasta chamada artigo-tutorial-git.

Entre na nova pasta com o comando:

<h6>cd artigo-tutorial-git</h6>

Você deverá ter algo similar a imagem abaixo:
![2](https://user-images.githubusercontent.com/88558377/146068305-9e19d2fa-1f84-4b2b-9eaf-479a95a17738.jpg)

Perceba que existe ali, uma pasta chamada .git, é nela que o Git guarda todas as informações do seu repositório, todas as alterações, o endereço do repositório remoto e tudo o que é relacionado ao controle de versão.

No Windows talvez você não consiga visualizar esta pasta pois ela é um arquivo oculto, então é só seguir esse tutorial para alterar as configurações.

<h4>Git Status e Git Add</h4>
Vamos criar um novo arquivo para que possamos adicionar ele depois, então, crie um arquivo de texto qualquer dentro do diretório do repositório.

<h6>echo "Tutorial de Git e GitHub" > arquivo.txt</h6>
Voltando para o terminal, digite git status. Você verá essa mensagem:

![header](https://user-images.githubusercontent.com/88558377/146068399-a429bc35-a529-4d46-b0dd-78654d7716b6.jpg)

Untracked files são as alterações pendentes, nós precisamos adicionar elas à área de staging. As alterações que estão no staging são as que serão commitadas futuramente.

Para adicionar apenas um arquivo execute o comando:

<h6>git add nome-do-arquivo</h6>
Ou para adicionar todos os arquivos execute o comando:

<h6>git add .</h6>

O git add não afeta diretamente o repositório, pois ele ainda não “salvou” as alterações, apenas às moveu para a área de staging, quando executamos git commit essas as alterações serão salvas.

Agora sim, podemos confirmar as alterações, para isso execute o comando:

<h6>git commit -m "Meu primeiro commit"</h6>

O -m é para informar uma mensagem que será gravada junto ao commit.

Se você executar o comando git status novamente, o seu terminal deverá estar parecido com o abaixo.

![header](https://user-images.githubusercontent.com/88558377/146068512-ab0bef6b-1bab-486c-b428-dd6feb9a5a64.jpg)

Agora é hora de subir as alterações feitas no seu repositório local para o seu repositório remoto, nesse caso, o do GitHub.

<h4>Git Push</h4>
Quando estamos com alguma alteração commitada localmente e queremos subir elas para o repositório remoto, precisamos publicá-las, para isso execute o comando:

<h6>git push</h6>
Após, visite a página do seu repositório no GitHub. Você percebera que as alterações feitas localmente, já estão lá, mas atenção, quando você fez o push, as alterações foram para o seu fork, não para o repositório principal.

<h4>Criando um Pull request</h4>
No seu repositório, após feito um push, você verá um botão escrito Pull request. Clique nele.

![header](https://user-images.githubusercontent.com/88558377/146068612-3e14b880-f4e7-4666-a9a7-ce8d096073d1.jpg)

Isso irá abrir uma página mostrando os arquivos alterados e um botão Create pull request. Clique nele, informe o título e um comentário para esse pull request e clique no botão Create pull request.

Pronto, seu PR foi criado com sucesso.

Se você for até a página de pull requests do repositório principal, o seu PR estara lá. Agora, para a sua alteração entrar de fato no repositório principal, o se pull request deve ser aceito por algum mantedor do repositório. Esse processo de aceitar um pull request é chamado de merge.

<h4>O que é Pull Request?</h4>
Desde o começo desse artigo, tudo girou em torno deste momento, em que você cria o seu pull request, mas afinal, o que é um pull request?

Para entendermos o que é um pull request precisamos entender o que é um pull. Quando existe alguma alteração no repositório remoto, e você quer baixar essa alteração para o seu repositório local, ou seja, o seu repositório local está atrasado em relação ao remoto, você digita git pull no terminal (olha só, mais um comando novo). Um pull request é uma sugestão de uma alteração, ou seja, você está pedindo para que aquele repositório que você enviou o pull request faça um pull com as suas alterações.

<h4>Fluxo de trabalho 2</h4>
Como dito anteriormente, vamos ver outra maneira de se utilizar o Git e GitHub.

Desta vez, vamos começar com o comando git init para criar o nosso repositório localmente, depois iremos conectar ele ao GitHub e enviar os nossos commits.

<h4>Git Init</h4>
Crie uma pasta em qualquer lugar do seu computador e navegue até ela com o seu terminal. Digite então dentro dela, o comando:

<h6>git init</h6>
Você perceberá que foi criado uma pasta .git, que mapeia as alterações e commits do repositório como mencionado anteriormente.

Realize agora alguma alteração. Crie um arquivo de texto, por exemplo. Depois, execute o comando git add que foi falado anteriormente e git commit -m, agora você já está craque nisso.

![header](https://user-images.githubusercontent.com/88558377/146068686-1dbbd699-53b2-404d-8037-892600d89750.jpg)

Feito isso, é hora de subirmos essas alterações para o repositório remoto (que ainda não foi criado).

Precisamos criar um repositório no GitHub. Nesta página informe algumas informações sobre o repositório, como o nome, descrição, e clique em Create repository.

Pronto, um novo repositório foi criado.

Vinculando o repositório local, ao remoto
Veja que existem ali três opções:

…or create a new repository on the command line

…or push an existing repository from the command line

…or import code from another repository

![header](https://user-images.githubusercontent.com/88558377/146068771-0486ba65-90e3-4882-aeab-40eeb28c6914.jpg)

A primeira opção, é para criar um repositório local, vincular ele ao GitHub, e fazer um push das alterações. A segunda é para apenas conectar um repositório local já existente, e fazer um push dele. E a terceira, é para importar o código de algum repositório que esteja utilizando um sistema de versionamento de código diferente do Git.

Nós já temos o nosso repositório criado, queremos apenas subir ele ao GitHub, portanto, vamos realizar os passos da segunda opção.

Com o seu terminal aberto na pasta do seu repositório local, execute então os seguintes comandos:

<h6>git remote add origin git@github.com:seu-nome/git-init-exemplo.git</h6>
Esse comando define para onde enviaremos nossos commits, nesse caso o GitHub.

<h6>git branch -M main</h6>

Esse comando cria uma branch com o nome main, padrão do GitHub.
1
<h6>git push -u origin main</h6>

Esse comando envia as alterações commitadas ao seu repositório remoto no GitHub.

Pronto, se você for até a página do seu repositório no GitHub as alterações já estarão lá.

O fim, se existe, está muito distante ainda
Se você chegou até aqui, então aprendeu bastante coisa.

Você aprendeu como fazer um fork de um repositório no GitHub, como clonar ele para a sua máquina local com git clone, adicionar as suas alterações a ele com git add, commitar elas com git commit, subir as suas alterações ao repositório remoto com git push e como abrir um pull request com as alterações.

Mas não acabou por aí, o próximo passo é estudar sobre branches, entendendo como elas funcionam e são usadas. E claro, contribuir com software livre.


