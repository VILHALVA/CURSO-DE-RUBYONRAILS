# ASSOCIATIONS - HAS_ONE THROUGH
Em Ruby on Rails, o relacionamento `has_one :through` permite estabelecer uma associação entre dois modelos por meio de um terceiro modelo associativo. Isso é útil quando você deseja criar uma relação indireta onde um modelo tem apenas um relacionamento com outro modelo através de um terceiro modelo. Vamos explorar como configurar uma associação `has_one :through`:

Suponha que você tenha três modelos: `User`, `Subscription`, e `Account`. Você deseja estabelecer um relacionamento onde cada usuário tem uma conta através de sua assinatura. O modelo `Subscription` age como um modelo associativo para conectar os usuários às contas.

Aqui está como você configuraria essa relação:

**1. Defina os modelos:**

```ruby
# user.rb
class User < ApplicationRecord
  has_one :subscription
  has_one :account, through: :subscription
end

# subscription.rb
class Subscription < ApplicationRecord
  belongs_to :user
  belongs_to :account
end

# account.rb
class Account < ApplicationRecord
  has_one :subscription
  has_one :user, through: :subscription
end
```

Neste exemplo, o modelo `User` tem uma associação `has_one :subscription`, o que significa que cada usuário tem uma assinatura. O modelo `Subscription` age como um modelo intermediário para associar usuários a contas. A associação `has_one :account, through: :subscription` no modelo `User` define que cada usuário tem uma conta através de sua assinatura.

Da mesma forma, o modelo `Account` tem uma associação `has_one :subscription`, que também é conectada por meio do modelo `Subscription`. A associação `has_one :user, through: :subscription` no modelo `Account` define que cada conta pertence a um usuário através de sua assinatura.

**2. Migrações de banco de dados:**

Certifique-se de criar migrações para as tabelas `users`, `subscriptions` e `accounts` que refletem esses relacionamentos. A tabela `subscriptions` atua como uma tabela intermediária para conectar usuários a contas.

**3. Uso da Associação:**

Agora, você pode usar essa associação em seu aplicativo. Por exemplo, para criar uma nova conta para um usuário:

```ruby
user = User.find(1)
user.create_account
```

Isso criará uma nova conta associada a esse usuário através de sua assinatura.

Para acessar a conta de um usuário:

```ruby
user = User.find(1)
account = user.account
```

Isso retornará a conta associada a esse usuário através de sua assinatura.

A associação `has_one :through` é útil quando você precisa modelar relacionamentos complexos entre modelos em que um modelo tem apenas um relacionamento com outro modelo através de um terceiro modelo associativo. É especialmente útil em cenários em que a relação é única e direta, mas a ligação entre os modelos requer um modelo intermediário.