# CONHECENDO AS VIEWS E ROTAS
As visualizações (views) e as rotas (routes) são dois componentes-chave no framework Ruby on Rails que desempenham um papel essencial na criação de interfaces de usuário e no roteamento de solicitações HTTP para controladores. Vou explicar cada um deles em detalhes:

**Views (Visualizações):**

1. **O que são Visualizações:**

   As visualizações são os componentes que determinam a aparência da interface do seu aplicativo e exibem os dados processados pelos controladores. As visualizações são geralmente escritas em HTML com a inclusão de código Ruby embutido, que é executado no servidor para gerar conteúdo dinâmico.

2. **Responsabilidades das Visualizações:**

   - Exibir dados de maneira formatada e amigável para o usuário.
   - Incluir lógica de apresentação, como loops e condicionais para gerar conteúdo dinâmico.
   - Interagir com os dados fornecidos pelos controladores.
   - Renderizar formulários para coletar informações do usuário.

3. **Exemplo de Visualização:**

   Aqui está um exemplo simples de uma visualização que exibe uma lista de tarefas:

   ```html
   <h1>Lista de Tarefas</h1>
   <ul>
     <% @tasks.each do |task| %>
       <li><%= task.title %></li>
     <% end %>
   </ul>
   ```

   Neste exemplo, `@tasks` é uma variável de instância fornecida pelo controlador e usada na visualização para exibir uma lista de tarefas.

**Rotas (Routes):**

1. **O que são Rotas:**

   As rotas em Ruby on Rails mapeiam URLs para ações em controladores. Elas determinam como as solicitações HTTP são roteadas para os controladores correspondentes.

2. **Responsabilidades das Rotas:**

   - Definir associações entre URLs e ações de controladores.
   - Especificar os parâmetros que as ações do controlador esperam.
   - Fornecer URLs amigáveis e significativas para os usuários.

3. **Exemplo de Definição de Rota:**

   No arquivo `config/routes.rb`, você pode definir rotas usando o método `get`, `post`, `put`, `patch` e `delete`. Aqui está um exemplo de rota que mapeia a URL "/tasks" para a ação "index" do controlador "Tasks":

   ```ruby
   get '/tasks', to: 'tasks#index'
   ```

   Isso significa que quando um usuário acessa a URL "/tasks", o controlador "Tasks" irá disparar a ação "index".

**Exemplo Completo de Visualização, Controlador e Rotas:**

1. **Visualização:**

   Em uma visualização em HTML com Ruby incorporado, você pode exibir dados do modelo de tarefas:

   ```html
   <h1>Lista de Tarefas</h1>
   <ul>
     <% @tasks.each do |task| %>
       <li><%= task.title %></li>
     <% end %>
   </ul>
   ```

2. **Controlador:**

   O controlador "Tasks" pode buscar dados do modelo de tarefas e fornecê-los à visualização:

   ```ruby
   class TasksController < ApplicationController
     def index
       @tasks = Task.all
     end
   end
   ```

3. **Rotas:**

   As rotas definidas no arquivo `config/routes.rb` associam a URL "/tasks" à ação "index" no controlador "Tasks":

   ```ruby
   get '/tasks', to: 'tasks#index'
   ```

Isso significa que quando um usuário acessa "/tasks", a ação "index" do controlador "Tasks" é chamada, e a visualização correspondente é renderizada.

Juntos, as visualizações, controladores e rotas formam o mecanismo essencial que permite ao Ruby on Rails criar interfaces de usuário dinâmicas e direcionar as solicitações dos usuários para as partes apropriadas do aplicativo.