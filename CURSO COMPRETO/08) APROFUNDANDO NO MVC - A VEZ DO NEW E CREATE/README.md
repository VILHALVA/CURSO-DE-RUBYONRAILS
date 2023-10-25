# APROFUNDANDO NO MVC - A VEZ DO NEW E CREATE
Aprofundando no padrão MVC (Model-View-Controller) em Ruby on Rails, é importante entender o fluxo de trabalho ao criar novos registros e como o `new` e `create` são fundamentais nesse processo.

**`new` e `create` no Controlador (Controller):**

1. **new:** A ação `new` é responsável por exibir um formulário para criar um novo registro. Quando o usuário acessa uma URL associada a esta ação, como "/posts/new" em um blog, o controlador exibirá o formulário vazio para que o usuário preencha.

   Exemplo:

   ```ruby
   def new
     @post = Post.new
   end
   ```

   No exemplo acima, estamos criando uma nova instância do modelo `Post` para representar o novo registro, e esta instância é atribuída a uma variável de instância `@post`, que é usada na visualização do formulário.

2. **create:** A ação `create` é responsável por processar os dados enviados pelo usuário por meio do formulário. Quando o usuário envia o formulário preenchido, os dados são enviados como parte de uma solicitação POST. O controlador `create` processa esses dados, cria um novo registro e salva-o no banco de dados.

   Exemplo:

   ```ruby
   def create
     @post = Post.new(post_params)
     if @post.save
       redirect_to @post
     else
       render 'new'
     end
   end
   ```

   Neste exemplo, estamos criando uma nova instância do modelo `Post` com base nos parâmetros fornecidos pelo usuário (normalmente do formulário). Em seguida, verificamos se a operação de salvamento foi bem-sucedida. Se for bem-sucedida, redirecionamos o usuário para a página de detalhes do post. Caso contrário, renderizamos novamente o formulário com mensagens de erro.

**Visualizações (Views):**

1. **Formulário de Criação:** A visualização associada à ação `new` exibe um formulário de criação vazio para o usuário preencher. Geralmente, essa visualização é um formulário HTML com campos que correspondem aos atributos do modelo.

   Exemplo:

   ```html
   <%= form_for @post do |f| %>
     <%= f.label :title %>
     <%= f.text_field :title %>

     <%= f.label :content %>
     <%= f.text_area :content %>

     <%= f.submit 'Create Post' %>
   <% end %>
   ```

2. **Formulário de Processamento:** A visualização associada à ação `create` geralmente não é acessada diretamente pelos usuários, pois ela lida com o processamento dos dados do formulário. Se ocorrer um erro durante a criação, você pode renderizar a visualização `new` novamente com mensagens de erro para que o usuário possa corrigir os dados.

**Roteamento (Routes):**

1. **Rota para `new`:** Você deve definir uma rota para a ação `new` no seu arquivo `config/routes.rb`. Isso mapeia uma URL, como "/posts/new", para a ação `new` no controlador `Posts`.

   Exemplo:

   ```ruby
   get '/posts/new', to: 'posts#new'
   ```

2. **Rota para `create`:** Da mesma forma, você deve definir uma rota para a ação `create`, que trata da submissão do formulário.

   Exemplo:

   ```ruby
   post '/posts', to: 'posts#create'
   ```

**Formulários (Forms):**

1. **`form_for`:** O método `form_for` é usado nas visualizações `new` e `create` para gerar um formulário HTML que está vinculado ao modelo `@post`. Ele permite que os dados do formulário sejam enviados ao controlador na ação `create`.

**Segurança e Validações:**

1. **Validações:** É importante definir validações no modelo para garantir que os dados sejam inseridos corretamente no banco de dados. Você pode usar métodos como `validates_presence_of` e `validates_length_of` para definir regras de validação.

2. **Strong Parameters:** No controlador, você deve usar o conceito de strong parameters para proteger contra ataques de atribuição em massa (mass assignment) e permitir apenas os parâmetros necessários para a ação `create`.

   Exemplo:

   ```ruby
   def post_params
     params.require(:post).permit(:title, :content)
   end
   ```

Aprofundar-se no `new` e `create` em Ruby on Rails é crucial para criar formulários de criação e processá-los com segurança e eficiência. Certifique-se de compreender a interação entre o controlador, as visualizações e as rotas para criar uma experiência de criação de registros perfeita para seus usuários.