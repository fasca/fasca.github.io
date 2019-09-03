---
layout: post
title: fast memo RoR
date: 2019-09-01
tags:
  - backend
  - web
  - script
  - ruby
  - rails
description: cours sur RoR...
categories: Web
serie: Backend
published: true
---

- [Memo Github](#1)
- [PostgreSQL](#2)
- [Gems](#3)
- [Bundler](#4)
- [Ruby](#5)
- [ERB](#6)
- [Rails](#7)
- [dans la console rails](#8)
- [Les méthodes basiques d’Active Record](#9)
- [Validations](#10)
- [l'authentification avec la gem devise](#11)

---

## Memo Github <a id="1"></a>

[Mémo Github](https://github.com/geoffroymontel/notes/blob/master/postgresql.md)

Créer un répo et faire un commit :
```
git init
git add .
git commit -m "rails new"
```

### Hub
[**Hub**](https://github.com/github/hub) est un outil de ligne de commande qui enveloppe git afin de l'étendre avec des fonctionnalités et des commandes supplémentaires qui facilitent le travail avec GitHub.

Il permet de créer un répo directement sur GitHub :
```
hub create          // on crée le repo Github
git push origin master    // on push son travail dessus
hub browse        // on ouvre le repo dans son navigateur
```

---

## PostgreSQL <a id="2"></a>

[Mémo PostgreSQL](https://github.com/geoffroymontel/notes/blob/master/postgresql.md)

Demarrer postgresql :
```
lunchy start postgres
```

Voir les infos sur le postgresql installé :
```
brew info postgresql
```

Pour creer une BDD :
```
createdb
createdb -Ouser -Eutf8 emptyapp_dev
```

Pour se connecter au prompt de postgresql :
```
psql
```

Lister les databases :
```
\l
```

Se connecter à une database :
```
\connect dbName
```

Lister les tables :
```
\d
```

Afficher une table :
```
SELECT * FROM nomTable;
```

Afficher la structure d'une table :
```
\d nomTable
```

Pour quitter :
```
\q
```


### PgAdmin4

C'est le client "phpMyAdmin-like for MySQL" permettant de gérer une BDD postgresql.
Pour afficher les données d'une table dans PgAdmin4, il suffit de **right-clic** sur une table et cliquer sur **view**.

### Quelques commandes

```
db:create #creates the database for the current env
db:create:all #creates the databases for all envs
db:drop #drops the database for the current env
db:drop:all #drops the databases for all envs
db:migrate #runs migrations for the current env that have not run yet
db:migrate:up #runs one specific migration
db:migrate:down #rolls back one specific migration
db:migrate:status #shows current migration status
db:rollback #rolls back the last migration
db:forward #advances the current schema version to the next one
db:seed #(only) runs the db/seed.rb file
db:schema:load #loads the schema into the current env's database
db:schema:dump #dumps the current env's schema (and seems to create the db as well)

db:setup #runs db:schema:load, db:seed

db:reset #runs db:drop db:setup
db:migrate:redo #runs (db:migrate:down db:migrate:up) or (db:rollback db:migrate) depending on the specified migration
db:migrate:reset #runs db:drop db:create db:migrate
```

## Gems <a id="3"></a>

J'ai installé la gem lunchy permettant de lancer des services facilement. voir la page [github](https://github.com/eddiezane/lunchy) :
```
lunchy start postgres
```

## Bundler <a id="4"></a>

gérer les bibliothèques tierces et les versions de ces dernières en utilisant Bundler.

Bundler fournit un environnement cohérent pour les projets Ruby en suivant et en installant les gemmes exactes et les versions nécessaires.

Bundler est une sortie de l'enfer des dépendances, et garantit que les gemmes dont vous avez besoin sont présentes dans le développement, la mise en scène et la production. Le démarrage d'un projet est aussi simple que `bundle install`.

dans le gemfile, nous avons des gems à installer ex:
```
gem "cloudinary"
gem "attachinary"
gem "jquery-fileupload-rails"
gem "coffee-rails"
```

Pour installer tout cela il suffit de faire:
```
bundle install
```

---

## Ruby <a id="5"></a>

Executer du code ruby via le terminal :
```
irb
```

Lancer un script ruby :
```
ruby monScript.rb
```

---

## ERB <a id="6"></a>

pour mettre en commentaire une balise ERB:
```
<#%= render "shared/footer" %>
```

---

## Rails <a id="7"></a>

**A savoir :** il y a une console dans les pages d'erreurs Rails sur le navigateur, cela permet de tester les variables.

Les gems sont accessible via [RubyGems.org](https://rubygems.org/).

Lors de la création d'un nouveau projet Rails, l'option `-T` enlève les fichiers de tests lors de la génération :
```
rails _5.0.0.1_ new MY_APP -T --database=postgresql
cd MY_APP
rails db:create
#Puis créez un repo et faire un commit
git init
git add .
git commit -m "rails new"
```

Le template de wagon qui inclut une meilleure organisation du CSS et Bootstrap.
Ce template Rails se charge aussi de faire le rails db:create,
le git init et le premier commit. Vous pouvez donc
directement passer à l’étape de création du repo Github.
```
rails new \
  -T --database postgresql \
  -m https://raw.githubusercontent.com/lewagon/rails-templates/master/minimal.rb \
  MY_APP
hub create             // on crée le repo Github
git push origin master // on push son travail dessus
hub browse             // on ouvre le repo dans son navigateur
```

Pour lancer le serveur rails:
```
rails s
```

sous Cloud9:
```
rails s -b 0.0.0.0
```

voir sa page:
```
localhost:3000
```

voir sa page sous Cloud9:
```
https://rails-apps-VOTRE_USERNAME.c9users.io
```

Pour lancer la console rails:
```
rails console
```

Pour afficher les routes:
```
rails routes
```

Pour generer un nouveau controller (cela genere son dossier dans view, il faudra creer le fichier .erb):
```
rails g controller Products
```

Pour generer un nouveau model (Majuscule pour la 1ere lettre et au singulier c'est la convention):
```
rails g model Product title:string text:text
```

Ce générateur crée deux fichier :

    * Le modèle `product.rb` dans le dossier `app/models`
    * La migration `yyyymmddhhmmss_create_products` dans le dossier `db/migrate`

Le fichier de migration correspond aux instructions à lancer pour modifier le schéma de la base de données, ici pour créer une nouvelle table.

Puis generer la table de migration apres la generation du model:
```
rails db:migrate
```

Attention : si vous ne lancez pas la migration, la table n’existera pas dans la base de données et le modèle ne pourra donc pas s’y connecter.

On peut jouer avec le model, en lancant une console qui charge tout les modeles de votre app :

    * rails c
    * Product
    * Product.all

Vous avez parfois besoin de générer une migration, par exemple pour ajouter une colonne à une table existante. Pour cela, utilisez le générateur de migration de Rails :

```ruby
rails g migration AddRatingToProducts rating:integer
rails db:migrate # pour lancer la nouvelle migration
```

Notez bien la façon de nommer la migration qui respecte la convention CamelCase avec un `s` à `Products` car on parle ici de la table products à laquelle on veut ajouter une nouvelle colonne `rating` de type `integer`.


---

Pour envoyer un fichier texte depuis une action:
```
render plain: "hello"
```

Un controleur contient des actions (methodes),
Chaques controleurs possede un dossier avec son nom dans "VIEWS/",
chaques actions possede une page "nomAction.html.erb" dans "VIEWS/NomControleur/".

Rails va automatiquement chercher la bonne vue par rapport à l'action.

Il faut utiliser les variables d'instances dans le controleur puis les appeler dans la vue (@variable).

Les variables locales ne sont pas accecible depuis la vue.

---

##Les params dans Rails

Rails récupère tous les paramètres dans le hash "params".

### URL dynamique
Prenons un exemple :
```
# config/routes.rb
Rails.application.routes.draw do
  get "/say/:message" => "pages#speak"
end

# app/controllers/pages_controller.rb
class PagesController < ApplicationController
  def speak
    render plain: "I say: #{params[:message]}"
  end
end
```

Dans ce cas :

    http://localhost:3000/say/hello va renvoyer "I say: hello"
    http://localhost:3000/say/goodbye va renvoyer "I say: goodbye"
    Le paramètre dynamique de l’URL s’appelle ici message (l’équivalent du username sur Facebook ou de la city sur Airbnb)

AUTRE EXEMPLE URL DYNAMIQUE:
```
# config/routes.rb
Rails.application.routes.draw do
  get "/products/:id" => "products#show"
end

#app/controllers/products_controller.rb
class ProductsController < ApplicationController
  #CONST
  PRODUCTS = [
          {name: "basket-ball", category: "en equipe"},
          {name: "surf", category: "mer"},
          {name: "snowboard", category: "montagne"},
          {name: "ski", category: "montagne"},
          {name: "tir à l'arc", category: "tir"}
  ]
  def show
    #on recupere une valeur du tab CONST PRODUCTS via un index
    @product = PRODUCTS[params[:id].to_i]
  end
end
```

http://localhost:3000/products/0 renvoie dans show.html.erb
```
<%= @product[:name] %> ; <%= @product[:category] %>
```
soit "basketball ; en equipe"

_

### Query string
Prenons un autre exemple :
```
# config/routes.rb

Rails.application.routes.draw do
  get "/search" => "pages#search"
end

# app/controllers/pages_controller.rb
class PagesController < ApplicationController
  def search
    render plain: "Search for category #{params[:filter]}"
  end
end
```
    
http://localhost:3000/seach?filter=design va renvoyer "Search for category design"

http://localhost:3000/seach?filter=tech va renvoyer "Search for category tech"



AUTRE EXEMPLE QUERY STRING:
```
# config/routes.rb
Rails.application.routes.draw do
    get "/products" => "products#index"
end

#app/controllers/products_controller.rb
class ProductsController < ApplicationController
  #CONST
  PRODUCTS = [
          {name: "basket-ball", category: "en equipe"},
          {name: "surf", category: "mer"},
          {name: "snowboard", category: "montagne"},
          {name: "ski", category: "montagne"},
          {name: "tir à l'arc", category: "tir"}
  ]
  def index
    #Exemple de Query String, passer une var depuis l'url "?filter=paris"
    #Si dans ma requete j'ai ajouté un <PARAMS> ":filter", alors dans mon tab CONST PRODUCTS
    #je selectionne ceux qui dont la "category" correspond au param de l'url
    #sinon je prends tt le tab
    # Exemple d'url: "http://localhost:3000/products?filter=montagne"
    if params[:filter]
      @products = PRODUCTS.select {|product| product[:category] == params[:filter]}
    else
      @products = PRODUCTS
    end
  end
end
```
    
http://localhost:3000/products?filter=montagne va renvoyer "snowboard (montagne) et ski (montagne)"

---

## dans la console rails: <a id="8"></a>

pour creer du contenue exemple:
```
Product.create(name: "toto")
```

ex: dans le controler je recupere tt:
```
@products = Product.all
```

---

## Les méthodes basiques d’Active Record <a id="9"></a>

### All
La méthode "all" permet de récupérer toutes les entrée de la table:
```ruby
Product.all
#eq à SELECT * FROM products
```

### Count
Permet de compter le nombre d'entité
```ruby
Product.count
```

### First
Le premier produit de la base
```ruby
Product.first
```

### New, save, create
Pour créer un nouveau produit en base de données, vous pouvez le faire en deux étapes avec "new" et "save":
```ruby
var = Product.new(name: "toto", url: "toto.com")
var.save
# eq à INSERT INTO products (name, url) VALUES ('toto', 'toto.com')
```

Ou alors en un coup avec la méthode "create" :
```ruby
Product.create(name: "toto", url: "toto.com")
```

### Find
La méthode "find" permet de retrouver un produit dans la table étant donné son identifiant "id":
```ruby
Product.find(1)
# eq à SELECT * FROM products WHERE id = 1
```

### Find By
Dans la table Products, on recherche par noms:
```ruby
Product.find_by_name("toto")
# eq à SELECT * FROM products WHERE name = 'toto'
```

### Where
Dans la table Products, on cherche une "categorie == à params[:category]"
```ruby
Product.where(category: params[:category])
```

## Validations <a id="10"></a>
On peut ajouter des validations Active Record sur un modèle si l’on veut se protéger contre l’écriture de mauvaise données en base. Prenons un exemple :
```ruby
class Restaurant < ActiveRecord::Base
  validates :name, presence: true
  validates :address, presence: true, uniqueness: true
  validates :rating, inclusion: {in: [0, 1, 2, 3, 4, 5]}
end
```
Ici, on ne peut pas sauvegarder un produit en base si jamais :

    * Il n’a pas de nom ou d’adresse
    * Son adresse n’est pas unique (i.e. il y a déjà un produit avec la même adresse dans la DB)
    * Son rating n’est pas compris entre 0 et 5

Si on essaie de sauver un produit invalide (par exemple dans la console), Active Record va d’abord vérifier les validations et empêcher d’écrire en base si les validations ne passent pas :
```
rails c
> wrong = Restaurant.new(name: "Wrong restaurant", "1 wrong street", rating: 1000000)
> wrong.save # N'écrit pas en base de données et renvoie => false
```

### valid?
la methode `valid?` permet de tester la variable avant de la sauvegarder en BDD
Ici, nous avons rendu obligatoire le nom et l'url or la variable instantiée ne contient pas de nom :
```ruby
> kudoz = Product.new(url: “getkudoz.com”)
> kudoz.valid? # => false
> kudoz.save   # => false
> kudoz.name = “Kudoz”
> kudoz.valid? # => true
> kudoz.save   # => true
```

---

### Les 7 routes CRUD

Ces routes sont conventionnelles dans Rails. Il faut les connaître par coeur :
```ruby
get    "products"          => "products#index"
get    "products/:id"      => "products#show"
get    "products/new"      => "products#new"
post   "products"          => "products#create"
get    "products/:id/edit" => "products#edit"
patch  "products/:id"      => "products#update"
delete "products/:id"      => "products#destroy"
```

### Méthode de routing resources

On n’écrit jamais toutes les 7 routes CRUD à la main dans son fichier de routing `routes.rb`. A la place on utilise la méthode `resources`, qui génère exactement les mêmes routes:
```ruby
#config/routes.rb
resources :products
```

Vous pouvez vérifier que vos 7 routes sont toujours là dans la console avec :
```
rails routes
```

Vous pouvez aussi générer un sous-ensemble de ces 7 routes si vous ne les voulez pas toutes. Par exemple, pour générer uniquement les routes des actions de lecture :
```
resources :products, only: [:index, :show]
```

### Les helpers

Les helpers Rails sont des méthodes ruby qui vous aident à générer des URLs ou du HTML. Quand vous affichez vos routes avec :
```
rails routes
```

Vous avez un affichage qui ressemble à ça :
```
      Prefix Verb   URI Pattern                  Controller#Action
    products GET    /products(.:format)          products#index
             POST   /products(.:format)          products#create
 new_product GET    /products/new(.:format)      products#new
edit_product GET    /products/:id/edit(.:format) products#edit
     product GET    /products/:id(.:format)      products#show
             PATCH  /products/:id(.:format)      products#update
             PUT    /products/:id(.:format)      products#update
             DELETE /products/:id(.:format)      products#destroy
```

Ici la colonne `Prefix` sert à générer la colonne `URI`. Par exemple :
```
products_path             # => "/products"
new_product_path          # => "/products/new"

# kudoz = Product.find(23)
product_path(kudoz)       # => "/products/23"
edit_product_path(kudoz)  # => "/products/23/edit"
```

Vous pouvez ensuite combiner ces méthodes qui génèrent des URLs avec la méthode `link_to` qui génère une balise de lien `<a>`. Par exemple, le code ERB suivant :
```ruby
<!-- kudoz = Product.find(23) -->
<%= link_to kudoz.name, product_path(kudoz), class: "btn btn-warning" %>
<%= link_to "Ajouter un produit", new_product_path, class: "btn btn-primary" %>
```

va générer le HTML suivant :
```html
<a href="/products/23" class="btn btn-warning">Kudoz</a>
<a href="/products/new" class="btn btn-primary">Ajouter un produit</a>
```


---

pour les formulaires utiliser la gem 'simple_form'
La syntaxe `simple_form_for` pour générer un formulaire est la suivante (on considère ici que `@product = Product.new`) :
```ruby
<%= simple_form_for @product do |f| %>
  <%= f.input :name %>
  <%= f.input :tagline %>
  <%= f.button :submit %>
<% end %>
```
ou encore:
```ruby
<%= simple_form_for @product do |f| %>
        <%= f.input :name, placeholder: "kudoz", label: "quel produit?" %>
        <%= f.input :url, placeholder: "adresseweb.com", label: "quelle url?" %>
        <%= f.button :submit, "Ajouter", class: "btn btn-primary" %>
      <% end %>
```

pour debuger et faire un point d'arret pour voir les parametres etc sur le terminal, il faut utiliser la gem 'pry-byebug' puis inserer la 
ligne `binding-pry` ensuite tapez `exit` pour quitter le debug


### Strong `params`: filtrer ses paramètres
Rien n’empêche un utilisateur d’ajouter des champs dans un formulaire en éditant le HTML. Dans ce cas, la requête provient bien de notre site (elle a donc un `authenticity_token`) mais elle contient des infos supplémentaires qu’on n’a pas forcément envie d’enregistrer en base.
Heureusement, Rails permet d’appliquer un **filtre** aux paramètres dans le controller. Dans le schéma ci-dessus, ce filtre n’autorise que les champs `name` et `tagline`. **Du coup le champ `review` passe à la trappe**. C’est vous qui choisissez les paramètres que vous laissez passer dans vos controller.
```ruby
class ProductsController < ApplicationController
  def new
    @product = Product.new
  end
  def create
    @product = Product.new(product_params)
    if @product.save
      redirect_to products_path
    else
      render :new
    end
  end

  private
  def product_params
  #require permet de garder que ce que contient product
    params.require(:product).permit(:name, :url, :tagline)
  end
end
```

Pour rediriger vers une page apres une sauvegarde d'un formulaire en post par exemple:
```
redirect_to <un_helper>
```

---

### Validations et `Seed`

Une Seed est un fichier ruby qui permet de peupler la BDD de données d'exemple, utile lors du développement. Il est present dans `db/seeds.rb`. Il permet d'ecrire un scenario en base.
```ruby
#Detruire tout ce qui est en base
Product.destroy_all
User.destroy_all

vegeta = User.create!(email: "vegeta@vegeta.com", password: "vegetavegeta")
jiren = User.create!(email: "jiren@jiren.com", password: "jirenjiren")

#puis on créé des seed, le "!" permet de lever une exception si la seed ne passe pas a cause d'une validation par exemple
Product.create!(user: jiren, name: "Kudoz", url: "http://www.site.com", tagline: "tinder for job search", category: "tech")
Product.create!(user: jiren, name: "kamehameha", url: "http://www.kamehouse.com", tagline: "atk of goku", category: "education")
Product.create!(user: vegeta, name: "shumpo", url: "http://www.fly.com", tagline: "fast run", category: "design")
```

Pour executer la seed taper dans le terminal `rails db:seed` puis le code sera executé (effacement et creation de la seed)

Il est aussi possible de faire du scraping puis alimenter le bdd avec ce qu'on a récupéré.

### sauver les données écrit sur les champs même si la page est rechargé

Il suffit d'utiliser `render` puis appeler le template `new`, les donnes sont
déja implémenté dans l'attribut `@product` precedement:
```ruby
def create
    @product = Product.new(product_params)
    #si il a respecté les champs obligatoires on save et on redirige sur la page des produits
    if @product.save
      redirect_to products_path
    else
      #sinon renvoie le template "new" avec ce que l'user a écrit
      #vu que l'attribut @product a été déja instancié alors les données sont toujours présentes
      render :new
    end
  end
```

---

Remarquons ici que les URLs des actions "show" et "destroy" sont les mêmes :

Prefix    Verb    URI Pattern    Controller#Action
product   GET     /products/:id  products#show
          DELETE  /products/:id  products#destroy

C’est bien pour ça qu’on a une seule méthode product_path pour générer l’URL /products/:id. Si on veut un lien qui fait bien une requête DELETE (et non une requête GET) dans nos templates, on doit ajouter l’option `method: :delete` lorsqu’on appelle la méthode `link_to`. Regardez bien la différence entre les deux liens suivants :
```
<%= link_to "Aller voir le produit", product_path(@product) %>
<%= link_to "Supprimer le produit", product_path(@product), method: :delete %>
```

    Le premier lien fait une requête GET sur l’URL product_path(@product), c’est donc un lien classique vers la page show qui détaille du produit.
    Le second lien fait une requête DELETE sur la même URL. D’après notre routing, cette requête va être traitée par l’action destroy qui va supprimer le produit de la base de données.

---


### Filtre `before_action` dans son controller

Dans beaucoup d’action on a besoin d’aller chercher le produit à partir de l’`:id` récupéré dans l’URL :
```ruby
class ProductsController < ApplicationController
  def show
    @product = Product.find(params[:id])
    # ...
  end
  def edit
    @product = Product.find(params[:id])
    # ...
  end
  def update
    @product = Product.find(params[:id])
    # ...
  end
  def destroy
    @product = Product.find(params[:id])
    # ...
  end
end
```

Pour ne pas répéter le code `@product = Product.find(params[:id])` on peut le mettre dans une méthode privée `find_product` qui sera appelé avant les actions qui en ont besoin grâce au filtre Rails `before_action`:
```ruby
class ProductsController < ApplicationController
  before_action :find_product, only: [:show, :edit, :update, :destroy]
  def show
    # ...
  end
  def edit
    # ...
  end
  def update
    # ...
  end
  def destroy
    # ...
  end
  private
  def find_product
    @product = Product.find(params[:id])
  end
end
```

----


### Factoriser ses formulaires avec une partielle ERB

On a exactement le même code pour le formulaire `simple_form` dans les templates `new.html.erb` et `edit.html.erb`.
```ruby
<%= simple_form_for @product do |f| %>
  <%= f.input :name %>
  <%= f.input :url %>
  <%= f.input :tagline %>
  <%= f.button :submit %>
<% end %>
```

C’est un peu idiot car si on veut enrichir ce formulaire (par exemple en ajoutant un `input`), on devra le faire à deux endroits. Heureusement, ERB nous permet de définir des vues **partielles** qui sont des fichiers ERB qui commence par un _ et qu’on peut injecter dans d’autres templates. Ici ça donne :
```ruby
<!-- products/new.html.erb -->
<h1>Créer un produit</h1>
<%= render "form" %>
```
```ruby
<!-- products/edit.html.erb -->
<h1>Editer le produit</h1>
<%= render "form" %>
```
```ruby
<!-- products/_form.html.erb -->
<%= simple_form_for @product do |f| %>
  <%= f.input :name %>
  <%= f.input :url %>
  <%= f.input :tagline %>
  <%= f.button :submit %>
<% end %>
```

On a mis le code du formulaire à un seul endroit, **dans la partielle ERB** `_form.html.erb` qui est ensuite appelée dans les deux templates `new.html.erb` et `edit.html.erb` grâce à la méthode `render`.


----

les images doivent etre placé dans `app/assets/images`

Pour ingecter avec ERB l'url d'une image avec `image_path` :
```ruby
<%= image_path NomImage.jpg %>
#exemple:
<div class="banner" style="background-image: linear-gradient(-225deg, rgba(0,101,168,0.6) 0%, rgba(0,36,61,0.6) 50%), url('<%= image_path "banner-home.jpg" %>');">
```

Pour generer une image avec ERB on utilise `image_tag` ceci genere l'url et la balise `<img>`:
```ruby
<%= image_tag monImage.png %>
```

Le CSS se trouve dans `app/assets/stylesheets`.
Pour la page Home nous allons ajouter un composant CSS soit une partial sass dans `app/assets/stylesheets/components`.
Il suffit de créér un fichier `_banner.scss` dans le dossier en question puis importer la partial dans le fichier `_index.scss` du même repertoire qui fait office de "main principal" comme ceci `@import "banner";`.

### Le layout de l’application

Depuis le début de cette track, on ne code jamais le squelette HTML de nos pages lorsqu’on ajoute des templates (comme `show.html.erb`, `index.html.erb`, `edit.html.erb`, etc..). En effet, tous ces templates s’injectent dans un fichier bien particulier `layout/application.html.erb` qu’on appelle **le layout**.

**Le layout est la structure commune partagée par toutes les pages de notre site** et ressemble à ça :
```ruby
<!-- layout/application.html.erb -->
<html>
  <head>
    <!-- le contenu du head -->
  </head>
  <body>
    <!-- le code de la navbar -->
    <%= yield %>
    <!-- le code du footer -->
  </body>
</html>
```

Le contenu de chaque template (`show.html.erb`, `index.html.erb`, `edit.html.erb`, etc..) **va venir s’injecter dans le layout au niveau du mot-clef **yield**.

### Partielles partagées

Pour éviter de “noyer son layout” avec 50 lignes de code pour sa navbar, 30 lignes de code pour son footer, 30 lignes pour ses scripts d’analytics (Google Analytics ou autre), une bonne pratique consiste à écrire ces différents codes dans des partielles ERB. Voici ce que ça donne :
```ruby
<!-- layout/application.html.erb -->
<html>
  <head>
    <!-- le contenu du head -->
  </head>
  <body>
    <%= render "shared/navbar" %>
    <%= yield %>
    <%= render "shared/footer" %>
    <%= render "shared/analytics" %>
  </body>
</html>
```

Ensuite, vous devez créer un dossier `shared` dans votre dossier `views`, et y mettre vos différentes partielles ERB :
```ruby
<!-- shared/_navbar.html.erb -->
<div class="navbar">
  <!-- etc.. -->
</div>
```

```ruby
<!-- shared/_footer.html.erb -->
<div class="footer">
  <!-- etc.. -->
</div>
```

```ruby
<!-- shared/_analytics.html.erb -->
<script>
  <!-- Votre code de tracking Google Analytics ou autre (pixel facebook, code Mixpanel, etc..) -->
</script>
```

---

## l'authentification avec la gem devise <a id="11"></a>

Pour ajouter une gem il suffit de la rajouter dans le fichier Gemfile, exemple ici la gem Devise pour l'authentification. En generale, la commande "budne install" est suffisante mais dans la doc de "Devise" il existe des commandes specifiques pour installer les fichiers ruby necessaires et generer la BDD User compatible avec "Devise":
```
# dans le fichier Gemfile:
gem 'devise', '4.0.0.rc2'

#dans le terminal, on lance l'installation:
bundle install
rails generate devise:install

#pour generer le model "User"
rails generate devise user
rails db:migrate
```


### Routes

Lancez un rails routes en ligne de commande pour voir les nouvelles routes installées.
Ce qui nous intéresse, ce sont les trois suivantes :
```
new_user_registration GET    /users/sign_up(.:format)       devise/registrations#new
     new_user_session GET    /users/sign_in(.:format)       devise/sessions#new
 destroy_user_session DELETE /users/sign_out(.:format)      devise/sessions#destroy
```
Ainsi, vous pouvez aller sur "localhost:3000/users/sign_up" pour vous créer un compte puis
sur "localhost:3000/users/sign_in" pour vous connecter.

### Côté vue

Un helper bien utile va vous permettre de modifier votre barre de navigation afin de la rendre plus intelligente, c’est-à-dire qu’elle va afficher de l’information conditionnelement au fait qu’un utilisateur est connecté ou non. Ce helper est :
```
user_signed_in?
```

Pour rendre les messages flash plus jolis, n’hésitez pas à utiliser ce gist

Pour modifier les écrans de Sign in et Sign up par défaut de Devise (qui sont très “bruts de décoffrage”…), il faut d’abord importer ces vues dans notre propre projet par la commande :
```
rails generate devise:views
```

pour avoir un message flash "vous etes co/déco" sur le layout, apres la navbar par exemple:
```
#app/views/layouts/application.html.erb
<p class="notice"><%= notice %></p>
<p class="notice"><%= alert %></p>
```

### Côté controlleur

La politique la plus safe à utiliser est celle de la liste blanche. Par défaut, on interdit l’accès à toutes les pages pour les utilisateurs non connectés, et on ouvre certains accès uniquement.

Cela se passe dans le fichier `app/controllers/application.controller.rb` en ajoutant la ligne :
```
# app/controllers/application_controller.rb
class ApplicationController < ActionController::Base
  # [...]
  before_action :authenticate_user!
end
```

Maintenant, dans certains controlleurs, on peut décider que certaines actions soient accessibles pour un utilisateur non connecté. Par exemple, si on souhaite que la route `/about`, gérée par `PagesController#about`, on aura :
```
# app/controllers/pages_controller.rb
class PagesController < ApplicationController
  skip_before_action :authenticate_user!, only: [ :about ]

  # [...]
end
```

Le `only:` est là pour préciser un Array d’actions sur lesquelles le `skip_before_action` s’applique. Si il n’y a pas de `only:`, alors le `skip_before_action` s’applique à toutes les actions du controlleur.

### Impact sur le schéma user_id dans products

Pour l’instant, un produit est créé sans être relié à un utilisateur en particulier. Nous voulons donc conserver en base de données une trace du créateur du produit. Pour cela nous allons ajouter une clé 
étrangère `user_id` dans la table "products"

Pour ajouter cette colonne, on va générer la migration suivante :
```
rails generate migration AddUserToProducts user:references
```

Vérifiez la migration automatiquement générée qui devrait comporter la ligne :
```
add_reference :products, :user, foreign_key: true
```

que vous pouvez ensuite jouer avec la commande habituelle :
```
rails db:migrate
```

N’oubliez pas de mettre à jour vos deux modèles :
```
# app/models/product.rb
class Product < ApplicationRecord
  belongs_to :user

  # [...]
end


# app/models/user.rb
class User < ApplicationRecord
  has_many :products

  # [...]
end
```

### Côté controlleur

Au niveau du contrôlleur, on va utiliser le helper de Devise `current_user` pour associer automatiquement le produit nouvellement créé avec l’utilisateur actuellement connecté:
```
# app/controllers/products_controller.rb
class ProductsController
  # [...]
  def create
    @product = Product.new(product_params)
    @product.user = current_user
    # [...]
  end
end
```

---

pour configurer les gems, les options etc aller dans "config/initializers/nomGem"

ajout d'une clé étrangere
rails g migration AddUserToProducts user:references

---
Pour afficher toutes les erreurs lors du dev:
```ruby
#dans un fichier.html.erb
<%= @product.errors.full_messages %>
```


---

### Gem rails_admin

Pour faire simple, RailsAdmin est clé en main, il n’y a rien à faire (à part le protéger bien sûr derrière un login admin!) et tous les modèles. C’est souvent celui-là que j’utilise quand je veux aller vide et qu’il n’y a que moi qui y ait accès.

Si je veux donner un back-office à un client, je vais me pencher sur **ActiveAdmin** car il a une logique de n’exposer que des modèles spécifiques. Ainsi on ne noie pas le client dans une multitudes de tables.

Il faut protéger Rails Admin à des gens qui ne sont qu’admin en fait. Le plus simple:

1. Générer une migration sur User
```
rails g migration AddAdminToUsers admin:boolean
rails db:migrate
```

2. Protéger la route de Rails Admin
```ruby
# in config/initializer/rails_admin.rb

RailsAdmin.config do |config|
  config.authorize_with do |controller|
    redirect_to main_app.root_path unless current_user && current_user.admin
  end

  # [...]
end
```

3. Passer un utilisateur admin
```
rails c
irb> user = User.find_by_email('leboss@laboite.com')
irb> user.admin = true
irb> user.save
```

C’est le setup standard de Rails Admin qu’on conseille aux élèves du wagon. ça nécessite bien entendu d’avoir Devise installé auparavant.

Ensuite pour gérer plus finement les permissions, plutôt que de parsemer les contrôleurs et les vues de if, on utilise des gems d’autorisations comme `cancancan` ou `pundit`.

---

mettre les lignes pour Cloudinary, Figaro et Attachinary
