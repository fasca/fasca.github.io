---
layout: post
title: RoR Grafikart
date: 2017-10-27
tags:
  - backend
  - developpement
description: Base du framework RoR...
categories: developpement backend
serie: programmation
published: true
---

Cours [grafikart](https://www.grafikart.fr/), apprendre ruby on rails

# 1 INTRODUCTION

## 1.1 Installation

### L'arbo

```shell
/
|_app
|   |_asset (css,js,img)
|   |_channels (web sockets, systeme de notification instantané) 
|   |_controllers (la logique)
|   |_helpers (ecrire des fonctions qui vont etre propagées et être dispo n'importe ou dans notre appli)
|   |_jobs (permet de creer des tâches)
|   |_mailers (gerer les mails à envoyer ex: inscription utilisateur)
|   |_models (la bdd)
|   |_views (html)
|
|_config (contient la conf de notre appli)
|	|_database.yml (content la conf de notre bdd)
|	|_application.rb (indique comment doit fonctionner notre framework)
|	|_environments (les differents env tq dev, prod ou test)
|	|_routes.rb (les routes)
|
|_db (contient des infos sur la bdd et le seeding pour inserer des info au lancement de la pool)
|
|_lib (library ruby externe à rails)
|
|_log (contient les log)
|
|_public (il faut faire pointer le serveur web ici, c'est la racine)
|
|_test (test unitaire et fonctionnel)
|
|_tmp (fichiers temporaires, cache, session)
|
|_vendor (fichier importé par des lib externes ex bootstrap)
|
|_Gemfile (liste les differents dependance de notre projet)
|
|_Gemfile.lock (permet de locker les dependance, lors d'un bundle install on aura les mêmes versions de gems)
|
|_config.ru (utile à Rake, permet de lancer un serveur web)
|
|_Rakefile (equivalent à Make)

```


Pour lancer un serveur sur le port 3000: `rails server`

Si on lance rails sur une machine virtuelle: `rails s -b 0.0.0.0`

Voir la doc rails (guide) pour plus d'info:
* api.rubyonrails.org
* guides.rubyonrails.org


## 1.2 Notre 1ere page

### Les routes

Les routes sont définies dans `config/routes.rb`, ex:

```ruby
Rails.application.routes.draw do
	#pour afficher la page "salut", il faut executer la methode "salut" presente dans le controller "pages_controller.rb"
	get '/salut', to: 'pages#salut'
end
```

Toutes les classes controllers heritent de `ApplicationController::Base`, donc s'il faut modifier quelquechose, on peut modifier cette classe.

On crée un controller pour gérer des pages:

`pages_controller.rb`:
```ruby
class PagesController < ApplicationController
	def salut
	end
end
```

Il faut créer la vue de notre action `salut` dans un nouveau dossier ayant pour nom le controller en question, donc dans `views/pages/salut.html.erb` (RoR utilise le moteur de template ERB pour generer de l'HTML):

Voici les differents types de tag qu'uilise ERB:
* Expression tags `<%= @name %>`
* Execution tags `<% 4.time do %>`...`<% end %>`
* Comment tags `<%# my comment %>`

`salut.html.erb`:
```erb
Hello world <%= mon code ERB %>
```

Toutes les vues créés vont avoir comme template `layouts/application.html.erb`, la vue va être injectée dans le 'yield'. (on peut mettre du css ici)


Donc ici on a créé une **Route** puis une **Action** et enfin une **Vue**.


On ajoute maintenant la route 'root' qui sera la racine de notre appli:

`routes.rb`:
```ruby
root to: 'pages#home'
```

Puis le controller:

`pages_controller.rb`:
```ruby
def home
end
```

Enfin la vue:

`views/pages/home.html.erb`:
```erb
bienvenue
```

Si on veut l'url `/salut/toto` il faut ajouter un parametre dans le `get`:

`routes.rb`:
```ruby
get '/salut/:name', to: 'pages#salut'
#ici, ":name" est un parametre 
```

Il faut que le controller recupere dans l'url le param (toto):

`pages_controller.rb`:
```ruby
	def salut
		# puts params.inspect #Permet d'afficher les param dans le terminal
		@name = params[:name].inspect #recupere le param toto
	end
```

Pour faire passer le param récupéré du controller à la vue, la vue a accès à tout ce qui a été défini comme propriété d'instance au niveau du controller. Donc la vue a accès à la variable d'instance `@name`

`salut.html.erb`:
```erb
Bonjour <%= @name %>
```

En cas de modification de l'url (`salut` devient `bonjour`), pour eviter de tout changer, on peut faire ceci:

On donne un nom à nos routes (des helpers)

`routes.rb`: 
```ruby
# affiche moi la page bonjour en utilisant la methode 'salut' du controller 'pages_controller.rb' en utilisant le helper 'salut'
get '/bonjour/:name', to: 'pages#salut', as: 'salut'
```

Dans `application.html.erb` on met le helper en question au lieu du chemin absolu de l'url soit:
```erb
href="<%= salut_path %>" # HELPER-NAME_path
href="<%= salut_path(name: 'toto') %>"  
href="<%= root_path%>"
```

On peut rendre également le paramètre `name` optionnel dans `routes.rb`:
```ruby
#--------<ROUTE>------,-----<ACTION>-----,--<NOM DE LA ROUTE (helper)
get '/bonjour(/:name)', to: 'pages#salut', as: 'salut'
```

## 1.3 Les migrations

Les migrations permettent de definir les modification à faire dans la BDD (ajout/suppr de champs, un pseudo git, ror utilise les numéros `schema_migration` pour reconstruire les tables dans le bon ordre de création)

Il faut generer la migration: `rails generate migration CreatePostsTable title:string content:text`

La migration est généré dans `db/migrate/<YYMMDDHHMMSS>_create_posts_table.rb`:
```ruby
class CreatePostsTable < ActiveRecord::Migration[5.0]
	def change
		create_table :posts do |t|
			t.string :title
			t.text :content
		end
	end
end
```

A chaque changement il faut faire un: `rails db:migrate`

Pour revenir en arriere il faut faire: `rails db:rollback`

pour renomer une colonne (ex: `title` => `name` et ajouter les dates de modification et d'ajout grâce à `timestamps`): `rails g migration RenamePostTitleToName`

Ceci créé `db/migrate/<YYMMDDHHMMSS>_rename_post_title_to_name.rb`, puis on change:
```ruby
class CreatePostsTable < ActiveRecord::Migration[5.0]
	def change
		change_table :posts do |t|
			t.rename :title, :name
			t.timestamps
		end
	end
end

enfin pour la MAJ on refait : `rails db:migrate`


## 1.4 Les models

pour creer un model il faut créér une classe dans `app/models/`.

`post.rb`:
```ruby
class Post < ApplicationRecord

end
```

Le mode console de rails permet de faire des tests: `rails console ou rails c`

On a acces à la classe Post en tapant: 'Post'

la methode find permet de recuperer un enregistrement en fonction de son ID:
```shell
Post.find(1) #exemple d'ID
#SELECT 'posts' .* FROM 'posts' WHERE 'posts' . 'id' = 1 LIMIT 1
```

Donc pour recuperer les info dans une variable:
```shell
p=Post.find(1)
p.name renvoie la variable récupéré dans la BDD
```

Si on modifie une valeur, il faut la persister dans la bdd (UPDATE): `p.save`

Pour supprimer de la bdd (DELETE): `p.destroy`

Pour créér un enregistrement (INSERT) et ne pas oublier de persister:
```shell
p= Post.new  OU Post.new(name: 'salut')
p.name = "salut"
p.save
```

Ou sinon en utilisant `create` (create créé et persiste):
```shell
p= Post.create(name: 'article 3', content: 'contenu du txt')
```

Pour changer plusieurs chanmps: `p.update(name: 'abc', content: 'abc')`

pour plus d'info il faut consulter la doc active records basics dans le site rails...

Recuperer le 1er enregistrement: `Post.first`

Recuperer le dernier enregistrement: `Post.last`

Recuperer le nombre d'enregistrement: `Post.count`

Recuperer toutes les articles: `Post.all`

Trier par noms et recuperer que le 1er enregistrement: `Post.order(:name).limit(1)`

Recuperer l'enregistrement tq `nom=salut` les updater en `bienvenue` (pour detruire `destroy_all` / `delete_all`):
```shell
Post.where(name: 'Salut').update_all(name: 'bienvenue')
```

Pour afficher les infos dans le site:

`routes.rb`:
```ruby
get '/articles', to: 'posts#index', as: 'posts'
```

on créé le controller:
```shell
#On créé un controller Posts avec l'action index
rails g controller Posts index 
```

`posts_controller.rb`:
```ruby
class PostsController < ApplicationController
	def index
		@posts = Post.all
	end
end
```

Puis créér la vue `index.html.erb`:
```erb
<%= @posts.inspect %>
<%= @posts.each do |post| %>

<%= end %>
```


## 1.5 Le CRUD


* **Create**, permet de créer un nouvel enregistrement, `POST: /{resources}`
* **Read**, permet d'afficher un ou plusieurs enregistrements, `GET: /{resources}` et `GET: /{resources}/:id`
* **Update**, permet de mettre à jour un enregistrement, `PUT: /{resources}/:id`
* **Destroy**, permet de supprimer un enregistrement, `DELETE: /{resources}/:id`


Pour la resource `:photo` voici les differents routes possible:

| **HTTP Verb** | **Path** | **Controller#Action** | **Used for** |
|-----------|------|-------------------|---------|
| GET | /photos | photos#index | display a list of all photos |
| GET | /photos/new | photos#new | return an HTML form for creating a new photo |
| POST | /photos | photos#create | create a new photo |
| GET | /photos/:id | photos#show | display a specific photo |
| GET | /photos/:id/edit | photos#edit | return an HTML form for editing a photo |
| PATCH/PUT | /photos/:id | photos#update | update a specific photo |
| DELETE | /photos/:id | photos#destroy | delete a specific photo |




Dans `routers.rb`, on peut creer tout un systeme de CRUD grâce à la methode `resources`:
```ruby
resources :posts
```

dans le terminal, on peut verifier nos routes:
```shell
rails routes
#(ex: post GET /posts/:id(.:format) posts#show)
```

puis dans notre view, on met un btn pour voir l'article suivant. Pour voir un article on met ce helper dans le `href`:

`index.html.erb`:
```shell
<h1>Articles</h1>
<% @posts.each do |post| %>
	<h2><%= post.name %></h2>
	<p><%= post.content %></p>
	<p>
		<a href="<%= post_path(post.id) %>" class="btn btn-primary">Lire la suite</a>
	<p>
<% end %>
```

`posts_controller.rb`:
```ruby
def show
	@post=Post.find(params[:id])
end

puis la vue de `show`:

`show.html.erb`:
```erb
<h1><%= @post.name %></h1>
<p><%= @post.content %></p>
<p>
	<a href="<%= posts_path %>" class="btn btn-primary">revenir aux articles</a> #voir `rails routes` pour les routes...
<p>
```

Pour editer, 

`posts_controller.rb`:
```ruby
def edit
	@post=Post.find(params[:id])
end
```

On peut generer des formulaires avec `form helpers`,

`edit.html.erb`:
```erb
<h1>Editer l'article</h1>
<%= form_for @post do |f| %>
	<div class="form-group">
		<label>Titre de l'article</label>
		<%= f.text_field :name, class: 'form-control' %>
	</div>
	<button type="submit">modifier l'article</button>
<% end %>
```

Avant d'update il faut utiliser la methode `require` qui permet de voir si la variable existe (retourne les variables) sinon return error et `permit` qui permet d'autoriser certains chanmps pour securiser l'update.

`posts_controller.rb`:
```ruby
def update
	@post=Post.find(params[:id])
	#on peut inspecter notre variable pour voir ce que l'on a
	#puts params.inspect
	post_params=params.require(:post).permit(:name, :content)
	@post.update(post_params)
	redirect_to posts_path
end
```

`index.html.erb`:
```erb
<a href="<%= edit_post_path(post.id) %>" class="btn btn-default">Editer</a>
```


Pour creer,

`index.html.erb`:
```erb
<a href="<%= new_post_path(post.id) %>" class="btn btn-default">creer</a>
```

`posts_controller.rb`:
```ruby
def new
# on créé une entité vide (car le nouvel article n'est pas persisté)
@post = Post.new
end
```

`new.html.erb`:
```erb
<h1>Creer un article</h1>
<%= form_for @post do |f| %>
	<div class="form-group">
		<label>Titre de l'article</label>
		<%= f.text_field :name, class: 'form-control' %>
	</div>
	<button type="submit">creer l'article</button>
<% end %>
```

`posts_controller.rb`:
```ruby
def create
	post=Post.create(post_params)
	redirect_to post_path(post.id)
end
private
def post_params
	params.require(:post).permit(:name,:content)
```


Pour supprimer,

`index.html.erb`:
```ruby
#RoR ajoute la lib JQuery_UJS qui permet d'ajouter des fonctions JS à travers l'attribut data
# data-confirm ajoute un popup js
# on peut poster notre lien avec une methode particuliere avec data-method, ici on l'utilise pour faire appel à DELETE
<a href="<%= post_path(post.id) %>" class="btn btn-default" data-confirm="etes-vous sur?" data-method="DELETE">supprimer</a>
```

`posts_controller.rb`:
```ruby
def destroy
	@post=Post.find(params[:id])
	@post.destroy
	redirect_to post_path
end
```


**Creation d'un systeme CRUD pour la gestion des categories.**

`rails g migration CreateCategories name:string slug:string`

la migration (la table) `db/migrate/<YYMMDDHHMMSS_create_categories.rb` est créé.

`rails db:migrate`

`rails g model Category --skip`

`rails g controller Categories index show update destroy new edit create`

`application.html.rb`:
```ruby
dans le navbar href="<%= categories_path %>"categorie
```

`routes.rb`:
```ruby
resources :categories
```

`categories_controller.rb`:
```ruby
def index 
	@categories = Category.all
end

def show
	@category=Category.find(params[:id])
end

def update
	@category=Category.find(params[:id])
	@category.update(category_params)
end

def destroy
	@category=Category.find(params[:id])
	@category.destroy
	redirect_to categories_path
end

def new
	@category=Category.new
end

def edit
	@category=Category.find(params[:id])
end

def create
	@category=Category.create(category_params)
	redirect_to category_path(@category.id)
end

private
def category_params
	params.require(:category).permit(:name,:slug)
end
```

`categories/index.html.erb`:
```erb
<h1>les categories</h1>
<%= @categories.each do |category| %>
<%= category.id %>
<%= category.name %>
<a href="<%= edit_category_path(category.id) %>" class"btn btn-primary">Editer</a>
<a href="<%= category_path(category.id) %>" class"btn btn-danger" data-confirm="sur?" data-method="delete">supprimer</a>
<% end %>
<a href="<%= new_category_path(category.id) %>" class"btn btn-primary">creer</a>
```

`new.html.erb`:
```erb
<h1>New categorie</h1>
<%= form_for @category do |f| %>
	<div class="form-group">
		<%= f.text_field :name, placeholder: 'Nom', class:'form-control' %>
	</div>
	<div class="form-group">
		<%= f.text_field :slug, placeholder: 'url', class:'form-control' %>
	</div>
	<div class="form-group">
		<button class="btn btn-primary">creer</button>
	</div>
<% end %>
```

`edit.html.erb`:
```erb
<h1>modif categorie</h1>
<%= form_for @category do |f| %>
	<div class="form-group">
		<%= f.text_field :name, placeholder: 'Nom', class:'form-control' %>
	</div>
	<div class="form-group">
		<%= f.text_field :slug, placeholder: 'url', class:'form-control' %>
	</div>
	<div class="form-group">
		<button class="btn btn-primary">modif</button>
	</div>
<% end %>
```

### la commande `scaffold`

Il existe une commande pour générer tout cela (ex: creer un CRUD pour `user`):
```shell
rails g scaffold User username:string bio:text
```

Cela crée la migration, les tests, le controller et les vues...

Puis il faut migrer: `rails db:migrate`

Pour annuler la migration: `rails db:rollback`

Pour annuler le scaffold: `rails d scaffold User username:string bio:txt`



# 2 CONTROLLERS

## 2.1 Controllers, Les filtres

Les filtres nous permettent d'effectuer des operation avant ou apres chaques actions:

* `before_action` permet d'effectuer une action avant
* `around_action` permet d'effectuer une action avant et apres
* `after_action` permet d'effectuer une action apres

ex:

`categories_controller.rb`:
```ruby
# quand on essaie d'acceder a une action qui correspond 
# au systeme de categorie, ce code sera executé avant l'execution d'une action tq show, index etc...
before_action do |controller|
	puts "je suis avant l'action"
end

#ou

around_action :around
private
def around
	puts "avant"
	yield
	puts "apres"
end
```

On peut utiliser ceci dans le `posts_controller.rb` par exemple.
Les methodes show, edit, update et destroy ont cette ligne en commun:
```ruby
@post = Post.find(params[:id])
```

Nous pouvons integrer cette ligne dans un `before_action`:
```ruby
#le only permet de specifier pour qui on doit utiliser before_action
before_action :set_post, only: [:update, :edit, :show, :destroy]

def set_post
	@post = Post.find(params[:id])
end
```

pour info, `scaffold` utilise `before_action`.

pour qu'un controller annule un `before_action` par exemple:
```ruby
skip_before_action :set_post
```


## 2.2 Controllers, Sessions et Cookies

les session se configure avec le fichier `config/initializers/session_store.rb` (cookie, cache, bdd ou encore redis...).

Ici le but est de définire une variable de session dans la page Article puis la recuperer dans la page Categorie:

`posts_controller.rb`:
```ruby
def index
	session[:user_id]=4
	@posts=Post.all
end
```

`categories_controller.rb`:
```ruby
def index
	@session=session[:user_id]
	@categories=Category.all
end
```

`index.html.erb`:
```erb
Session: <%= @session.inspect %>
```

Pour info, la clé de chiffrement des cookies se trouve dans `config/secrets.yml`

Pour supprimer une variable de session:
`session.delete(:user_id)`

### Le `flash`

Le flash permet de sauvegarder quelquechose en session puis de la supprimer à la prochaine requete.

exemple:

`posts_controller.rb`:
```ruby
def update
	flash[:notice]="article modifié"
end
```

`application.html.erb`:
```erb
<% if flash[:notice] %>
	<div class="alert alert-success"><%= flash[:notice] %></div>
<% end %>
```

On peut aussi ajouter le `flash` dans les `redirect_to`:
```ruby
redirect_to posts_path, flash: {success: "Article modifié avec succès"}
```

Pour afficher un message `flash` instantanément, (utiliser flash que pour la requete actuelle):
`posts_controller.rb`:
```ruby
def index
	flash.now[:success]="salut"
end
```

les sessions sont sauvegardées juste pendant la navigation de l'utilisateur, les cookies permettent de sauvegarder des information sous forme de fichier (si paramétré).

Pour créer un cookie:

`posts_controller.rb`:
```ruby
def index
	cookies[:username]= {
		value: "Jhon",
		expires: 1.month.from_now
	}
end
```

Pour sauvegarder des objets il faut utiliser la classe `JSON`:

`posts_controller.rb`:
```ruby
def index
	cookies[:username]= {
		value: JSON.generate("Jhon"),
		expires: 1.month.from_now
	}
end
```

pour recuperer l'objet:
```ruby
puts JSON.parse(cookies[:username]).inspect
```

Pour eviter que les utilisateur ne modifie les données, il faut utiliser des cookies signés:
`posts_controller.rb`:
```ruby
def index
	cookies.signed[:username]= {
		value: "Jhon",
		expires: 1.month.from_now
	}
end
```

Il est possible de chiffrer un cookie:
`posts_controller.rb`:
```ruby
def index
	cookies.encrypted[:username]= {
		value: "Jhon",
		expires: 1.month.from_now
	}
end
```

Pour laisser un cookie permanant:
`posts_controller.rb`:
```ruby
def index
	cookies.permanent[:username]= {
		value: "Jhon",
		expires: 1.month.from_now
	}
end
```

Pour supprimer une clé:
`posts_controller.rb`:
```ruby
def index
	cookies.delete(:username)
end
```



## 2.3 Controllers, Gerer plusieurs formats
