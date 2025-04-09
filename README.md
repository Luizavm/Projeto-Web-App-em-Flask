# Projeto-Web-App-em-Flask

### **Objetivo**

- Desenvolver um sistema web de lista de tarefas (TODO) utilizando Flask. O sistema deverá armazenar os dados em um arquivo CSV e fornecer uma interface simples para gerenciamento das tarefas.

### **Requisitos Funcionais**

- **Adicionar tarefas** – O usuário poderá criar novas tarefas com um título, descrição e imagem;
- **Remover tarefas** – O usuário poderá excluir tarefas individualmente;
- **Editar tarefas** – O usuário poderá modificar o título, descrição e imagem de uma tarefa existente;
- **Listar tarefas** – Exibir todas as tarefas cadastradas;

### Configurar o ambiente virtual - Flask Web Server

**Criar uma nova pasta**

<aside>
<img src="/icons/photo-landscape_blue.svg" alt="/icons/photo-landscape_blue.svg" width="40px" />

![image.png](attachment:a4afb9d9-17ce-4eac-b690-092169f5b8a3:image.png)

</aside>

**Criar o Venv**

```python
python -m venv venv
```

**Entrar no ambiente virtual**

```python
./venv/Scripts/Activate.ps1
```

**Instalar o Flask**

```python
pip install flask
```

**Criar um arquivo app.py**

<aside>
<img src="/icons/photo-landscape_blue.svg" alt="/icons/photo-landscape_blue.svg" width="40px" />

![image.png](attachment:870f9deb-2464-4829-bad9-36b727fca6be:image.png)

</aside>

**Importar o Flask e o Jinja2**

<aside>
<img src="/icons/photo-landscape_blue.svg" alt="/icons/photo-landscape_blue.svg" width="40px" />

![image.png](attachment:522af2b9-b2a1-46d6-83f6-35868c3ff486:image.png)

</aside>

**Criar pasta - Templates** 

<aside>
<img src="/icons/photo-landscape_blue.svg" alt="/icons/photo-landscape_blue.svg" width="40px" />

![image.png](attachment:8d4d79b5-ed86-4d95-8c8f-f9f1b32eac09:image.png)

</aside>

**Criar a pasta - Static (dividida em CSS, JS e Img)**

<aside>
<img src="/icons/photo-landscape_blue.svg" alt="/icons/photo-landscape_blue.svg" width="40px" />

![image.png](attachment:afbf2401-981a-44d5-a439-925a89a1545d:image.png)

</aside>

**Resultado**

<aside>
<img src="/icons/photo-landscape_blue.svg" alt="/icons/photo-landscape_blue.svg" width="40px" />

![image.png](attachment:0fde26c9-8ae9-4acc-b3ad-e59ac0dcf9d3:image.png)

</aside>

**Biblioteca Werkzeug**

```python
pip install werkzeug
```

- **Werkzeug** é uma biblioteca essencial que funciona **por trás do Flask**. Na verdade, o Flask é construído em cima do Werkzeug — ele usa o Werkzeug para lidar com **requisições HTTP**, **respostas**, **roteamento**, **sessões**, e outras operações de baixo nível da web.
- No app.py utilizamos a função **secure_filename()** serve para **limpar o nome de arquivos enviados por usuários** antes de salvar esses arquivos no servidor.

### Funções app.py

