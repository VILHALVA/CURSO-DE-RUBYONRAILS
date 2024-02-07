# SINTAXE
Vou te guiar através dos passos básicos para criar um pequeno projeto em Ruby on Rails. Neste exemplo, vamos criar um aplicativo simples de lista de tarefas (To-Do List).

1. **Instalação do Ruby on Rails:**

Certifique-se de ter o Ruby e o Rails instalados em sua máquina. Você pode verificar se o Ruby está instalado executando `ruby -v` no terminal e o Rails executando `rails -v`. Se não estiverem instalados, você pode seguir as instruções de instalação do [Ruby](https://www.ruby-lang.org/pt/documentation/installation/) e do [Rails](https://guides.rubyonrails.org/getting_started.html#installing-rails).

2. **Criando o Projeto:**

Abra o terminal e navegue até o diretório onde deseja criar o projeto. Em seguida, execute o seguinte comando para criar um novo aplicativo Rails chamado "todo_list":

```bash
rails new todo_list
```

Isso criará uma nova pasta chamada "todo_list" com a estrutura básica de um aplicativo Rails.

3. **Criando o Modelo e o Controlador:**

Agora, precisamos criar um modelo e um controlador para gerenciar as tarefas da lista. No terminal, navegue até o diretório do projeto e execute os seguintes comandos:

```bash
cd todo_list
rails generate model Task title:string completed:boolean
rails generate controller Tasks index create update destroy
```

Isso irá gerar um modelo `Task` com atributos `title` e `completed`, e um controlador `Tasks` com ações `index`, `create`, `update` e `destroy`.

4. **Migrando o Banco de Dados:**

Agora, precisamos migrar o banco de dados para criar a tabela de tarefas. No terminal, execute o seguinte comando:

```bash
rails db:migrate
```

Isso executará todas as migrações pendentes e criará a tabela de tarefas no banco de dados.

5. **Definindo Rotas:**

Abra o arquivo `config/routes.rb` e adicione as seguintes rotas para as ações do controlador:

```ruby
Rails.application.routes.draw do
  resources :tasks, only: [:index, :create, :update, :destroy]
end
```

Isso define rotas RESTful para manipular as tarefas.

6. **Criando as Visualizações:**

Crie as visualizações para listar as tarefas e adicionar novas tarefas. Crie um arquivo `index.html.erb` em `app/views/tasks` com o seguinte conteúdo:

```html
<h1>To-Do List</h1>

<ul id="tasks">
  <% @tasks.each do |task| %>
    <li>
      <%= task.title %>
      <%= link_to 'Delete', task, method: :delete, data: { confirm: 'Are you sure?' } %>
    </li>
  <% end %>
</ul>

<%= form_with(model: Task.new, remote: true) do |form| %>
  <%= form.text_field :title, placeholder: 'New task' %>
  <%= form.submit 'Add Task' %>
<% end %>
```

7. **Configurando Controlador:**

Abra o arquivo `app/controllers/tasks_controller.rb` e defina as ações do controlador:

```ruby
class TasksController < ApplicationController
  before_action :set_task, only: [:update, :destroy]

  def index
    @tasks = Task.all
  end

  def create
    @task = Task.new(task_params)
    if @task.save
      render json: @task
    else
      render json: @task.errors, status: :unprocessable_entity
    end
  end

  def update
    if @task.update(task_params)
      render json: @task
    else
      render json: @task.errors, status: :unprocessable_entity
    end
  end

  def destroy
    @task.destroy
    head :no_content
  end

  private

  def set_task
    @task = Task.find(params[:id])
  end

  def task_params
    params.require(:task).permit(:title, :completed)
  end
end
```

Isso define as ações para manipular as tarefas.

8. **Executando o Servidor:**

Agora, você pode iniciar o servidor Rails executando o seguinte comando:

```bash
rails server
```

Isso iniciará o servidor Rails localmente. Você pode acessar o aplicativo em `http://localhost:3000/tasks`.

Esse é um exemplo básico de como criar um projeto simples em Ruby on Rails para uma lista de tarefas. Você pode expandir esse projeto adicionando mais funcionalidades, como edição de tarefas, marcação de tarefas como concluídas e autenticação de usuários.