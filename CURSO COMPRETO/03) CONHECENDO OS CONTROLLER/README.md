# CONHECENDO OS CONTROLLER
Os controladores (controllers) em Ruby on Rails são responsáveis por lidar com solicitações HTTP e tomar decisões sobre como responder a essas solicitações. Eles são uma parte fundamental do padrão de arquitetura MVC (Model-View-Controller) do Rails. Aqui estão alguns conceitos importantes e uma visão geral de como os controladores funcionam:

**1. Responsabilidades dos Controladores:**
   
   - Receber solicitações HTTP dos clientes (navegadores, aplicativos móveis, etc.).
   - Interagir com o modelo (geralmente um banco de dados) para buscar ou manipular dados.
   - Renderizar visualizações para serem exibidas no navegador.
   - Controlar o fluxo de uma solicitação, tomar decisões com base nos dados da solicitação e modelagem.

**2. Estrutura de um Controlador:**

   Um controlador em Ruby on Rails é uma classe Ruby que herda da classe `ApplicationController`. Por exemplo:

   ```ruby
   class TasksController < ApplicationController
     # Métodos de ação (action) vão aqui
   end
   ```

   Os métodos de ação em um controlador correspondem às ações HTTP, como `index`, `new`, `create`, `edit`, `update`, `destroy`, entre outros.

**3. Ações Básicas:**

   - **index:** Lista os registros. Por exemplo, exibir uma lista de tarefas.
   - **show:** Exibe detalhes de um registro específico.
   - **new:** Exibe o formulário para criar um novo registro.
   - **create:** Cria um novo registro com base nos dados do formulário.
   - **edit:** Exibe o formulário para editar um registro existente.
   - **update:** Atualiza um registro com base nos dados do formulário.
   - **destroy:** Exclui um registro.

**4. Exemplo de Métodos de Ação:**

   Aqui está um exemplo de um controlador de tarefas com métodos de ação simples:

   ```ruby
   class TasksController < ApplicationController
     def index
       @tasks = Task.all
     end

     def show
       @task = Task.find(params[:id])
     end

     def new
       @task = Task.new
     end

     def create
       @task = Task.new(task_params)
       if @task.save
         redirect_to tasks_path
       else
         render 'new'
       end
     end

     def edit
       @task = Task.find(params[:id])
     end

     def update
       @task = Task.find(params[:id])
       if @task.update(task_params)
         redirect_to task_path(@task)
       else
         render 'edit'
       end
     end

     def destroy
       @task = Task.find(params[:id])
       @task.destroy
       redirect_to tasks_path
     end

     private

     def task_params
       params.require(:task).permit(:title, :description, :completed)
     end
   end
   ```

**5. Parâmetros da Solicitação:**

   Os parâmetros da solicitação, como os enviados por formulários, são acessíveis no controlador por meio do objeto `params`. Você pode usá-los para recuperar dados da solicitação e tomar decisões com base neles.

**6. Filtros (Filters):**

   Rails fornece filtros que podem ser aplicados a ações de controlador. Um exemplo comum é o `before_action`, que permite executar métodos antes de entrar em uma ação. Isso é útil para verificar a autenticação do usuário, por exemplo.

**7. Redirecionamento e Renderização:**

   Você pode usar os métodos `redirect_to` para redirecionar para outra página e `render` para exibir uma visualização. Por exemplo, após criar uma tarefa, você pode redirecionar o usuário para a lista de tarefas.

**8. Views (Visualizações):**

   As visualizações são arquivos HTML incorporando código Ruby (geralmente ERB) que são renderizados pelos controladores. As variáveis de instância definidas no controlador podem ser usadas nas visualizações para exibir dados dinâmicos.

**9. Roteamento:**

   As rotas definidas no arquivo `config/routes.rb` mapeiam URLs para ações nos controladores.

Controladores desempenham um papel crítico na criação de aplicativos Ruby on Rails, permitindo que você gerencie a lógica de negócios e interaja com o modelo de dados. Conforme você se aprofunda no desenvolvimento com Rails, você aprenderá a trabalhar com mais complexidade, como autenticação e autorização, e a criar controladores personalizados para atender às necessidades específicas do seu aplicativo.