# ASSOCIATIONS - HAS AND BELONGS TO MANY
A associação `has_and_belongs_to_many`, frequentemente abreviada como HABTM, é usada em Ruby on Rails para estabelecer relacionamentos "muitos-para-muitos" entre dois modelos. Esse tipo de associação é adequado quando você tem dois modelos que podem estar associados a vários registros de cada lado. Não há necessidade de um modelo intermediário, como em `has_many :through`. Vamos explorar como configurar uma associação `has_and_belongs_to_many`:

Suponha que você tenha dois modelos: `User` e `Role`. Cada usuário pode ter várias funções e, ao mesmo tempo, uma função pode ser atribuída a vários usuários.

**1. Defina os modelos:**

```ruby
# user.rb
class User < ApplicationRecord
  has_and_belongs_to_many :roles
end

# role.rb
class Role < ApplicationRecord
  has_and_belongs_to_many :users
end
```

Neste exemplo, o modelo `User` tem uma associação `has_and_belongs_to_many :roles`, o que significa que um usuário pode ter várias funções. Da mesma forma, o modelo `Role` tem uma associação `has_and_belongs_to_many :users`, o que indica que uma função pode ser atribuída a vários usuários.

**2. Migrações de banco de dados:**

Você precisa criar uma tabela intermediária no banco de dados para fazer a ligação entre os modelos `User` e `Role`. Esta tabela deve seguir uma convenção de nomenclatura que combina os nomes dos modelos no plural, em ordem alfabética, separados por um sublinhado. Nesse caso, a tabela intermediária deve ser chamada `roles_users`.

Aqui está como você pode criar as migrações para as tabelas:

```ruby
# Migration para a tabela de usuários
class CreateUsers < ActiveRecord::Migration
  def change
    create_table :users do |t|
      t.string :name
      # outros campos
      t.timestamps
    end
  end
end

# Migration para a tabela de funções
class CreateRoles < ActiveRecord::Migration
  def change
    create_table :roles do |t|
      t.string :name
      # outros campos
      t.timestamps
    end
  end
end

# Migration para a tabela intermediária roles_users
class CreateRolesUsers < ActiveRecord::Migration
  def change
    create_table :roles_users, id: false do |t|
      t.integer :user_id
      t.integer :role_id
    end
  end
end
```

Observe que na migração da tabela intermediária `roles_users`, estamos especificando `id: false` para evitar que essa tabela tenha uma coluna de ID primária.

**3. Uso da Associação:**

Agora, você pode associar usuários a funções e vice-versa:

Para adicionar uma função a um usuário:

```ruby
user = User.find(1)
role = Role.find(1)
user.roles << role
```

Isso adicionará a função ao conjunto de funções associadas a esse usuário.

Para listar as funções de um usuário:

```ruby
user = User.find(1)
roles = user.roles
```

Isso retornará uma coleção de funções associadas a esse usuário.

A associação `has_and_belongs_to_many` é útil quando você precisa estabelecer relacionamentos muitos-para-muitos de maneira simples e direta, sem a necessidade de um modelo intermediário. No entanto, essa associação é limitada em termos de personalização de campos na tabela intermediária. Se você precisar de atributos adicionais associados a essa relação, considere usar `has_many :through`.