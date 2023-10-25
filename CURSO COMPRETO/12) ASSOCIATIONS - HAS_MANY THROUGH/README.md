# ASSOCIATIONS - HAS_MANY THROUGH 
A associação `has_many through` é uma relação complexa no framework Ruby on Rails que permite estabelecer um relacionamento indireto entre dois modelos por meio de um terceiro modelo associativo. Essa associação é útil quando você deseja criar relacionamentos de "muitos para muitos" entre modelos com um grau adicional de flexibilidade e complexidade. Vamos explorar como funciona e como configurar uma associação `has_many through`:

Suponha que você tenha três modelos: `Author`, `Book`, e `Authorship`. Você deseja estabelecer um relacionamento onde autores podem ter muitos livros, e um livro pode ter muitos autores. O modelo `Authorship` age como um modelo associativo para conectar autores a livros.

Aqui está como você configuraria essa relação:

**1. Defina os modelos:**

```ruby
# author.rb
class Author < ApplicationRecord
  has_many :authorships
  has_many :books, through: :authorships
end

# book.rb
class Book < ApplicationRecord
  has_many :authorships
  has_many :authors, through: :authorships
end

# authorship.rb
class Authorship < ApplicationRecord
  belongs_to :author
  belongs_to :book
end
```

Neste exemplo, o modelo `Author` tem uma associação `has_many :authorships`, que permite que um autor tenha várias entradas na tabela `Authorship`. Da mesma forma, o modelo `Book` tem uma associação `has_many :authorships`.

A parte crítica é o uso de `has_many :through` nas definições. Em `Author`, `has_many :books, through: :authorships` define que um autor pode ter muitos livros através da tabela `Authorship`. E em `Book`, `has_many :authors, through: :authorships` define que um livro pode ter muitos autores através da mesma tabela `Authorship`.

**2. Migrações de banco de dados:**

Certifique-se de criar migrações para as tabelas `authors`, `books` e `authorships` que refletem esses relacionamentos. A tabela `authorships` atua como uma tabela intermediária para conectar autores e livros.

**3. Uso da Associação:**

Agora, você pode usar essa associação em seu aplicativo. Por exemplo, para adicionar um autor a um livro:

```ruby
author = Author.find(1)
book = Book.find(1)

author.books << book
```

Isso adicionará o livro ao conjunto de livros escritos por esse autor através da tabela `Authorship`.

Para encontrar os autores de um livro:

```ruby
book = Book.find(1)
authors = book.authors
```

Isso retornará uma coleção de autores associados a esse livro.

A associação `has_many through` é poderosa para modelar relacionamentos complexos em que um modelo está relacionado a outro por meio de um terceiro modelo associativo. Pode ser usado em muitos cenários diferentes, como relacionamentos muitos-para-muitos com atributos extras ou até mesmo relações de várias etapas. É uma das características mais úteis do Ruby on Rails para trabalhar com dados complexos de maneira eficiente.