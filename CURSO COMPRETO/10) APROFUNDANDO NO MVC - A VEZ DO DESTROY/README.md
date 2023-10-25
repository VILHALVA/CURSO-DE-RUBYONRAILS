# APROFUNDANDO NO MVC - A VEZ DO DESTROY
Aprofundando no padrão MVC (Model-View-Controller) em Ruby on Rails, é fundamental entender como a ação `destroy` funciona para permitir a exclusão de registros. Vamos explorar a ação `destroy` em detalhes:

**`destroy` no Controlador (Controller):**

A ação `destroy` é responsável por excluir um registro específico do banco de dados. Essa ação geralmente é desencadeada quando o usuário clica em um botão "Excluir" em uma interface de usuário.

Exemplo de código no controlador:

```ruby
def destroy
  @post = Post.find(params[:id])
  @post.destroy
  redirect_to posts_path
end
```

No exemplo acima, estamos localizando o registro com base no ID fornecido na URL, excluindo-o do banco de dados usando o método `destroy`, e em seguida, redirecionando o usuário para uma página que lista os registros restantes (no exemplo, `posts_path`).

**Roteamento (Routes):**

Para permitir a exclusão de registros, você deve definir uma rota para a ação `destroy` no seu arquivo `config/routes.rb`.

Exemplo de código no arquivo `config/routes.rb`:

```ruby
delete '/posts/:id', to: 'posts#destroy', as: 'delete_post'
```

Neste exemplo, estamos definindo uma rota que mapeia a URL "/posts/:id" para a ação `destroy` no controlador `Posts`. O método `delete` é usado para lidar com solicitações de exclusão.

**Botão de Exclusão na Visualização (View):**

Na visualização onde você exibe os registros, geralmente você incluirá um botão ou link "Excluir" para permitir que os usuários solicitem a exclusão de um registro específico. Você pode usar um formulário ou um simples link para fazer isso.

Exemplo de código em uma visualização:

```html
<%= link_to 'Excluir', delete_post_path(post), method: :delete, data: { confirm: 'Tem certeza?' } %>
```

Neste exemplo, estamos usando o método `link_to` para criar um link "Excluir". O atributo `method: :delete` indica que esta é uma solicitação de exclusão, e o atributo `data: { confirm: 'Tem certeza?' }` exibe uma confirmação ao usuário antes de realizar a exclusão.

**Segurança:**

A exclusão de registros é uma operação crítica, e é importante garantir que apenas usuários autorizados possam excluí-los. Certifique-se de implementar controles de autenticação e autorização para proteger contra exclusões não autorizadas. Isso geralmente envolve o uso de sistemas de autenticação e autorização, como Devise ou Pundit, para verificar as permissões dos usuários.

Além disso, considere a inclusão de uma confirmação antes de realizar a exclusão, como no exemplo acima. Isso ajuda a evitar a exclusão acidental de registros.

Aprofundar-se na ação `destroy` em Ruby on Rails é crucial para permitir que os usuários excluam registros de forma segura e eficiente. Certifique-se de compreender a interação entre o controlador, as visualizações e as rotas para criar uma experiência de exclusão de registros que seja segura e amigável para o usuário.