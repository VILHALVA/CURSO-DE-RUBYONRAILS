# ASSOCIATIONS - BELONGS_TO, HAS_MANY E HAS_ONE
Em Ruby on Rails, as associações (associations) são um conceito fundamental que permitem estabelecer relacionamentos entre modelos (models) para representar a estrutura de dados de um aplicativo de maneira eficaz. Existem três tipos principais de associações: `belongs_to`, `has_many` e `has_one`. Vamos explorar cada um deles:

**1. `belongs_to`:**

A associação `belongs_to` é usada para estabelecer um relacionamento de "pertence a" entre dois modelos. Ela é frequentemente usada no lado "pertencente" do relacionamento. Por exemplo, se você tem um modelo `Comment` e um modelo `Post`, você pode usar `belongs_to` para indicar que um comentário pertence a um post.

Exemplo:

```ruby
class Comment < ApplicationRecord
  belongs_to :post
end
```

Neste exemplo, um comentário pertence a um post. Isso significa que cada registro de comentário está associado a um único registro de post. Você pode acessar o post relacionado a partir de um comentário usando `comment.post`.

**2. `has_many`:**

A associação `has_many` é usada para estabelecer um relacionamento de "tem muitos" entre dois modelos. Ela é frequentemente usada no lado "possuidor" do relacionamento. Usando o exemplo anterior, um post pode ter muitos comentários, então você usaria `has_many` no modelo `Post`.

Exemplo:

```ruby
class Post < ApplicationRecord
  has_many :comments
end
```

Neste exemplo, um post pode ter muitos comentários. Isso significa que você pode acessar todos os comentários associados a um post usando `post.comments`.

**3. `has_one`:**

A associação `has_one` é usada para estabelecer um relacionamento de "tem um" entre dois modelos. Ela é frequentemente usada quando você deseja que um modelo tenha no máximo um registro associado de outro modelo. Por exemplo, se você tem um modelo `Profile` e um modelo `User`, você pode usar `has_one` para associar um perfil a um usuário.

Exemplo:

```ruby
class User < ApplicationRecord
  has_one :profile
end
```

Neste exemplo, um usuário pode ter no máximo um perfil. Isso significa que você pode acessar o perfil associado a um usuário usando `user.profile`.

**Outras Opções:**

Além dessas associações fundamentais, há opções adicionais que podem ser usadas para personalizar o comportamento das associações. Algumas das opções comuns incluem:

- `dependent`: Essa opção permite especificar o que acontece com os registros associados quando o registro pai é excluído. Por exemplo, `dependent: :destroy` excluirá todos os registros associados quando o registro pai for excluído.

- `foreign_key`: Use essa opção para especificar o nome da coluna de chave estrangeira que será usada para estabelecer a associação. Por padrão, o Rails assume que a chave estrangeira segue a convenção `model_id`, mas você pode personalizá-la conforme necessário.

- `class_name`: Use esta opção para especificar o nome da classe do modelo associado se ela não seguir a convenção de nomenclatura padrão.

- `through`: Esta opção é usada para estabelecer associações `has_many` através de outra associação. Isso é comumente usado para relacionamentos muitos para muitos.

- E muitas outras opções que permitem personalizar o comportamento das associações.

As associações são uma parte crucial do desenvolvimento de aplicativos Ruby on Rails, pois permitem representar relações complexas entre os dados de forma organizada e eficiente. Dominar o uso correto das associações é fundamental para o desenvolvimento eficaz de aplicativos Rails.