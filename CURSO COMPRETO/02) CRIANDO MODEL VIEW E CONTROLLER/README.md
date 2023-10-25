# CRIANDO MODEL VIEW E CONTROLLER
Vou guiar você através da criação de um modelo, uma visualização e um controlador em um projeto Ruby on Rails. Neste exemplo, criaremos um aplicativo simples para gerenciar tarefas ("To-Do List").

**Passo 1: Crie um Novo Projeto Rails**

Primeiro, certifique-se de que você esteja na pasta onde deseja criar o projeto. Então, execute o seguinte comando para criar um novo projeto Rails chamado "TodoList":

```bash
rails new TodoList
```

Navegue até a pasta do projeto:

```bash
cd TodoList
```

**Passo 2: Crie um Modelo**

Vamos criar um modelo chamado "Task" que representará nossas tarefas. Execute o seguinte comando para gerar o modelo:

```bash
rails generate model Task title:string description:text completed:boolean
```

Isso cria um arquivo `task.rb` na pasta `app/models` e uma migração na pasta `db/migrate`. A migração define a estrutura da tabela no banco de dados para as tarefas, incluindo os campos `title`, `description` e `completed`.

**Passo 3: Execute a Migração do Banco de Dados**

Agora, execute a migração para criar a tabela no banco de dados:

```bash
rake db:migrate
```

Isso criará a tabela `tasks` no banco de dados.

**Passo 4: Crie um Controlador**

Agora, crie um controlador chamado "Tasks" para lidar com as ações relacionadas às tarefas:

```bash
rails generate controller Tasks
```

Isso cria um arquivo `tasks_controller.rb` na pasta `app/controllers`.

**Passo 5: Defina Rotas**

Abra o arquivo `config/routes.rb` e adicione as rotas para as ações do controlador "Tasks":

```ruby
# config/routes.rb
Rails.application.routes.draw do
  resources :tasks
  root 'tasks#index'
end
```

Isso define rotas RESTful para as ações do controlador "Tasks" e define a página inicial para a lista de tarefas.

**Passo 6: Crie Visualizações**

Agora, crie as visualizações para o controlador "Tasks". Na pasta `app/views/tasks`, você pode criar os seguintes arquivos:

- `index.html.erb`: Para exibir a lista de tarefas.
- `new.html.erb`: Para criar uma nova tarefa.
- `edit.html.erb`: Para editar uma tarefa.

Por exemplo, em `index.html.erb`, você pode exibir a lista de tarefas:

```html
<h1>Lista de Tarefas</h1>
<%= link_to "Nova Tarefa", new_task_path %>

<ul>
  <% @tasks.each do |task| %>
    <li>
      <%= task.title %>
      <%= link_to "Editar", edit_task_path(task) %>
    </li>
  <% end %>
</ul>
```

**Passo 7: Crie o Controlador**

No arquivo `tasks_controller.rb`, adicione a lógica para as ações do controlador, como `index`, `new`, `create`, `edit`, `update` e `destroy`. Você também precisará definir métodos para acessar e modificar as tarefas no banco de dados.

**Passo 8: Inicie o Servidor**

Agora você pode iniciar o servidor Rails com o comando:

```bash
rails server
```

Acesse seu aplicativo em `http://localhost:3000` e você poderá criar, editar e listar tarefas.

Lembre-se de que este é um exemplo simples para ilustrar a criação de um modelo, controlador e visualizações. Em um aplicativo real, você adicionaria autenticação, validações e recursos adicionais conforme necessário.