- Este código implementa um **aplicativo web de lista de tarefas** usando o framework **Flask**, que permite que os usuários adicionem, visualizem, editem e excluam tarefas de maneira simples. As tarefas são armazenadas em um **dicionário na memória** durante a execução do app, e também são persistidas em um arquivo ‘**.csv’** chamado ‘**banco_arquivo.csv**' para garantir que os dados não se percam entre reinicializações do servidor.
- Cada tarefa possui um identificador único (ID), um nome, uma descrição e, opcionalmente, uma imagem. Essas informações são mantidas no dicionário ‘**tarefas’**, onde a chave é o ID e o valor é outro dicionário com os dados da tarefa.
- O aplicativo define várias rotas para organizar suas funcionalidades. A rota ‘**/’** exibe a página inicial com uma mensagem de boas-vindas. A rota **/tarefa** mostra a lista de tarefas registradas, enquanto ‘**/add_tarefa_form’** renderiza um formulário para que o usuário possa adicionar uma nova tarefa. Quando esse formulário é submetido, os dados são enviados para a rota ‘**/add_tarefa’**, que processa o nome, a descrição e, se houver, o upload de uma imagem associada à tarefa.
- Se uma imagem for enviada, ela será salva na pasta ‘**static/img/’** do projeto. Para garantir a segurança ao salvar esses arquivos, é usada a função ‘**secure_filename()’** da biblioteca ‘**werkzeug.utils’.** Essa função tem um papel importante: ela **limpa e protege o nome do arquivo**, evitando que usuários mal-intencionados tentem usar nomes com comandos ou caminhos maliciosos (como ‘**../../etc/passwd’** ou **arquivo;.exe**). Assim, ‘**secure_filename()’** garante que o nome final seja seguro para ser salvo no servidor, removendo ou substituindo qualquer caractere indesejado.
- Além de adicionar tarefas, o usuário pode excluí-las por meio da página ‘**/del_tarefa’**, onde as tarefas são listadas com checkboxes. Quando o formulário de exclusão é enviado, a rota ‘**/excluir_tarefas’** processa a exclusão com base nos IDs recebidos e atualiza tanto o dicionário quanto o arquivo CSV.
- Também é possível atualizar tarefas existentes através da rota ‘**/up_tarefa’**, que recebe os novos dados via formulário, atualiza a entrada correspondente no dicionário e salva novamente no arquivo CSV.
- O arquivo pode ser executado diretamente e roda o servidor Flask com ‘**debug=True’**, permitindo visualizar erros e reiniciar automaticamente durante o desenvolvimento.

### Funções banco_arquivo.csv

- O arquivo ‘**banco_arquivo.csv’** atua como uma solução de **persistência de dados baseada em arquivo**, funcionando como um banco de dados rudimentar para o sistema. Trata-se de um arquivo no formato **CSV**, onde os dados são estruturados em colunas separadas por vírgulas, permitindo fácil leitura e escrita por meio da biblioteca ‘**csv’** do Python.
- A primeira linha do arquivo representa o cabeçalho, contendo os nomes dos campos que compõem cada registro: **id, nome, descricao e imagem**. As linhas subsequentes representam as tarefas cadastradas no sistema, onde cada linha corresponde a uma entrada única no dicionário tarefas.

### Pasta templates

No Flask, a pasta ‘**templates’** é um **diretório padrão** onde ficam armazenados os **arquivos HTML** usados para gerar o conteúdo visual do seu site. O Flask utiliza o motor de template **Jinja2**, que permite misturar HTML com código Python (usando ‘**{{ }}’** e ‘**{% %}’)** para criar páginas dinâmicas.

Sempre que usamos ‘render_template("nome_do_arquivo.html"’) no código, o Flask vai procurar esse arquivo **dentro da pasta’ templates’**.

**add_tarefa.html →**

Página que exibe o **formulário para adicionar uma nova tarefa**. Contendo campos como nome, descrição e upload de imagem.

**del_tarefa.html →**

Página onde o usuário pode **selecionar tarefas para excluir**. Deve listar as tarefas existentes com checkboxes para exclusão em massa.

**homepage.html →**

Página inicial do sistema. Exibe uma **mensagem de boas-vindas**, uma introdução ao server.

**index.html →**

Página principal, base estrutural do site. 

**nav.html →**

**Template** contendo o menu de navegação (navbar). 

**tarefa.html →**

Formulário para adicionar novas tarefas, contendo elementos como nome, descrição e imagem das tarefas.

### Pasta static

A pasta ‘**static’** é onde ficam armazenados arquivos estáticos que não mudam dinamicamente no backend, como:

- **CSS (estilização) -** Contém os **arquivos de estilo (CSS)** responsáveis pela aparência visual das páginas.
- **Imagens -** Armazena **imagens estáticas** utilizadas no projeto, exibidas nos templates HTML.
- JavaScript (interatividade) - Contém **scripts JavaScript** que adicionam interatividade às páginas.
