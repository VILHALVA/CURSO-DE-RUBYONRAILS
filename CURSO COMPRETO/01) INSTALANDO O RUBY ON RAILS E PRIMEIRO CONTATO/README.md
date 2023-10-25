# INSTALANDO O RUBY ON RAILS E PRIMEIRO CONTATO
## INSTALAÇÃO
Para começar a usar o Ruby on Rails, você precisará configurar um ambiente de desenvolvimento. Vou guiá-lo através do processo de instalação do Ruby on Rails e criar um projeto simples para dar os primeiros passos.

**Passo 1: Instalar o Ruby**

1. Verifique se o Ruby já está instalado no seu sistema. No terminal, você pode digitar:

   ```
   ruby -v
   ```

   Isso deve exibir a versão do Ruby. Se o Ruby não estiver instalado, você pode seguir as instruções no site oficial (https://www.ruby-lang.org/en/documentation/installation/) para instalar o Ruby na sua plataforma.

**Passo 2: Instalar o Rails**

1. Com o Ruby instalado, você pode instalar o Ruby on Rails usando o seguinte comando:

   ```
   gem install rails
   ```

   Isso instalará a versão mais recente do Ruby on Rails.

2. Verifique a instalação do Rails com:

   ```
   rails -v
   ```

   Isso deve exibir a versão do Ruby on Rails.

**Passo 3: Criar um Novo Projeto Rails**

Agora que o Ruby on Rails está instalado, vamos criar um novo projeto simples. Abra o terminal e siga estas etapas:

1. Navegue até a pasta onde você deseja criar o projeto. Por exemplo:

   ```
   cd ~/Documentos
   ```

2. Crie um novo projeto Rails. Substitua "myapp" pelo nome que você deseja dar ao seu projeto:

   ```
   rails new myapp
   ```

   Isso criará uma estrutura de projeto com arquivos e pastas iniciais.

3. Navegue até a pasta do projeto:

   ```
   cd myapp
   ```

**Passo 4: Iniciar o Servidor**

Agora, você pode iniciar o servidor de desenvolvimento embutido para seu projeto:

```
rails server
```

Isso iniciará o servidor na porta padrão 3000. Você pode acessar o aplicativo em seu navegador visitando `http://localhost:3000`.

**Passo 5: Visualize a Página Inicial Padrão**

Abra seu navegador da web e acesse `http://localhost:3000`. Você verá a página inicial padrão do Rails, indicando que sua instalação e projeto estão funcionando.

Agora, você está pronto para começar a desenvolver aplicativos web com Ruby on Rails. Este é apenas o primeiro passo, e há muito mais a aprender, como criar modelos, controladores, visualizações e configurar o banco de dados. Conforme você avança no curso, você aprenderá a criar aplicativos web mais complexos. 

## ESTRUTURA DAS PASTAS:
A estrutura de pastas de um projeto Ruby on Rails segue as convenções da estrutura MVC (Model-View-Controller) e é projetada para tornar o desenvolvimento organizado e eficiente. Aqui está uma visão geral das pastas e os primeiros códigos que você pode encontrar em um projeto Rails:

1. **app:** Esta é a pasta onde você passará a maior parte do tempo desenvolvendo seu aplicativo. Ela contém subpastas para modelos, controladores e visualizações. Aqui estão algumas das pastas importantes dentro de `app`:

   - **models:** Esta pasta contém os modelos que representam as tabelas do banco de dados. Cada modelo é um arquivo Ruby que define a estrutura da tabela e as relações entre os modelos.

   - **controllers:** Os controladores são responsáveis por lidar com solicitações HTTP. Eles definem a lógica de negócios e interagem com os modelos. Você pode criar controladores personalizados aqui.

   - **views:** As visualizações são as páginas da web que são renderizadas e enviadas para o navegador. Elas normalmente usam HTML com código Ruby incorporado (ERB) para exibir dados dinâmicos.

2. **config:** Esta pasta contém configurações para o seu aplicativo. Algumas pastas e arquivos notáveis incluem:

   - **database.yml:** Este arquivo contém as configurações do banco de dados para seu aplicativo.

   - **routes.rb:** Aqui é onde você define as rotas para mapear URLs para ações em controladores.

3. **db:** Essa pasta é onde você pode criar e executar migrações de banco de dados para definir a estrutura do banco de dados.

4. **public:** A pasta `public` contém ativos estáticos, como imagens, folhas de estilo e scripts JavaScript.

5. **Gemfile:** Este arquivo lista as gemas (bibliotecas) que seu aplicativo depende. Você pode adicionar gemas adicionais ao projeto aqui.

6. **Rakefile:** O Rakefile é usado para definir tarefas personalizadas que você pode executar com o utilitário Rake.

## EXEMPLO:
Aqui está um exemplo simples de código para criar um modelo, controlador e visualização:

**1. Modelo:**

Suponha que você esteja criando um aplicativo de blog. Você pode criar um modelo para postagens assim:

```bash
rails generate model Post title:string content:text
```

Este comando cria um arquivo `post.rb` na pasta `app/models` e uma migração na pasta `db/migrate`. A migração é usada para criar a tabela de banco de dados para as postagens.

**2. Migração:**

Você pode executar a migração para criar a tabela no banco de dados com o seguinte comando:

```bash
rake db:migrate
```

**3. Controlador:**

Em seguida, você pode criar um controlador para lidar com as ações relacionadas às postagens:

```bash
rails generate controller Posts
```

Isso cria um arquivo `posts_controller.rb` na pasta `app/controllers`.

**4. Visualização:**

Agora, você pode criar uma visualização para exibir as postagens. Em `app/views/posts`, você pode criar um arquivo `index.html.erb` com o seguinte código:

```html
<h1>Minhas Postagens</h1>
<% @posts.each do |post| %>
  <h2><%= post.title %></h2>
  <p><%= post.content %></p>
<% end %>
```

Este é um exemplo básico de como criar uma estrutura de modelo, controlador e visualização em Ruby on Rails. Lembre-se de que a estrutura e o código podem variar dependendo das necessidades do seu aplicativo.