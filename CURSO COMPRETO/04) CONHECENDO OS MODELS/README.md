# CONHECENDO OS MODELS
Os modelos (models) no Ruby on Rails desempenham um papel fundamental no gerenciamento e manipulação de dados em um aplicativo. Eles representam tabelas no banco de dados e definem as regras de negócios para a interação com esses dados. Abaixo, você encontrará uma visão geral dos modelos em Ruby on Rails:

**1. Responsabilidades dos Modelos:**

- Representam tabelas no banco de dados.
- Definem a estrutura dos dados (colunas da tabela) usando migrações.
- Fornecem métodos para acessar, inserir, atualizar e excluir registros no banco de dados.
- Validam os dados antes de salvá-los no banco de dados.
- Estabelecem relações entre modelos para representar associações entre tabelas.

**2. Estrutura de um Modelo:**

- Um modelo em Ruby on Rails é uma classe Ruby que herda da classe `ApplicationRecord`.
- Por exemplo, aqui está um modelo simples chamado `Task`:

```ruby
class Task < ApplicationRecord
  validates :title, presence: true
  validates :description, length: { maximum: 255 }
end
```

**3. Migrações:**

- As migrações são usadas para definir a estrutura da tabela no banco de dados.
- Por exemplo, você pode criar uma migração para criar a tabela de tarefas:

```bash
rails generate migration CreateTasks title:string description:text completed:boolean
```

- Após criar a migração, você pode aplicá-la ao banco de dados com `rake db:migrate`.

**4. Métodos de Acesso ao Banco de Dados:**

- Os modelos fornecem métodos para acessar registros no banco de dados. Alguns exemplos incluem `find`, `all`, `where`, `create`, `save`, `update`, e `destroy`.
- Por exemplo, para buscar todas as tarefas não concluídas:

```ruby
incomplete_tasks = Task.where(completed: false)
```

**5. Validações:**

- Os modelos geralmente incluem validações para garantir que os dados inseridos no banco de dados estejam corretos.
- No exemplo do modelo `Task` acima, estamos validando que o título é obrigatório e que a descrição tem um limite de 255 caracteres.

**6. Associações:**

- Os modelos podem estabelecer associações uns com os outros para representar relacionamentos entre tabelas no banco de dados.
- Por exemplo, um modelo `User` pode ter muitas tarefas, e uma tarefa pode pertencer a um único usuário.

**7. Callbacks:**

- Os modelos podem incluir callbacks que são acionados em momentos específicos durante o ciclo de vida de um objeto.
- Isso permite que você adicione lógica personalizada antes ou após a criação, atualização ou exclusão de um registro.

**8. Consultas Complexas:**

- Você pode usar métodos de consulta para criar consultas complexas e personalizadas ao banco de dados, o que é útil para buscar dados específicos com base em critérios personalizados.

**9. Integração com o Controlador e a Visualização:**

- Os controladores utilizam os modelos para buscar e manipular dados que serão exibidos nas visualizações.

**10. Validando Dados do Formulário:**

- Os modelos são frequentemente usados para validar dados de formulários antes de salvar no banco de dados, garantindo que os dados sejam válidos e seguros.

**11. Testes Unitários:**

- Os modelos são frequentemente testados com testes unitários para garantir que funcionem corretamente.

Os modelos desempenham um papel crítico na construção de aplicativos Rails, permitindo que você gerencie os dados de maneira eficiente e segura. Eles ajudam a manter a integridade dos dados e a garantir que as regras de negócios sejam aplicadas consistentemente. Conforme você continua a desenvolver aplicativos com Rails, você aprenderá a trabalhar com modelos mais complexos e explorar recursos adicionais.