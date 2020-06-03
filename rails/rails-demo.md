# Rails Demo

## Install Rails

```text
gem install rails
rails _5.2.3_ new blog -d postgresql --skip-turbolinks --skip-coffee
cd blog
rails db:create
```

## Start the Rails Server

```text
rails server
```

## Routes

#### Open the file `config/routes.rb` in your editor.

```ruby
Rails.application.routes.draw do
  root 'articles#index'
end
```

To see your work:

```text
rake routes
```

Create a controller: \(controller names are plural\)

```text
touch app/controllers/articles_controller.rb
```

Add a method for each RESTful action.

```text
class ArticlesController < ApplicationController
  def index
  end

  def show
  end

  def new
  end

  def edit
  end

  def create
  end

  def update
  end

  def destroy
  end
end
```

\(view directory names are plural, file names are normally singular\)

```text
mkdir app/views/articles
touch app/views/articles/index.html.erb
touch app/views/articles/new.html.erb
```

#### Add this code into app/views/articles/index.html.erb

```text
<h1>hello world</h1>
```

#### Try it out

#### Add this code into app/views/articles/new.html.erb

```text
<%= form_with scope: :article, url: articles_path, local: true do |form| %>
  <p>
    <%= form.label :title %><br>
    <%= form.text_field :title %>
  </p>

  <p>
    <%= form.label :text %><br>
    <%= form.text_area :text %>
  </p>

  <p>
    <%= form.submit %>
  </p>
<% end %>
```

#### Add the route to config/routes.rb

```text
  get '/articles/new' => 'articles#new', as: 'new_article'
```

#### Change the create method to output the params being sent to it:

```text
def create
  render plain: params[:article].inspect
end
```

#### Add the route to config/routes.rb

```text
  post '/articles' => 'articles#create'
```

#### Try it out in the browser:

[http://localhost:3000/articles/new](http://localhost:3000/articles/new)

#### Create the table:

```text
rails generate migration articles
```

Look inside the generated file:

```text
class Articles < ActiveRecord::Migration
  def change
  end
end
```

Inside the `change` method add your table creation code:

```text
create_table :articles do |t|
  t.string :title
  t.text :text
  t.timestamps
end
```

#### Run the migration

```text
rails db:migrate
```

#### Create the model

touch app/models/article.rb \(model filenames are singular\)

```text
class Article < ApplicationRecord
  # AR classes are singular and capitalized by convention
end
```

#### Start saving things in the controller:

```text
def create
  @article = Article.new(article_params)

  @article.save
  redirect_to @article
end
```

At the bottom of the file put the private article\_params security method:

```text
private
  def article_params
    params.require(:article).permit(:title, :text)
  end
```

#### Add to the show controller

```text
def show
  @article = Article.find(params[:id])
end
```

#### Create a new file app/views/articles/show.html.erb with the following content:

```text
<p>
  <strong>Title:</strong>
  <%= @article.title %>
</p>

<p>
  <strong>Text:</strong>
  <%= @article.text %>
</p>
```

#### Also add a link to go back to the index action as well, so that people who are viewing a single article can go back and view the whole list:

```text
<%= link_to 'Back', root_path %>
```

#### Add the route to the config/routes.rb file

```text
  get '/articles/:id' => 'articles#show' , as: 'article'
```

#### Add to the index controller

```text
def index
  @articles = Article.all
end
```

#### Add the view for this action, located at app/views/articles/index.html.erb

```text
<h1>Listing articles</h1>

<table>
  <tr>
    <th>Title</th>
    <th>Text</th>
    <th></th>
  </tr>

  <% @articles.each do |article| %>
    <tr>
      <td><%= article.title %></td>
      <td><%= article.text %></td>
      <td><%= link_to 'Show', article_path(article) %></td>
    </tr>
  <% end %>
</table>
```

#### Add this "New Article" link to app/views/articles/index.html.erb placing it above the  tag:

```text
<%= link_to 'New article', new_article_path %>
```

#### Add another link in app/views/articles/new.html.erb underneath the form, to go back to the index action:

```text
<%= form_with scope: :article, url: articles_path, local: true do |form| %>
  ...
<% end %>

<%= link_to 'Back', root_path %>
```

### Editing

#### Add an edit action to the ArticlesController

```text
def edit
  @article = Article.find(params[:id])
end
```

#### create the route

```text
get '/articles/:id/edit' => 'articles#edit', as: 'edit_article'
```

#### Create a file called app/views/articles/edit.html.erb

```text
<h1>Edit article</h1>

<%= form_with scope: :article, model: @article, local: true do |form| %>

  <p>
    <%= form.label :title %><br>
    <%= form.text_field :title %>
  </p>

  <p>
    <%= form.label :text %><br>
    <%= form.text_area :text %>
  </p>

  <p>
    <%= form.submit %>
  </p>

<% end %>

<%= link_to 'Back', root_path %>
```

#### Add the route to the config/routes.rb file

```text
patch '/articles/:id' => 'articles#update'
```

#### Create the update action in app/controllers/articles\_controller.rb

```text
def update
  @article = Article.find(params[:id])

  @article.update(article_params)
  redirect_to @article
end
```

#### Add the edit link to app/views/articles/index.html.erb to make it appear next to the "Show" link:

```text
<td><%= link_to 'Edit', edit_article_path(article) %></td>
```

#### Also add one to the app/views/articles/show.html.erb template as well

```text
<%= link_to 'Edit', edit_article_path(@article) %>
```

## Deleting

#### Add the route to the config/routes.rb file

```text
delete '/articles/:id' => 'articles#destroy'
```

#### Add the delete controller to app/controllers/articles\_controller.rb

```text
def destroy
  @article = Article.find(params[:id])
  @article.destroy

  redirect_to root_path
end
```

Add a 'Destroy' link to your index action template, inside the loop \(app/views/articles/index.html.erb\)

```text
<td><%= link_to 'Destroy', article_path(article),
        method: :delete,
        data: { confirm: 'Are you sure?' } %></td>
```

### Pairing Exercise

Run the above code.

