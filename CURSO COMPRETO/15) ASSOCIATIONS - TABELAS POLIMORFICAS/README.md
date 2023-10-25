# ASSOCIATIONS - TABELAS POLIMORFICAS
Tabelas polimórficas, ou associações polimórficas, em Ruby on Rails permitem que um modelo esteja associado a vários outros modelos diferentes. Isso é particularmente útil quando você deseja criar uma associação flexível em que um modelo possa pertencer a vários tipos diferentes de modelos. Vamos explorar como configurar e usar tabelas polimórficas em Ruby on Rails.

Suponha que você deseje criar um sistema de comentários onde os comentários possam ser vinculados a vários tipos de conteúdo, como posts, fotos e vídeos. Isso é um cenário típico para o uso de tabelas polimórficas.

**1. Crie um modelo de Comment (Comentário):**

```ruby
rails generate model Comment content:text commentable:references{polymorphic}
```

Isso criará um modelo `Comment` com um campo de texto chamado `content` e uma coluna `commentable_id` para a chave estrangeira e uma coluna `commentable_type` para o tipo do objeto associado.

**2. Associe o modelo Comment com outros modelos:**

No modelo `Comment`, defina a associação polimórfica da seguinte forma:

```ruby
# comment.rb
class Comment < ApplicationRecord
  belongs_to :commentable, polymorphic: true
end
```

**3. Configure os outros modelos (por exemplo, Post, Photo e Video):**

Em cada modelo que você deseja associar com comentários (por exemplo, `Post`, `Photo`, `Video`), você precisa definir a associação de comentários de forma inversa. Por exemplo, no modelo `Post`, você faria o seguinte:

```ruby
# post.rb
class Post < ApplicationRecord
  has_many :comments, as: :commentable
end
```

**4. Migrações de banco de dados:**

Certifique-se de executar migrações para criar as tabelas associadas a esses modelos.

**5. Uso da Associação:**

Agora você pode criar e associar comentários a qualquer um dos modelos relacionados. Por exemplo:

```ruby
# Criar um comentário em um post
post = Post.find(1)
comment = post.comments.create(content: "Este é um ótimo post!")

# Criar um comentário em uma foto
photo = Photo.find(1)
comment = photo.comments.create(content: "Adoro essa foto!")

# Listar todos os comentários associados a um objeto
post = Post.find(1)
comments = post.comments

photo = Photo.find(1)
comments = photo.comments
```

Uma das principais vantagens das tabelas polimórficas é que elas permitem que você crie associações flexíveis e reutilizáveis em cenários onde vários modelos diferentes podem estar associados a um único modelo. No entanto, é importante planejar bem a estrutura de seu banco de dados e como as associações serão usadas em seu aplicativo para evitar complexidade desnecessária.