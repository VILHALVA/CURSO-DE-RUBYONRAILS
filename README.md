# CURSO DE RUBY ON RAILS
👨‍⚖️RUBY ON RAILS É UM FRAMEWORK DE DESENVOLVIMENTO WEB ESCRITO EM RUBY. ELE SEGUE O PADRÃO MVC (MODEL-VIEW-CONTROLLER) E FACILITA A CRIAÇÃO DE APLICATIVOS WEB, FORNECENDO UMA ESTRUTURA ORGANIZADA E CONVENÇÕES DE CODIFICAÇÃO. É CONHECIDO POR SUA SIMPLICIDADE E PRODUTIVIDADE.

[![GitHub Repo stars](https://img.shields.io/badge/VILHALVA-GITHUB-03A9F4?logo=github)](https://github.com/VILHALVA) 
[![GitHub Repo stars](https://img.shields.io/badge/VEJA-DOCUMENTAÇÃO-03A9F4?logo=google)](https://guides.rubyonrails.org/) <br>

[![GitHub Repo stars](https://img.shields.io/badge/-PLAYLIST%20DO%20YOUTUBE-blueviolet)](https://youtube.com/playlist?list=PLnV7i1DUV_zP6BV1xoy0TV5IkPcYtz6rx&si=d8KqAEVtfo6-nY4Z)

<img src="https://assets.stickpng.com/images/62c48bd4d884e8c372162224.png" align="center" width="280"> <br>

![](https://i.imgur.com/waxVImv.png)

# CONCEITO:
Ruby on Rails, muitas vezes abreviado como Rails, é um popular framework de desenvolvimento web escrito em Ruby. Ele foi criado para tornar o desenvolvimento de aplicativos web mais rápido e mais fácil, seguindo o princípio de convenção sobre configuração. Aqui estão alguns conceitos-chave e exemplos de código para você começar:

1. **Model-View-Controller (MVC):** Rails segue o padrão de arquitetura MVC. O MVC divide a aplicação em três partes principais:

   - **Model:** Representa a camada de dados. Modelos definem como os dados são estruturados e manipulados. Por exemplo, se você estiver criando uma aplicação de blog, um modelo de "Post" representaria as postagens do blog.

   - **View:** É responsável pela apresentação dos dados aos usuários. As visões em Rails geralmente são criadas em HTML com incorporação de código Ruby (ERB - Embedded Ruby) para mostrar dinamicamente os dados.

   - **Controller:** Atua como intermediário entre o Modelo e a Visão. Ele recebe solicitações do navegador, interage com o modelo e renderiza as vistas apropriadas. É onde a lógica de negócios é implementada.

2. **Rotas (Routes):** No Rails, as rotas mapeiam URLs para ações nos controladores. Você define rotas no arquivo `config/routes.rb`. Aqui está um exemplo de rota:

```ruby
# config/routes.rb
Rails.application.routes.draw do
  get '/posts', to: 'posts#index'
end
```

Isso mapeia a URL '/posts' para a ação 'index' no controlador 'PostsController'.

3. **Controladores (Controllers):** Controladores são responsáveis por lidar com solicitações HTTP e decidir como responder. Aqui está um exemplo de um controlador:

```ruby
class PostsController < ApplicationController
  def index
    @posts = Post.all
  end
end
```

No exemplo acima, o controlador 'PostsController' lida com a solicitação da rota '/posts' e obtém todos os registros da tabela 'Post' do banco de dados.

4. **Modelos (Models):** Os modelos representam tabelas no banco de dados e definem a lógica para interagir com os dados. Aqui está um exemplo de modelo:

```ruby
class Post < ApplicationRecord
  validates :title, presence: true
  validates :content, presence: true
end
```

Este modelo 'Post' possui validações que garantem que os campos 'title' e 'content' não estejam em branco.

5. **Visões (Views):** As visões geralmente são arquivos HTML incorporando código Ruby. Aqui está um exemplo de uma visão que itera sobre os posts e os exibe:

```html
<!-- app/views/posts/index.html.erb -->
<% @posts.each do |post| %>
  <h2><%= post.title %></h2>
  <p><%= post.content %></p>
<% end %>
```

Esses são conceitos fundamentais do Ruby on Rails. À medida que você avança no curso, você aprenderá mais sobre tópicos como migrações de banco de dados, formulários, autenticação e autorização, e muito mais.

# CARACTERISTICAS:
## Características Positivas:
1. **Produtividade:** Ruby on Rails segue o princípio de "convenção sobre configuração" (Convention over Configuration) e "DRY" (Don't Repeat Yourself), o que acelera o desenvolvimento, tornando-o altamente produtivo.

2. **Comunidade Ativa:** Rails tem uma comunidade de desenvolvedores ativa e vibrante. Isso significa que há muitos recursos, bibliotecas e gemas disponíveis para ajudar no desenvolvimento.

3. **Abundância de Gemas:** O sistema de gemas de Ruby facilita a incorporação de funcionalidades adicionais em seus projetos. Existem milhares de gemas disponíveis, abrangendo uma ampla variedade de funcionalidades.

4. **Baterias Incluídas:** Rails inclui muitos componentes prontos para uso, como autenticação, geração de formulários e manipulação de banco de dados, o que economiza tempo na configuração.

5. **Segurança:** Rails tem recursos de segurança embutidos, como proteção contra ataques de injeção de SQL e proteção contra CSRF (Cross-Site Request Forgery).

6. **Desenvolvimento Rápido:** A estrutura permite que você prototipe e desenvolva aplicativos web de maneira rápida e eficiente.

## Características Negativas:
1. **Curva de Aprendizado:** Ruby on Rails pode ter uma curva de aprendizado íngreme para iniciantes. As convenções e o tamanho do ecossistema podem ser esmagadores no início.

2. **Escalabilidade:** Embora Rails seja adequado para muitos aplicativos, pode haver desafios de escalabilidade em aplicativos extremamente grandes ou complexos.

3. **Desempenho:** Rails não é a estrutura mais rápida disponível, e você pode precisar otimizar seu código e infraestrutura para obter o desempenho desejado em aplicativos de grande escala.

4. **Migrações de Banco de Dados:** Embora as migrações de banco de dados sejam uma característica útil, elas podem se tornar complicadas em aplicativos complexos com esquemas de banco de dados em constante mudança.

5. **Flexibilidade Limitada:** A ênfase nas convenções pode limitar a flexibilidade em projetos que desviam muito do padrão. Às vezes, você pode precisar lutar contra as convenções.

6. **Manutenção de Versões Antigas:** Às vezes, pode ser desafiador manter aplicativos Rails mais antigos, devido às mudanças nas versões da estrutura e das gemas.

Em geral, Ruby on Rails é uma escolha sólida para o desenvolvimento web, especialmente para projetos de médio porte. No entanto, a escolha de uma estrutura depende das necessidades específicas do seu projeto, da sua equipe e da sua familiaridade com a tecnologia. Certifique-se de considerar cuidadosamente as características positivas e negativas ao decidir se Rails é a melhor escolha para o seu caso.
