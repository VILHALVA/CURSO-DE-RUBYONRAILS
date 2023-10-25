# APROFUNDANDO NO MVC - A VEZ DO EDIT E UPDATE
Aprofundando no padrão MVC (Model-View-Controller) em Ruby on Rails, é fundamental entender como as ações `edit` e `update` funcionam para permitir a edição de registros. Vamos explorar essas ações em detalhes:

**`edit` e `update` no Controlador (Controller):**

1. **`edit`:** A ação `edit` é responsável por exibir um formulário pré-preenchido que permite aos usuários editar um registro existente. Quando o usuário acessa uma URL associada a esta ação, como "/posts/1/edit", o controlador busca os dados do registro que deseja editar e exibe o formulário preenchido com esses dados.

   Exemplo:

   ```ruby
   def edit
     @post = Post.find(params[:id])
   end
   ```

   Neste exemplo, estamos localizando o registro com base no ID fornecido na URL e atribuindo-o a uma variável de instância `@post`, que é usada na visualização do formulário.

2. **`update`:** A ação `update` é responsável por processar os dados enviados pelo usuário por meio do formulário de edição. Quando o usuário envia o formulário preenchido, os dados são enviados como parte de uma solicitação POST. O controlador `update` processa esses dados, atualiza o registro existente no banco de dados e redireciona o usuário para a página de detalhes do registro atualizado.

   Exemplo:

   ```ruby
   def update
     @post = Post.find(params[:id])
     if @post.update(post_params)
       redirect_to @post
     else
       render 'edit'
     end
   end
   ```

   Neste exemplo, estamos localizando o registro com base no ID fornecido na URL, atualizando-o com os parâmetros fornecidos pelo usuário (normalmente do formulário) e verificando se a operação de atualização foi bem-sucedida. Se for bem-sucedida, redirecionamos o usuário para a página de detalhes do post. Caso contrário, renderizamos novamente o formulário com mensagens de erro.

**Visualizações (Views):**

1. **Formulário de Edição:** A visualização associada à ação `edit` exibe um formulário pré-preenchido com os dados do registro a ser editado. O usuário pode fazer alterações nos campos conforme necessário.

   Exemplo:

   ```html
   <%= form_for @post do |f| %>
     <%= f.label :title %>
     <%= f.text_field :title %>

     <%= f.label :content %>
     <%= f.text_area :content %>

     <%= f.submit 'Update Post' %>
   <% end %>
   ```

2. **Formulário de Processamento:** A visualização associada à ação `update` geralmente não é acessada diretamente pelos usuários, pois ela lida com o processamento dos dados do formulário. Se ocorrer um erro durante a atualização, você pode renderizar a visualização `edit` novamente com mensagens de erro para que o usuário possa corrigir os dados.

**Roteamento (Routes):**

1. **Rota para `edit`:** Você deve definir uma rota para a ação `edit` no seu arquivo `config/routes.rb`. Isso mapeia uma URL, como "/posts/1/edit", para a ação `edit` no controlador `Posts`.

   Exemplo:

   ```ruby
   get '/posts/:id/edit', to: 'posts#edit', as: 'edit_post'
   ```

2. **Rota para `update`:** Da mesma forma, você deve definir uma rota para a ação `update`, que trata da submissão do formulário de edição.

   Exemplo:

   ```ruby
   patch '/posts/:id', to: 'posts#update'
   ```

**Formulários (Forms):**

1. **`form_for`:** O método `form_for` é usado nas visualizações `edit` e `update` para gerar um formulário HTML que está vinculado ao modelo `@post`. Isso permite que os dados do formulário sejam enviados ao controlador na ação `update`.

**Segurança e Validações:**

1. **Validações:** Certifique-se de manter as validações no modelo para garantir que os dados sejam atualizados corretamente no banco de dados.

2. **Strong Parameters:** No controlador, você deve usar os strong parameters para proteger contra ataques de atribuição em massa e permitir apenas os parâmetros necessários para a ação `update`.

   Exemplo:

   ```ruby
   def post_params
     params.require(:post).permit(:title, :content)
   end
   ```

Aprofundar-se nas ações `edit` e `update` em Ruby on Rails é crucial para permitir que os usuários editem registros existentes com segurança e eficiência. Certifique-se de compreender a interação entre o controlador, as visualizações e as rotas para criar uma experiência de edição de registros perfeita para seus usuários.