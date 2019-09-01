---
layout: post
title: trainvag cours RoR
date: 2019-09-01
tags:
  - backend
  - developpement
description: cours sur RoR...
categories: developpement backend
serie: programmation
published: true
---

**Sommaire**

- [Le Design Pattern MVC](#1)
- [Démarrer un projet Rails](#2)
- [Le template du Wagon](#3)
- [Les requêtes HTTP](#4)
- [Vos premières routes](#5)
- [Convention Action/Vue et ERB](#6)
- [Les paramètres d’une requête HTTP](#7)
- [Paramètres dans l’URL](#8)
- [Nous partageons tous des URLs](#9)
- [A quoi sert Active Record ?](#10)
- [La convention de nommage](#11)
- [Générateurs de modèle / migration](#12)
- [La console Rails](#13)
- [Les méthodes basiques d’Active Record](#14)
- [Les actions CRUD](#15)
- [Les 7 routes CRUD](#16)
- [Création et modification](#17)
- [Méthode de routing resources](#18)
- [Les helpers](#19)
- [Actions `new` et `create`](#20)
- [Formulaire HTML natif](#21)
- [Strong `params`: filtrer ses paramètres](#22)
- [Finissons le `new` et `create`](#23)
- [Validations et `Seed`](#24)
- [sauver les données écrit sur les champs même si la page est rechargé](#25)
- [Les actions `edit` et `update`](#26)
- [`simple_form_for` est malin comme un singe !](#27)
- [L’action `update`](#28)
- [L’action `destroy`](#29)
- [“Refacto” de son code](#30)
- [Filtre `before_action` dans son controller](#31)
- [Factoriser ses formulaires avec une partielle ERB](#32)
- [Emmet](#33)
- [Color Picker](#34)
- [Color Highlighter](#35)
- [Le layout de l’application](#36)
- [Partielles partagées](#37)
- [Raisonner par composant web](#38)
- [Eplacement des images](#39)
- [Travailler sur une nouvelle user story](#40)
- [Prise en main Heroku](#41)
- [Installation](#42)
- [Connexion via le terminal](#43)
- [Création d’une application](#44)
- [Déploiement](#45)
- [Logs](#46)
- [Rails console](#47)
- [Prix](#48)
- [Utilisateurs et système d'authentification](#49)
- [Devise](#50)
- [Installation](#51)
- [Routes](#52)
- [Côté vue](#53)
- [Côté controlleur](#54)
- [Impact sur le schéma](#55)
- [Côté controlleur](#56)
- [Exercice](#57)
- [Coté Back Office](#58)
- [Cloudinary](#59)
- [Installation dans Rails](#60)
- [Configuration](#61)
- [Upload d’une image en console](#62)
- [Affichage de l’image dans une page statique](#63)
- [Upload d’image par l’utilisateur avec `attachinary`](#64)
- [Mise en production](#65)
- [Fonctionnalité d'upvote sur un produit](#66)
- [Vue (d’où part la requête AJAX)](#67)
- [Contrôleur](#68)
- [Vue (de réponse AJAX)](#69)
- [Resources](#70)

---

## COURS N3

Utilisation d'une API

Permet de lire du JSON:
`require "json"`

Faire des requetes HTTP en Ruby:
`require "open-uri"`

Ex :

```ruby
url = "https://api.site.com"
headers = {
  "Authorization" => "TOKEN"
}

posts = JSON.parse(open("url, headers).read)
```

## COURS N4

Fichier :
`ma_classe.rb`

Nom d'une classe :
`MaClasse`

Variable :
`blue_car=`


Dans irb pour charger une classe, exemple `car.rb`:

`require_relative "car"`

puis la classe est chargée (`Car.class => #Class`)


## COURS N5

### Le Design Pattern MVC <a id="1"></a>

Voici un exemple de "TODOLIST" en ligne de commande.
* Model
* Vu
* Controller
* Router : aiguille le choix de l'utilisateur vers la bonne méthode du controller

***app.rb :***

```ruby
require_relative "router"

router = Router.new
router.start
```

***controller.rb :***

```ruby
require_relative "task"
require_relative "view"

class Controller
  # 1 intention utilisateur => 1 méthode d'instance
  #
  # - Afficher les tâches
  # - Ajouter une tâche
  # - Marquer une tâche comme réalisée
  # - ...

  def initialize
    @tasks = []
    @view = View.new
  end

  def list
    @view.print_tasks(@tasks)
  end

  def add
    # 1. Demander au user description de la tache
    description = @view.ask_user_for_description
    # 2. Creer la nouvelle tâche
    task = Task.new(description)
    # 3. Stocker la nouvelle tâche
    @tasks << task
  end

  def mark_as_done
    # 1. Demander au user l'id de la tache
    id = @view.ask_user_for_id
    # 2. Chercher la Task de l'id demandé
    task = @tasks[id]
    # 3. Marker la tache comme faite
    task.mark_as_done
  end
end
```

***router.rb :***

```ruby
require_relative "controller"

class Router
  def initialize
    @controller = Controller.new
  end

  def start
    loop do
      # Qu'est-ce que tu veux faire ?
      puts "----------------------------"
      puts "What do you want to do next?"
      puts "1 - List tasks"
      puts "2 - Add a task"
      puts "3 - Mark task as done"
      puts "----------------------------"
      action = gets.chomp.to_i

      if action == 1
        @controller.list
      elsif action == 2
        @controller.add
      elsif action == 3
        @controller.mark_as_done
      else
        puts "Wrong choice"
      end
    end
  end
end
```

***task.rb :***

```ruby
class Task
  attr_reader :description

  def initialize(description)
    @description = description    # String
    @done = false                 # true / false
  end

  def done?
    return @done
  end

  def mark_as_done
    @done = true
  end
end
```

***test_scenario.rb :***

```ruby
require_relative "controller"

controller = Controller.new


# 1. Ajoute une tache
# 2. Ajoute une tache
# 3. Affiche une tache

controller.add
controller.add
controller.list
controller.mark_as_done
controller.list
```

***view.rb :***

```ruby
# Role: gets / puts

class View
  def print_tasks(tasks)  # Array<Task>
    tasks.each_with_index do |task, index|
      if task.done?
        marker = "[x]"
      else
        marker = "[ ]"
      end
      puts "#{index + 1}. #{marker} #{task.description}"
    end
  end

  def ask_user_for_description
    puts "Description?"
    print "> "
    description = gets.chomp
    return description
  end

  def ask_user_for_id
    puts "Index?"
    print "> "
    id = gets.chomp.to_i
    return id - 1
  end
end
```

## COURS N6

Quand on crée une appli

1. faire le mockup (si vous cherchez de l’inspiration en UI, vous pouvez consulter des sites comme [collectUI](http://collectui.com))
2. dessiner le schéma de la BDD
3. faire les user stories (pour la gestion de projet, sur trello par exemple faire du kanban)

Exemple, pour les user stories, faire 4 colonnes :

| **Backlog** | **Ready** | **In progress** | **Done** |
|-------------|-----------|-----------------|----------|
| As a visitor, i can sign up | | | |
| As a visitor, i can see all product | | | |
| As a user, i can post product| | | |


## COURS N7


HTTP Request --> ROUTER (config/routes.rb) --> CONTROLLER (app/controllers) <--> MODEL (app/models) <--> BDD
CONTROLLER --> VIEW (app/views) ==> USER

### Démarrer un projet Rails <a id="2"></a>

On démarre toujours un projet Rails de la même façon. On crée l’application Rails avec `Rails new <APP_NAME> <-T without_files_test> <--database=postgresql>`, on se déplace à l’intérieur, on crée la base de données associée et on ouvre le projet avec Sublime Text :

```shell
rails _5.0.0.1_ new MY_APP -T --database=postgresql
cd MY_APP
rails db:create
stt
```

```shell
/
|_ app
|   |__ controllers
|   |__ models
|   |__ views
|_ config
    |__ routes.rb
```

Pour lancer le serveur web, ouvrez un autre onglet du terminal, et lancez la commande puis allez sur `http://localhost:3000` :

```shell
rails server
# ou
rails s
```

Puis on versionne avec git dès le départ :

```shell
git init
git add .
git commit -m "rails new"
```

Enfin on crée le repository associé (on dit “dépôt” en français) sur Github et on push son travail dessus. Pour cela, on utilise le petit utilitaire [hub](https://github.com/github/hub) qui permet de créer des projets Github depuis son terminal quand on est paresseux :

```shell
hub create             // on crée le repo Github
git push origin master // on push son travail dessus
hub browse             // on ouvre le repo dans son navigateur
```

### Le template du vagon <a id="3"></a>

Le problème de `rails new`, c’est que ça vous génère un projet :

* Dans lequel Bootstrap n’est pas installé.
* Qui n’a pas une bonne organisation par défaut des fichiers CSS.

C’est pour ça qu’on va utiliser le template du vagon, que vous pouvez retrouver sur ce repo [Github](https://github.com/lewagon/rails-templates). Pour créer un projet, rien de plus simple :

```shell
rails new \
  -T --database postgresql \
  -m https://raw.githubusercontent.com/lewagon/rails-templates/master/minimal.rb \
  MY_APP
```

Ce template Rails se charge aussi de faire le `rails db:create`, le `git init` et le premier commit. Vous pouvez donc directement passer à l’étape de création du repo Github.

## COURS N8

Les headers http : [Developer.Mozilla.org](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)


### Les requêtes HTTP <a id="4"></a>

Une requête HTTP a quatre parties :

    * Un verbe HTTP (GET / POST / PATCH / DELETE)
    * Une URL (la partie visible dans la barre de navigation)
    * Des headers
    * Un body dans le cas d’une requête POST / PATCH (une requête GET n’a pas de body)

Pour voir ce que vos requêtes HTTP ont dans le ventre quand vous navigez sur un site, ouvrez l’onglet Network de votre Chrome :

Vous pouvez consulter la liste de tous les headers HTTP :

    * `Accept` permet par exemple de définir le type de fichier que votre client accepte en réponse du serveur.
    * `Referer` correspond au site sur lequel vous vous trouvez quand vous faites la requête.

Par exemple, ici :

    * On fait une requête **GET** `http://www.levagon.com`.
    * Le referer est bien `http://www.google.fr`, puisqu’on a fait cette requête depuis Google.
    * Le referer de la requête est récupéré par les solution d’analytics (comme Google Analytics, Mixpanel) pour vous permettre d’analyser les sources de traffic sur votre site.

### Vos premières routes <a id="5"></a>

Le fichier `routes.rb` est le point d’entrée des requêtes qui arrivent à votre site Rails. Chaque route dirige une requête vers une méthode ruby définie dans un **controller**, qu’on appelle aussi une **action**. Par exemple, ce routing :

```ruby
# config/routes.rb
Rails.application.routes.draw do
  root to: 'pages#home'
  get "/team" => "pages#team"
  get "/contact" => "pages#join_us"
end
```

Va diriger les trois requêtes (GET /, GET /team, GET /contact) vers :

```ruby
# app/controllers/pages_controller.rb
class PagesController < ApplicationController
  def home
    # ...
  end
  def team
    #variable d'instance
    @time=Time.now  #ensuite utiliser la var d'instance dans la vue
  end
  def join_us
    # ...
  end
end
```

N’oubliez pas, pour générer un nouveau controller (ex : `ProductsController`), vous avez la commande :

`rails g controller products`

Et pour afficher vos routes (à faire plusieurs fois par jour):

`rails routes`

### Convention Action/Vue et ERB <a id="6"></a>

#### La convention Action/Vue :

Une fois qu’une requête est routée vers une action d’un controller, l’action doit renvoyer un template. Comment sait-elle quel template renvoyer ? Grâce à la convention Action/Vue :

    * Le controller `PagesController` cherche les templates dans le dossier `views/pages` (nommé comme lui).
    * L’action `PagesController#home` chercher le template `views/pages/home.html.erb` qui a le même nom qu’elle.


#### ERB

Les templates **ERB** permettent d’injecter du ruby dans du HTML. Cela dit, il ne s’agit pas d’écrire trop de “code ruby” dedans. Si vous codez proprement, c’est le controller qui doit récupérer des informations, les stocker dans des variables d’instance (qui commencent par un `@`) pour ensuite les injecter dans le template **ERB**. Comme dans cet exemple :


```ruby
# app/controllers/pages_controller.rb
class PagesController < ApplicationController
  def home
    @tagline = "Tinder for job search"
  end
end
```

et ensuite dans le template associé :

```ruby
<!-- app/views/pages/home.html.erb -->

<h1>Kudoz</h1>
<h2>
  <%= @tagline %>
</h2>
```


## COURS N9

### Les paramètres d’une requête HTTP <a id="7"></a>

Il y a deux façon de communiquer des paramètres dans une requêtes HTTP :

    * directement dans l’URL (dans le cas d’une requête GET)
    * dans le corps de la requête (dans le cas d’une requête POST)

### Paramètres dans l’URL <a id="8"></a>

#### URL interprétée

Une application web est capable d’interpréter certaines parties de l’URL comme étant des valeurs de paramètres :

    * `http://facebook.com/jeandupont` : Facebook va interpréter `jeandupond` comme étant la valeur d’un paramètre "username"
    * `http://airbnb.com/s/istanbul` : Airbnb va interpréter `istanbul` comme étant la valeur d’un paramètre "city"

#### Query string

On peut aussi passer des paramètres dans l’URL de façon explicite après un `?`, par exemple :

    * Dans l’URL `https://www.airbnb.fr/s/istanbul?checkin=31/03/2016&checkout=15/04/2016`
    * La partie après le `?` (c’est-à-dire `checkin=31/03/2016&checkout=15/04/2016`) s’appelle une **query string**.
    * On peut y lire directement le nom des paramètres ("checkin" et "checkout") et leur valeur (`31/03/2016` et `15/04/2016`).
    * Les différents paramètres (clef=valeur) sont séparés par un `&`.

### Nous partageons tous des URLs <a id="9"></a>

Dans la vraie vie, nous partageons tous des URLs. Avoir des paramètres dans l’URL est donc très pratique, notamment pour toutes les pages de recherche.

#### Paramètres dans le body

Quand on remplit un formulaire pour créer une nouvelle entrée en base de données (nouvel utilisateur, nouveau post/tweet/produit/appartement/etc..), on fait une requête de type POST. Dans ce cas, on passe les paramètres dans le corps de la requête (i.e. le body), ce que l’inspecteur Google Chrome appelle "Form Data" :

**Les params dans Rails**

Rails récupère tous les paramètres dans le hash `params`.

**URL dynamique**

Prenons un exemple :

```ruby
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

    * `http://localhost:3000/say/hello` va renvoyer "I say: hello"
    * `http://localhost:3000/say/goodbye` va renvoyer "I say: goodbye"
    * Le paramètre dynamique de l’URL s’appelle ici message (l’équivalent du "username" sur Facebook ou de la "city" sur Airbnb)

**Query string**

Prenons un autre exemple :

```ruby
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

Dans ce cas :

    * `http://localhost:3000/seach?filter=design` va renvoyer "Search for category design"
    * `http://localhost:3000/seach?filter=tech` va renvoyer "Search for category tech"


## COURS N10

### A quoi sert Active Record ? <a id="10"></a>

Active Record est un ORM (mapping objet-relationnel), c’est la librairie ruby qui permet de se connecter à la base de données pour pouvoir lire/écrire dedans de façon très simple avec des méthodes ruby (à la place de requêtes SQL).

**Model** (app/models) <---ActiveRecord---> PostgreSQL

### La convention de nommage <a id="11"></a>

Chaque table de la base de données est reliée à un modèle ActiveRecord, c’est-à-dire une classe ruby qui hérite de ActiveRecord.

Comment se fait ce lien entre table et modèle ? Simplement grâce à une convention de nommage :

table: *products* <---ActiveRecord naming convention---> model: *Product*

    * La table s’écrit en minuscule / pluriel
    * Le modèle s’écrit en majuscule / singulier

Si vous respectez cette convention, votre modèle est connecté comme par magie à la table et vous pouvez donc l’utiliser pour lire ou écrire dans cette table.

### Générateurs de modèle / migration <a id="12"></a>

#### Modèle

Pour générer un modèle dans Rails (par exemple un modèle `Restaurant` pour changer) :

```ruby
rails g model Restaurant name:string address:string
```

Ce générateur crée deux fichier :

    * Le modèle `restaurant.rb` dans le dossier `app/models`
    * La migration `yyyymmddhhmmss_create_restaurants` dans le dossier `db/migrate`

Le fichier de migration correspond aux instructions à lancer pour modifier le schéma de la base de données, ici pour créer une nouvelle table. Pour lancer les migrations :

```ruby
rails db:migrate
```

Attention : si vous ne lancez pas la migration, la table restaurants n’existera pas dans la base de données et le modèle Restaurant ne pourra donc pas s’y connecter.

#### Migration

Vous avez parfois besoin de générer une migration, par exemple pour ajouter une colonne à une table existante. Pour cela, utilisez le générateur de migration de Rails :

```ruby
rails g migration AddRatingToRestaurants rating:integer
rails db:migrate # pour lancer la nouvelle migration
```

Notez bien la façon de nommer la migration qui respecte la convention CamelCase avec un s à Restaurants car on parle ici de la table restaurants à laquelle on veut ajouter une nouvelle colonne rating de type integer.

### La console Rails <a id="13"></a>

Une fois que vous avez créé un modèle et lancé la migration qui crée la table associée au modèle, vous pouvez tester votre modèle dans la console rails. Rien de plus simple :

```ruby
rails console # ou juste rails c
```

### Les méthodes basiques d’Active Record <a id="14"></a>

Vous pouvez retrouver toutes les méthodes qu’on décrit ci-dessous dans la [documentation officielle](https://guides.rubyonrails.org/active_record_basics.html).

#### All

La méthode `all` permet de récupérer toutes les entrée de la table (ici on lit dans la table `products`). Comprenez bien que ActiveRecord va faire la requête SQL correspondante pour vous et vous renvoyer les résultat sous la forme d’un tableau ruby d’objet de la classe `Product`, qui sont ensuite très simples à manipuler en ruby.

```ruby
Product.all
#==> SELECT * FROM products
```

#### New, save et create

Pour créer un nouveau produit en base de données, vous pouvez le faire en deux étapes avec `new` et `save` :

```ruby
kudoz = Product.new(name: "kudoz", url: "getkudoz.com")
kudoz.save
#==> INSERT INTO products (name, url) VALUES ('kudoz', 'getkudoz.com')
```

Ou alors en un coup avec la méthode `create` :

```ruby
Product.create(name: "kudoz", url: "getkudoz.com")
#==> INSERT INTO products (name, url) VALUES ('kudoz', 'getkudoz.com')
```

C’est parfois intéressant de le faire en deux temps, lorsqu’on a par exemple des **validations** sur le modèle (voir plus bas).

#### Find

La méthode `find` permet de retrouver un produit dans la table étant donné son identifiant `id` :

```ruby
Product.find(1)
#==> SELECT * FROM products WHERE id = 1
```

#### Validations

On peut ajouter des validations Active Record sur un modèle si l’on veut se protéger contre l’écriture de mauvaise données en base. Prenons un exemple :

```ruby
class Restaurant < ActiveRecord::Base
  validates :name, presence: true
  validates :address, presence: true, uniqueness: true
  validates :rating, inclusion: {in: [0, 1, 2, 3, 4, 5]}
end
```

Ici, on ne peut pas sauver un produit en base si jamais :

    * Il n’a pas de nom ou d’adresse
    * Son adresse n’est pas unique (i.e. il y a déjà un produit avec la même adresse dans la DB)
    * Son rating n’est pas compris entre 0 et 5

Si on essaie de sauver un produit invalide (par exemple dans la console), Active Record va d’abord vérifier les validations et empêcher d’écrire en base si les validations ne passent pas :

```
rails c
> wrong = Restaurant.new(name: "Wrong restaurant", "1 wrong street", rating: 1000000)
> wrong.save # N'écrit pas en base de données et renvoie => false
```

la methode `valid?` permet de tester la variable avant de la sauvegarder en BDD
Ici, nous avons rendu obligatoire le nom et l'url or la variable instantiée ne
contient pas de nom :
```ruby
> kudoz = Product.new(url: “getkudoz.com”)
> kudoz.valid? # => false
> kudoz.save   # => false
> kudoz.name = “Kudoz”
> kudoz.valid? # => true
> kudoz.save   # => true
```


## COURS N11

### Les actions CRUD <a id="15"></a>

Dans la plupart des sites, on veut pouvoir **créer / lire / modifier / supprimer** un modèle. Cela peut être un `Product` sur ProductHunt, un `Flat` sur Airbnb, ou encore un `Post` sur Facebook.

    * As a user, I can **CRUD** a flat (dans AirBnB)
    * As a user, I can **CRUD** a tweet (dans Tweeter)
    * As a user, I can **CRUD** a post (dans Facebook)
    * As a user, I can **CRUD** a product (dans ProductHunt)

Il est donc **extrêmement important** de connaître toutes les routes conventionnelles de Rails qui correspondent à ces actions CRUD.

### Les 7 routes CRUD <a id="16"></a>

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


    * Retenez bien à chaque fois **l’URL de la requête** ainsi que **le nom de l’action** dans le controlleur.
    * Notez bien que la création et la modification se font chacune **en deux requêtes**.

### Création et modification <a id="17"></a>

Pour créer un appartement sur Airbnb (ou encore une review sur Yelp, un post sur Facebook, etc.), ça se fait toujours **en deux temps** :

    * Une première requête `GET` permet d’arriver sur la page de création contenant un **formulaire vierge**.
    * En soumettant le formulaire, une seconde requête `POST` envoie les données du formulaire au site web *pour qu’il les enregistre en base*.

C’est exactement la même chose pour modifier une entrée existante :

    * Une première requête `GET` permet d’arriver sur la page d’édition contenant un **formulaire pré-rempli**.
    * En soumettant le formulaire, une seconde requête `PATCH` envoie les données du formulaire au site web **pour qu’il les modifie en base**.

### Méthode de routing resources <a id="18"></a>

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

Pour aller plus loin dans le routing Rails, n’hésitez pas à lire la documentation officielle sur le routing Rails.

### Les helpers <a id="19"></a>

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


## COURS N12

### Actions `new` et `create` <a id="20"></a>

Comme on l’a vu la dernière fois, créer un produit se fait en deux temps, deux requêtes HTTP, et donc deux actions (les actions `new` et `create`) :

    * `new` sert a afficher le formulaire de création de produit
    * En soumettant ce formulaire on fait une requête `POST` qui va appeler l’action `create` permettant d’enregistrer le produit en base.

### Formulaire HTML natif <a id="21"></a>

Commençons par le `new` qui renvoie la vue `new.html.erb.` Un formulaire de création en HTML, ça ressemble à ça :
```ruby
<form action="/products" method="post">
  <input type="text" name="product[name]"> #ici on met les param dans un tab
  <input type="text" name="product[tagline]">
  <input type="submit">
</form>
```

Le formulaire est envoyé via une requete http `POST "/products"`:
```ruby
params = {
  product: {
    name: "Kudoz"
    tagline: "tinder for job search"
  }
}
```

    * Ici, les attributs `name` des balises `<input>` sont très importants et **servent à nommer les paramètres** pour pouvoir les récupérer dans les `params` de Rails comme dans le schéma au-dessus.
    * Le problème d’un formulaire HTML comme celui-là, c’est qu’il ne sécurise pas la requête HTTP qui est faite quand on le soumet. Cette requête pourrait très bien venir d’un autre site et d’un petit malin qui veut vous hacker.
    * Rails a un mécanisme de protection qui vérifie que la requête contient une clef de sécurité (appelée `authenticity_token`) qui **garantit que cette requête vient bien du formulaire de votre site**.

## Simple form et clef de sécurité

En raison de ce mécanisme de sécurité, **vous ne pouvez pas utiliser un formulaire HTML natif dans Rails pour faire des requêtes POST**.

Vous devez utiliser une méthode ruby qui génére le code HTML du formulaire et **y ajoute une clef de sécurité**. La méthode basique qui permet de faire ça dans Rails s’appelle `form_for` mais elle est compliquée à utiliser.

on préfère la méthode `simple_form_for` qui fait la même chose que `form_for` avec une syntaxe plus simple (comme son nom l’indique). Si vous voulez lire la doc de cette [gem](https://github.com/plataformatec/simple_form).

La syntaxe `simple_form_for` pour générer un formulaire est la suivante (on considère ici que `@product = Product.new`) :
```ruby
<%= simple_form_for @product do |f| %>
  <%= f.input :name, placeholder:"kudoz", label:"quel produit?" %>
  <%= f.input :tagline %>
  <%= button :submit %>
<% end %>
```

Cela equivaut à:
```ruby
<form action="/products" method="post">
  <input type="text" name="product[name]" id="name">
  <input type="text" name="product"[tagline]" id="address">
  <input type="hidden" name="authenticity_token" value="AODLAM..."
  <input type="submit">
</form>
```

Ici, le formulaire va non seulement envoyer les données entrées par l’utilisateur (`name` et `tagline` du produit) mais la requête contiendra aussi un `authenticity_token` qui la sécurise. C’est presque gagné ! Il reste quand même un deuxième mécanisme de sécurité à mettre en place avant de sauvegarder les données en base.

### Strong `params`: filtrer ses paramètres <a id="22"></a>

Rien n’empêche un utilisateur d’ajouter des champs dans un formulaire en éditant le HTML comme dans la vidéo. Dans ce cas, la requête provient bien de notre site (elle a donc un `authenticity_token`) mais elle contient des infos supplémentaires qu’on n’a pas forcément envie d’enregistrer en base.

Dans l’exemple ci-dessous, quelqu’un a essayé d’ajouter une mauvaise review à Kudoz en ajoutant un champ dans le formulaire avant de le soumettre.

```
params = {
  product: {
    name: "Kudoz",
    tagline: "tinder for job search"
    review: "I am a hater..."
  }
}

params.require(:product)

{
    name: "Kudoz",
    tagline: "tinder for job search"
    review: "I am a hater..."
}

params.require(:product).permit(:name, :tagline)

{
  name: "Kudoz",
  tagline: "tinder for job search"
}
```


Heureusement, Rails permet d’appliquer un **filtre** aux paramètres dans le controller. Dans le schéma ci-dessus, ce filtre n’autorise que les champs `name` et `tagline`. **Du coup le champ `review` passe à la trappe**. C’est vous qui choisissez les paramètres que vous laissez passer dans vos controller.

### Finissons le `new` et `create` <a id="23"></a>

Voici le code final de nos actions de création dans le `ProductsController`, qui gère aussi les validations Active Record comme dans la vidéo :
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
    params.require(:product).permit(:name, :url, :tagline)
  end
end
```

Les validations Active Record nous permettent d’avoir des comportements différents lorsqu’on soumet le formulaire:

    * Si les données sont valides, on sauve le produit en base et on redirige vers le listing des produits (page `index`)
    * Si les validations ne passent pas, on retourne le formulaire pré-rempli pour que l’utilisateur puisse le modifier avec des données valides avant de le soumettre à nouveau.


### Validations et `Seed` <a id="24"></a>

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

### sauver les données écrit sur les champs même si la page est rechargé <a id="25"></a>

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



## COURS N13

### Les actions `edit` et `update` <a id="26"></a>

Pour éditer un produit existant en base de données, cela se fait en deux étapes comme pour la création :

    * L’action `edit` sert à afficher le formulaire **pré-rempli** permettant à l’utilisateur de changer certains champs.
    * En soumettant ce formulaire, on fait une requête de type `PATCH` qui va appeler la méthode update` et modifier les informations en base de données.

Regardons le routing qui correspond à ces deux actions :
```
Prefix        Verb    URI Pattern           Controller#Action
edit_product  GET     /products/:id/edit    products#edit
              PATCH   /products/:id         products#update
```

Que ce soit pour afficher le formulaire pré-rempli ou pour modifier le produit en base données, **on a d’abord besoin de récupérer son identifiant dans l’URL pour aller le chercher**. Les deux requêtes correspondant aux actions ont donc toutes les deux un `:id` dans l’URL et le code des deux actions démarrent de la même façon :
```ruby
class ProductsController < ApplicationController
  def edit
    @product = Product.find(params[:id])
  end
  def update
    @product = Product.find(params[:id])
     # ...
  end
end
```

### `simple_form_for` est malin comme un singe ! <a id="27"></a>

On peut utiliser la méthode `simple_form_for` soit avec un nouveau produit `@product = Product.new` soit avec un produit qu’on est allé chercher en base `@product = Product.find(params[:id])`. Dans les deux cas, le code du formulaire sera le même :
```ruby
<%= simple_form_for @product do |f| %>
  <%= f.input :name %>
  <%= f.input :url %>
  <%= f.input :tagline %>
  <%= f.button :submit %>
<% end %>
```

    * Si le produit est nouveau (`@product = Product.new`), **Simple Form construira un formulaire HTML vierge**.
    * Si le produit existe déjà (`@product = Product.find(params[:id])`), `Simple Form construira un formulaire HTML pré-rempli` avec les informations actuelles du produit en question.

Vu que Simple Form est si malin, le code du formulaire `edit.html.erb` sera exactement le même que celui du formulaire `new.html.erb`. Bon, vous pouvez quand même changer les titre `<h1>` des deux templates !

### L’action `update` <a id="28"></a>

L’action `update` va ensuite être très proche du `create` :
```ruby
class ProductsController < ApplicationController
  def update
    @product = Product.find(params[:id]) # 1
    if @product.update(product_params)   # 2
      redirect_to products_path          # 3
    else
      render :edit                       # 4
    end
  end

  private
  def product_params
    params.require(:product).permit(:name, :url, :tagline)
  end
end
```

Décrivons ce qu’elle fait :

    1. Elle va chercher le produit qu’on veut modifier à partir de son `:id` récupéré dans l’URL.
    2. Elle essaie de l’updater avec des paramètres filtrés par la méthode `product_params` (pour se protéger contre un hack)
    3. Si les validations passent, elle update le produit en base et on redirige vers le listing des produits (page `index`)
    4. Si les validations ne passent pas, elle retourne le formulaire d’édition pré-rempli pour que l’utilisateur puisse le modifier avec des données valides.

### L’action `destroy` <a id="29"></a>

Le routing de l’action `destroy` est le suivant :
```
Prefix    Verb    URI Pattern    Controller#Action
          DELETE  /products/:id  products#destroy
```

Là encore, on a besoin de l’`:id` dans l’URL pour aller chercher le produit qu’on veut supprimer. Le code de l’action `destroy` est ensuite très simple.
```ruby
class ProductsController < ApplicationController
  def destroy
    @product = Product.find(params[:id])  # on va chercher le produit
    @product.destroy                      # on le supprimer
    redirect_to products_path             # on redirige vers index
  end
end
```

Remarquons ici que les URLs des actions `show` et `destroy` sont les mêmes :
```
Prefix    Verb    URI Pattern    Controller#Action
product   GET     /products/:id  products#show
          DELETE  /products/:id  products#destroy
```

C’est bien pour ça qu’on a une seule méthode `product_path` pour générer l’URL `/products/:id`. Si on veut un lien qui fait bien une requête `DELETE` (et non une requête `GET`) dans nos templates, on doit ajouter l’option `method: :delete` lorsqu’on appelle la méthode `link_to`. **Regardez bien la différence entre les deux liens suivants** :
```ruby
<%= link_to "Aller voir le produit", product_path(@product) %>
<%= link_to "Supprimer le produit", product_path(@product), method: :delete %>
```

    * Le premier lien fait une requête `GET` sur l’URL `product_path(@product)`, c’est donc un lien classique vers la page `show` qui détaille du produit.
    * Le second lien fait une requête `DELETE` **sur la même URL**. D’après notre routing, cette requête va être traitée par l’action `destroy` qui va supprimer le produit de la base de données.

### “Refacto” de son code <a id="30"></a>

Maintenant qu’on a codé toutes les actions du `ProductsController` et les vues associées, il est temps de faire une “refacto” de son code, c’est-à-dire factoriser les morceaux de code qui sont répétés.

### Filtre `before_action` dans son controller <a id="31"></a>

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

On a gagné quelques lignes avec cette méthode. Quand vous avez un gros code de controlleur, quelques lignes ça compte !

### Factoriser ses formulaires avec une partielle ERB <a id="32"></a>

On a exactement le même code pour le formulaire `simple_form` dans les templates `new.html.erb` et `edit.html.erb`.
```ruby
<%= simple_form_for @product do |f| %>
  <%= f.input :name %>
  <%= f.input :url %>
  <%= f.input :tagline %>
  <%= f.button :submit %>
<% end %>
```

C’est un peu idiot car si on veut enrichir ce formulaire (par exemple en ajoutant un `input`), on devra le faire à deux endroits. Heureusement, ERB nous permet de définir des vues **partielles** qui sont des fichiers ERB qui commence par un `_` et qu’on peut injecter dans d’autres templates. Ici ça donne :
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


## COURS N14

Il faut prendre l'habitude de séparer tous composant CSS (avatar, button, banner...) dans un fichier à part puis les regrouper dans 'style.css' via des `@import url(components/avatar.css)`.

on peut aussi definir la police pour le body et les titres dans 'style.css'

---
https://placeholder.com/ ou https://unsplash.com permet de pointer vers des images en ligne tres utile lors du prototypage.
exemple:
```css
<img src:"http://placehold.it/50x50" alt="">
<img src:"http://unsplash.it/400/300/?random" alt=""> #le random n'est pas obligatoire
```

Pour imposer un style on utilise "!important":
```css
.dropdown-menu a{
  color: black !important
}
```

Les filtres sur les images (gradient filter):
```css
background: linear-gradient(angle,
    start_color start_point,
    end_color end_point),
  url("bckground.jpg")
```


position relative: positionner un objet puis dans cette objet nous
pouvons potionner des sous-objets en Position Absolu en fonction de
son parent.

Flexbox, permet de faciliter l'alignement verticale/horizontale d'elements qui n'ont pas la meme taille dans une div:
```css
.flex{
  display: flex;
}
.flex-item{
  flex: 0 0 200px;
}
```

unité en css3 le "vh" à voir (utilisé dans les banner fullscreen)

voir le plugin emmet qui permet de faire:
```css
(li>a)*3
```

tout ceci dans la video et lien:

- https://www.youtube.com/watch?v=ewxMpl09OwE
- http://lewagon.github.io/ui-components/

(en gros, soit faire tt de a-z soit se baser sur par exemple bootstrap puis customiser)

voir le framework de frontend : "middleman" (http://samuelbourdon.com/couicstart-template-middleman/)

pour les newsletter:
* sendinblue
* mailchimp
* wufoo

customiser les carte googlemap avec https://snazzymaps.com/

console JS en ligne https://jsbin.com/

Pipette Sip sur mac ou extension Chrome ColorZilla
Plugin Chrome FontFace Ninja
Sketch (free trial) sur mac ou inkscape

Voici les trois packages qu’on installe sur SublimeText3

    * Emmet
    * ColorPicker
    * ColorHighlighter

### Emmet <a id="33"></a>

Créez un fichier index.html dans Sublime text et entrainez-vous avec Emmet, par exemple, tapez
```
    h1+h2+img+p+a puis tab
    ul>li*3 puis tab
    ul>(li>a)*3 puis tab
    div#wrapper>div.container>h2 puis tab
    a.btn.btn-primary puis tab
    div.container>div.row>(div.col-xs-9+div.col-xs-3) puis tab
```
### Color Picker <a id="34"></a>

Créez un fichier style.css dans Sublime text et entrâinez-vous avec Color Picker, par exemple, écrivez
```
h1 {
  color: /* Cmd + Shift + C */;
}
```
Pour choisir une couleur avec color picker, entrez Cmd + Shift + C ou Ctrl + Shift + C (sur windows). Cela fait apparaître une palette de couleur dans laquelle vous pouvez piocher, et ça injecte le code hexadecimal directement dans votre CSS, comme par magie !

### Color Highlighter <a id="35"></a>

Si ColorHighlighter est bien installé, vous devez voir la couleur correspondant à un code hexadecimal dans le CSS lorsque vous cliquez sur ce code hexadecimal (cf. image ci-dessous). Très pratique vu qu’il est assez difficile de connaître par coeur tous les codes hexadecimaux !

EXEMPLE DE SITES TRES BEAU: https://www.awwwards.com/websites/sites_of_the_day/

On peut heberger les image des sitesweb sur https://aws.amazon.com/fr/cloudfront/

---

### Le layout de l’application <a id="36"></a>

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

Le contenu de chaque template (`show.html.erb`, `index.html.erb`, `edit.html.erb`, etc..) va venir s’injecter dans le layout au niveau du mot-clef **yield**.

### Partielles partagées <a id="37"></a>

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

### Raisonner par composant web <a id="38"></a>

Pour organiser votre CSS et être très performant en frontend, on vous recommande vivement de “raisonner par composant”. Deux petits cadeaux pour vous mettre à niveau :

    * La [librairie](http://lewagon.github.io/ui-components) de composant graphiques du vagon qu’on utilise dans la vidéo.
    * Le [workshop](https://www.youtube.com/watch?v=ewxMpl09OwE) Youtube Web-components qui recode tous les composants de cette librairie.

### Eplacement des images <a id="39"></a>

les images doivent etre placé dans `app/assets/images`

Pour injecter avec ERB l'url d'une image avec `image_path` :
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

Il suffit de créér un fichier `_banner.scss` dans le dossier en question puis importer la partial dans le fichier `_index.scss` du même repertoire qui fait office de "main principale" comme ceci `@import "banner";`.

Faire un lien icon:

```
<!-- HELPER : le product path de chaque produit, le lien GET /products/:id, ici nous n'avons pas de text et on utilise "do...end" -->
        <li>
          <%= link_to product_path(product) do %>
            <i class="fa fa-eye"></i>
          <% end %>
          </li>
```

## COURS N15

### Travailler sur une nouvelle user story <a id="40"></a>

Dans cette video, on travaille sur une nouvelle user story.

    En tant que visiteur, je peux consulter des produits filtrés par catégorie.

Implémenter une user story sur un site existant demande au développeur d’être rigoureux et de ne rien oublier depuis la base de données jusqu’au templates ERB. Voici les bonnes questions à se poser, dans le bon ordre :

    Cette user story necessite-t-elle de changer le schéma de la DB sur http://db.lewagon.org.
    Si oui, faut-il générer un nouveau modèle (et donc une nouvelle table) ou juste pour modifier une table existante grâce à une migration ? Doit-on ajouter des validations à nos modèles ?
    Faut-il de nouvelles routes ? Dans l’exemple de la video, on n’a pas besoin de nouvelles routes (ce n’est pas systématique).
    Que doit-on modifier dans les actions du controlleur ? Y-a-t-il de nouveaux strong params à autoriser ?
    Enfin, quelles informations doit-on ajouter aux vues (nouvelles données, nouvelles navigations, nouveau boutons, etc..)

En résumé, vous devez passer par toutes les couches de Rails quand vous implémenter une nouvelle fonctionnalité:

    DB
    modèle
    routing
    controller
    view

Avoir une bonne méthodologie de travail prend du temps et c’est normal si vous vous emmêlez un peu les pinceaux au début (est-ce que je dois coder dans le routing ? Dans les controllers ? Dans les vues ?). En essayant d’être rigoureux et en vous posant les bonnes questions sur toute la stack Rails depuis la base de données jusqu’aux template HTML, vous allez progresser vite !

---

Pour ajouter la colone "category" à une table qui existe déjà "Products" on fait:
```
rails g migration AddCategoryToProducts category:string
#puis on lance la migration
rails db:migrate
```

Dans `db/migrate` nous avons:
```ruby
class AddCategoryToProducts < ActiveRecord::Migration[5.1]
  def change
    add_column :products, :category, :string
  end
end
```

Puis dans `app/models/product.rb` on ajoute une validation sur la catégorie:
```ruby
validates :category, inclusion: { in: %w(tech education design),
    message: "%{value} is not a valid category." }
```

 Dans le routing, controller puis vue...

Dans le controller, on ajoute "category":
```ruby
private
    def product_params
      #require permet de garder que ce que contient product puis on filtre avec permit
      params.require(:product).permit(:name, :url, :tagline, :category)
    end
```

 dans la vue "simple_form":
```ruby
<%= f.input :category, collection: ["tech", "education", "design"], prompt: quelle categorie?  %>
 ```

dans le css, voir l'usage de "$" car la couleur est plus designé:
```css
.card-category.design {
  background: $blue;
}
```

enfin modifier `products_controller.rb`:
```ruby
def index
  if params[:category]
      @products = Product.where(category: params[:category])
    else
      @products = Product.all
    end
end
```

Dans le `home.html.erb`, si on veut avoir un bouton pour se diriger vers la categorie "tech":
```ruby
<div class="col-xs-12 col-sm-4">
  <%= link_to "tech", products_path(category: "tech"), class: "card-category tech" %>
</div>
```


## COURS N16

Nous alons déployer notre application Rails sur Heroku,
un des leaders du marché des PaaS (Platform as a Service). L’idée est d’utiliser
une solution clé en main pour ne pas avoir à se soucier de monter soi-même son serveur.

### Prise en main <a id="41"></a>

Le tutoriel de la vidéo commence à cette [adresse](https://devcenter.heroku.com/articles/getting-started-with-ruby#introduction), je vous invite donc à suivre les étapes au fur et à mesure.


### Installation <a id="42"></a>

Sur Mac, lancez simplement dans le terminal :
```
brew install heroku
```

Sur Cloud9, lancez la commande :
```
wget -O- https://toolbelt.heroku.com/install-ubuntu.sh | sh
```

### Connexion via le terminal <a id="43"></a>
```
heroku login

#pour voir avec quel compte on est logué
heroku auth:whoami

#pour se deconnecter
heroku logout
```

### Création d’une application <a id="44"></a>

Pour créer une application Heroku sur le datacenter européen, la commande à lancer (dans le dossier racine de votre application Rails) est :
```
heroku create --region=eu <le_nom_de_votre_app>
```

appli créé:
```
https://vhunt.herokuapp.com/ | https://git.heroku.com/vhunt.git
```

### Déploiement <a id="45"></a>

Lister les remotes sur lequel on peut envoyer notre code:
```
git remote -v
```

Pour déployer sur Heroku, nous allons à nouveau utiliser `git`, mais cette fois nous allons pousser sur une autre `remote` que `origin` :
```
git push heroku master
```

Durant le push, heroku fait un `rake assets:precompile` qui permet de minifier les fichiers JS, CSS, images, etc et les met dans un seul fichier.

Si on a pas été assez rapide entre le `git push` et le `db:migrate` faire un `heroku restart`

Dans la foulée, il ne faut pas oublier de lancer les migrations sur le schéma de données de production :
```
heroku run rails db:migrate
```

Pour ouvrir une page web sur le site directement:
```
heroku open
```

### Logs <a id="46"></a>

Pour observer les logs de l’application sur Heroku en cas d’erreur 500, lancez la commande :
```
heroku logs
```

Si vous voulez suivre en direct les logs au fur et à mesure des requêtes, ajoutez l’argument `--tail` :
```
heroku logs --tail
```

### Rails console <a id="47"></a>

Vous pouvez lancer une Rails console en production avec la commande :
```
heroku run rails c
```

Très pratique pour exécuter rapidement quelques requêtes ActiveRecord comme par exemple :
```
Product.count.inspect
Product.count
```

ou encore :
```
Product.last.inspect
p = Product.last
#on peut le supprimer par exemple
p.destroy
```

Faîtes attention si vous utilisez `destroy` ou même `destroy_all` !

### Prix <a id="48"></a>

Je n’en parle pas dans la vidéo, mais c’est quelque chose d’important. Heroku est gratuit dans des conditions de développement. Il y a un concept de “dyno” qu’on peut apparenter à une unité de serveur. Dans le plan gratuit, vous avez le droit à un dyno gratuit qui va pouvoir tourner jusque 18 heures par période de 24 heures. Lorsque votre application ne reçoit pas de requêtes HTTP (pas de visiteurs en gros), elle va dormir, et il faut qu’elle dorme au moins 6 heures par jour.

Si vous voulez que votre application soit tout le temps active, il faudra commencer à payer. Le plan Hobby à 7$ / mois est plutôt intéressant et avec un bon ROI sachant que vous n’avez aucun travail d’administration système à fournir.

Plus tard, pour une application Rails de production, il faudra passer à des plans plus chers, mais bon, il n’y a pas de free lunch ! Pour la petite histoire, l’hébergement de la plateforme Le vagon On Demand (sur laquelle vous êtes actuellement)sur Heroku coûte actuellement 96$ / mois.

Je peux vous assurer être très content de payer pour la tranquilité d’esprit de ne pas à avoir à gérer moi-même le serveur 24h/24, 7j/7 !


## COURS N17

### Utilisateurs et système d'authentification <a id="49"></a>

La gem `devise` va vous permettre:

    * D’ajouter un Sign in et un Sign up à votre application.
    * Votre base de données va donc s’enrichir d’un nouveau modèle, `User`.

### Devise <a id="50"></a>

Dans la suite de ces instructions, nous supposons que **vous n’avez pas
encore généré de modèle** `User`.

### Installation <a id="51"></a>

Ouvrez votre `Gemfile` et ajoutez la ligne suivante :
```
gem 'devise', '4.0.0.rc2'
```

Sauvegardez le fichier dans Sublime Text, ensuite dans le terminal lancez :
```
bundle install
```

Lancez ensuite la commande :
```
rails generate devise:install
```

Pour générer le modèle `User`, lancez les commandes :
```
rails generate devise user
rails db:migrate
```

### Routes <a id="52"></a>

Lancez un `rails routes` en ligne de commande pour voir les nouvelles routes installées.
Ce qui nous intéresse, ce sont les trois suivantes :
```
new_user_registration GET    /users/sign_up(.:format)       devise/registrations#new
     new_user_session GET    /users/sign_in(.:format)       devise/sessions#new
 destroy_user_session DELETE /users/sign_out(.:format)      devise/sessions#destroy
```

Ainsi, vous pouvez aller sur `localhost:3000/users/sign_up` pour vous créer un compte puis
sur `localhost:3000/users/sign_in` pour vous connecter.

### Côté vue <a id="53"></a>

Un helper bien utile va vous permettre de modifier votre barre de navigation afin de la rendre plus intelligente, c’est-à-dire qu’elle va afficher de l’information conditionnelement au fait qu’un utilisateur est connecté ou non. Ce helper est :
```
user_signed_in?
```

puis dans la navbar par exemple:
```
<% if user_signed_in? %>
//afficher ce qu'il faut
<% else %>
//ne rien afficher
<% end %>
```

Pour rendre les messages flash plus jolis, n’hésitez pas à utiliser ce gist:
```ruby
#_flashes.html.erb
<!-- This file is in `app/views/shared/_flashes.html.erb` -->

<% if notice %>
  <div class="alert alert-info alert-dismissible" role="alert">
    <button type="button" class="close" data-dismiss="alert" aria-label="Close"><span aria-hidden="true">&times;</span></button>
    <%= notice %>
  </div>
<% end %>
<% if alert %>
  <div class="alert alert-warning alert-dismissible" role="alert">
    <button type="button" class="close" data-dismiss="alert" aria-label="Close"><span aria-hidden="true">&times;</span></button>
    <%= alert %>
  </div>
<% end %>


#application.html.erb
<!-- This file is in `app/views/layouts/application.html.erb` -->

<%# [...] %>

<%= render 'shared/flashes' %>

<%# [...] %>
```

Pour modifier les écrans de Sign in et Sign up par défaut de Devise (qui sont très “bruts de décoffrage”…), il faut d’abord importer ces vues dans notre propre projet par la commande :
```
rails generate devise:views
```

### Côté controlleur <a id="54"></a>

La politique la plus safe à utiliser est celle de la liste blanche. Par défaut, on interdit l’accès à toutes les pages pour les utilisateurs non connectés, et on ouvre certains accès uniquement.

Cela se passe dans le fichier `app/controllers/application.controller.rb` en ajoutant la ligne :
```
# app/controllers/application_controller.rb
class ApplicationController < ActionController::Base
  # [...]
  before_action :authenticate_user!
end
```

Maintenant, dans certains controlleurs, on peut décider que certaines actions soient accessibles pour un utilisateur **non** connecté. Par exemple, si on souhaite que la route `/about`, gérée par `PagesController#about`, on aura :
```
# app/controllers/pages_controller.rb
class PagesController < ApplicationController
  skip_before_action :authenticate_user!, only: [ :about ]

  # [...]
end
```

Le `only:` est là pour préciser un `Array` d’actions sur lesquelles le `skip_before_action` s’applique. Si il n’y a pas de `only:`, alors le `skip_before_action` s’applique à `toutes` les actions du controlleur.

### Impact sur le schéma <a id="55"></a>

#### `user_id` dans `products`

Pour l’instant, un produit est créé sans être relié à un utilisateur en particulier. Nous voulons donc conserver en base de données une trace du créateur du produit. Pour cela nous allons ajouter une clé étrangère `user_id` dans la table `products`

3 Tables dans la BDD soit USERS[id, name, email, password], UPVOTES[id, user_id, product_id] et PRODUCTS[id, name, tagline, url, user_id, category]

Pour ajouter cette colonne, on va générer la migration suivante :
```
#Ajout d'une clé étrangere
rails generate migration AddUserToProducts user:references
```

Vérifiez la migration automatiquement générée qui devrait compoter la ligne :
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
```

```
# app/models/user.rb
class User < ApplicationRecord
  has_many :products

  # [...]
end
```

### Côté controlleur <a id="56"></a>

Au niveau du contrôlleur, on va utiliser le helper de Devise `current_user` pour associer automatiquement le produit nouvellement créé avec l’utilisateur actuellement connecté.
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

### Exercice <a id="57"></a>

Comme dit dans la vidéo, comment pourriez-vous modifier le code de la méthode `#destroy` du `ProductsController` pour que **seul le créateur du produit puisse le supprimer** (même question pour l’édition !). Discutons-en sur le forum :)

---

Pour afficher toutes les erreurs lors du dev:
```ruby
#dans un fichier.html.erb
<%= @product.errors.full_messages %>
```

### Coté Back Office <a id="58"></a>

#### Le Saas Forest Admin

Utiliser le [SaaS Forest Admin](https://www.forestadmin.com/) qui demande beaucoup moins d’effort de code, notamment pour la connexion avec des services tiers (Mailchimp, Stripe, etc.)

#### Gem rails_admin

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

C’est le setup standard de Rails Admin qu’on conseille aux élèves du vagon. ça nécessite bien entendu d’avoir Devise installé auparavant.

Ensuite pour gérer plus finement les permissions, plutôt que de parsemer les contrôleurs et les vues de if, on utilise des gems d’autorisations comme `cancancan` ou `pundit`.


## COURS N18

### Cloudinary <a id="59"></a>

[Cloudinary](http://cloudinary.com/) est un service de stockage d’image dans le cloud. Il permet également d’automatiser des traitements classiques lorsqu’on manipule des images dans un contexte de site web, à savoir les redimensionnements et compressions d’images.

En effet, il faut que les images pèsent le moins possible (largeur x hauteur mais aussi également compression JPEG) pour que le site se charge vite. C’est encore plus vrai sur mobile.

Créez-vous un compte (avec le plan gratuit) avant de passer à la suite.

Aperté : Nous ne pouvons pas utiliser Heroku comme espace de stockage des images car Heroku ne possède pas de système de stockage permanent. En gros, à chaque déploiement `git push heroku master`, tout le disque dur du serveur est effacé. D’où la necessité d’un service tiers comme Cloudinary. Pour en savoir plus, lisez ceci à propos du [ephemeral filesystem](https://devcenter.heroku.com/articles/dynos#ephemeral-filesystem)



### Installation dans Rails <a id="60"></a>

#### La gem `figaro`

Cette gem vous permet de protéger les secrets nécessaires à l’utilisation de services tiers. Le principe de cette gem est de stocker dans un fichier `config/application.yml` toutes les informations sensibles, et d’ajouter au fichier `.gitignore` ce fichier pour qu’il **ne se retrouve pas sur GitHub**.

Si vous avez utilisé le template du vagon pour générer votre application, vous n’avez rien à faire. Si vous avez fait un simple `rails new`, alors suivez le [README](https://github.com/laserlemon/figaro/) de la gem.

Instalation:
```
gem "figaro"
bundle exec figaro install
```


#### Installation de la gem Cloudinary

Dans notre gemfile, mettre cette ligne:
```ruby
gem "cloudinary"
```

Puis faire un `bundle install`.

### Configuration <a id="61"></a>
Dans votre fichier `config/application.yml`, ajoutez la ligne suivante en mettant votre URL cloudinary recupérable via le Dashboard en ajoutant les `: ` (deux points espace) et les `""` (guillemets) :
```yml
CLOUDINARY_URL: "cloudinary://..................."
```

### Upload d’une image en console <a id="62"></a>

Téléchargez une image, mettez-là à la racine de votre application web. Ensuite, lancez une Rails console (avec `rails c`) puis :
```
Cloudinary::Uploader.upload('votre_image.jpg')
```

En retour de cette commande nous avons :
```
=> {"public_id"=>"fhl0u2gh59e5qblfvarj",
 "version"=>1124955037,
 "signature"=>"etc42f603e5b541cde7c934f5a09f0dc335058af",
 "width"=>600,
 "height"=>400,
 "format"=>"jpg",
 "resource_type"=>"image",
 "created_at"=>"2018-04-28T22:37:17Z",
 "tags"=>[],
 "bytes"=>37075,
 "type"=>"upload",
 "etag"=>"c0100f9d1d3839fgda1ee148f5dcb86e",
 "placeholder"=>false,
 "url"=>"http://res.cloudinary.com/blabla/image/upload/v1521955017/ffl0u2gh59e5qblfyarj.jpg",
 "secure_url"=>"https://res.cloudinary.com/blabla/image/upload/v1521955017/ffl0u2gh59e5qblfyarj.jpg",
 "original_filename"=>"votre_image"}
```

Nous avons maintenant l'url permettant d'afficher l'image dans nos vues et nous avons aussi le `public_id` qui est un identifiant unique pour notre image, c'est cette variable qu'il faut sauvegarder en BDD pour faire réference à cette image plus tard.

### Affichage de l’image dans une page statique <a id="63"></a>

Pour finir de tester que tout s’est bien passé, on peut rapidement tester sur la page Team en ajoutant dans la vue la ligne suivante, la méthode `cl_image_tag` de la gem `cloudinary` :
```ruby
<!-- app/views/pages/team.html.erb -->
<%= cl_image_tag "PUBLIC_ID_DE_L_IMAGE" %>
```

Ensuite on peut manipuler l’image pour changer sa taille par exemple :
```ruby
<%= cl_image_tag "PUBLIC_ID_DE_L_IMAGE", width: 400, height: 100, crop: :fill %>
```

Je vous invite à lire la doc [Image transformations](https://cloudinary.com/documentation/image_transformations) pour avoir une idée des transformations à votre disposition. Ensuite, vous pouvez lire cette doc [Rails image manipulation](https://cloudinary.com/documentation/rails_image_manipulation) qui est spécifique à Rails et à l’utilisation de `cl_image_tag`.

### Upload d’image par l’utilisateur avec `attachinary` <a id="64"></a>

Voici la procédure [Attachinary Setup](https://gist.github.com/ssaunier/a32538935e6384af4c29) à suivre pour installer et configurer la gem. C’est la procédure que je suis dans la vidéo.

---

#### Attachinary Setup

First add the following gems to your `Gemfile`:

```ruby
# Gemfile
gem "attachinary"
gem "jquery-fileupload-rails"
gem "coffee-rails"
```

Then open the terminal and launch:

```bash
bundle install
rails attachinary:install:migrations
rails db:migrate
```

Open your `config/application.rb` and add this line after all the `require`:

```ruby
require "attachinary/orm/active_record"
```

Open the `config/routes.rb` file and add this as first line in the `draw` block:

```ruby
mount Attachinary::Engine => "/attachinary"
```

Open `app/views/layout/application.html.erb` and append this line after the main `javascript_include_tag`:

```erb
<%= cloudinary_js_config %>
```

Open `app/assets/javascripts/application.js` and append these lines before the `require_tree`:

```js
//= require jquery-fileupload/basic
//= require cloudinary/jquery.cloudinary
//= require attachinary
```

Create a file `app/assets/javascripts/init_attachinary.js` and copy-paste those lines:

```
$(document).ready(function() {
  $('.attachinary-input').attachinary();
});
```

##### Usage

###### One picture per model

You need to update the model:

```ruby
class Product < ApplicationRecord
  has_attachment :photo

  # [...]
end
```

And the form (`simple_form` gem used):

```erb
<%= f.input :photo, as: :attachinary %>
```

And the controller for strong params:

```ruby
def product_params
  params.require(:product).permit(:name, :description, :photo)
end
```

To display the product photo in the view, add (ceci genere la balise img etc):

```erb
<% if @product.photo? %>
  <%= cl_image_tag @product.photo.path %>
<% end %>
```

Pour recuperer que l'url de l'image
```erb
<%= cloudinary_url @product.photo.path, width: 200 %>
```

autres exemples :
```erb
#autre exemple:
<!-- on fait une condition avec la methode cloudinary qui fournit la balise img  -->
<% if product.photo? %>
  <%= cl_image_tag(product.photo.path, height: 117, width: 175, crop: :fill, class: 'product-image') %>
<% else %>
  <img src="http://unsplash.it/300/200?random" alt="kudoz" class="product-image hidden-xs">
<% end %>

#autre exemple:
<!-- Banner avec cloudinary_url qui permet d'avoir que l'url dans une condition ternaire-->
<div class="banner" style="background-image: linear-gradient(-225deg, rgba(0,101,168,0.6) 0%, rgba(0,36,61,0.6) 50%), url('<%= @product.photo? ? cloudinary_url(@product.photo.path, width: 1280, height: 700, crop: :fill) : image_path("banner-home.jpg") %>');">
```

##### Multiple pictures per model

You need to update the model:

```ruby
class Product < ApplicationRecord
  has_attachments :photos, maximum: 2  # Be carefule with `s`

  # [...]
end
```

And the form (`simple_form` gem used):

```erb
<%= f.input :photos, as: :attachinary %>
```

And the controller for strong params:

```ruby
def product_params
  params.require(:product).permit(:name, :description, photos: [])
end
```

To display the product photos in the view, add:

```erb
<% @product.photos.each do |photo| %>
  <%= cl_image_tag photo.path %>
<% end %>
```


##### Ajout d'un Avatar - Devise

(si l'img est en 30x30 on peut le mettre en 60x60 pour les rétina. puis forcer le 30x30 via CSS)

Il suffit de faire la même chose que dans le chapitre **"One picture per model"**
Dans le model `User` il faut ajouter:
```ruby
# app/models/user.rb
class User < applicationRecord
  #relation BDD, ajout d'un avatar
  has_attachment :avatar
  ...
```

Puis ajouter dans le formulaire de modification utilisateur généré par Devise qui a également généré la route (`edit_user_registration GET    /users/edit(.:format)          devise/registrations#edit`):
```erb
# app/views/devise/registrations/edit.html.erb
<%= f.input :avatar, as: :attachinary %>
```

Dans nos controllers nous avons rien qui correspond à Devise. Quand on va faire un PUT/PATCH on pointe sur le controller `devise/registrations#updade` qui est à l'interieur de la gem. Pour palier à ce probleme, il faut ajouter le code ci-dessous dans `application_controller` **(le before_action et la methode)**.

If you want to add an `avatar` to the `User` model, you need to sanitize regarding the strong params :

```ruby
# app/controllers/application_controller
class ApplicationController < ActionController::Base

  before_action :configure_permitted_parameters, if: :devise_controller?

  def configure_permitted_parameters
    devise_parameter_sanitizer.permit(:sign_up,        keys: [:avatar])
    devise_parameter_sanitizer.permit(:account_update, keys: [:avatar])
  end
end
```

Enfin dans la navbar nous allons ajouter notre avatar :
```erb
<!-- si l'user actuel a un avatar on l'affiche sinon img default -->
<% if current_user.avatar? %>
  <%= cl_image_tag current_user.avatar.path, width: 50, height: 50, crop: :fill, class: 'avatar dropdown-toggle', id: 'navbar-wagon-menu', :'data-toggle' => 'dropdown' %>
<% else %>
  <img src="https://kitt.lewagon.com/placeholder/users/ssaunier" class="avatar dropdown-toggle" id="navbar-wagon-menu" data-toggle="dropdown">
<% end %>
```

---

### Mise en production <a id="65"></a>

Comme d’habitude, il va falloir faire un `commit` et le pousser sur Heroku (puis lancer les migrations). Mais avant ça, il y a une étape importante. Comme on a ajouté une ligne à notre fichier `config/application.yml` (et que **ce fichier n’est pas dans git, donc pas envoyé à Heroku**), il faut communiquer à Heroku la valeur de cette variable d’environnement.

Cela va se faire grâce à la ligne de commande suivante (en mettant bien évidemment **votre propre clé** récupérée sur votre dashboard)
```
DANS LA VIDEO C'EST UN ADD PAS UN SET
heroku config:set CLOUDINARY_URL=cloudinary://...................
```


## COURS N19

### Fonctionnalité d'upvote sur un produit <a id="66"></a>

Marche à suivre lorsqu'on ajoute une nouvelle fonctionnalité :

> **Model -> Routing -> Controler -> Vue**

**FAIRE UNE TABLE DE JOINTURE QUAND ON A DES RELATION N:N EN BDD :**

La fonctionnalité d’upvote du `current_user` pour un produit va nécessiter une **table de jointure** qui va stocker tous ces votes.

```
  ___upvotes{id,user_id,product_id}___
 |                                    |
 |                                    |
 users{id,name,email,password}______products{id,name,tagline,url,user_id,category}
```

#### Modèle

Pour générer le modèle `Upvote`, on a fait tourné cette commande :

```
rails g model upvote user:references product:references
rails db:migrate
```

On a le nouveau modèle suivant :

```ruby
# app/models/upvote.rb
class Upvote < ApplicationRecord
  belongs_to :user
  belongs_to :product

# ici on dit qu'un user est unique dans la cadre d'un produit
  validates :user, uniqueness: { scope: :product }
end
```

Et il ne faut pas oublier d’enrichir les deux modèles `User` et `Product` existants :

```ruby
# app/models/user.rb
class User < ApplicationRecord
  # [...]
  has_many :upvotes
end
```

```ruby
# app/models/product.rb
class Product < ApplicationRecord
  # [...]
  has_many :upvotes
end
```

Nous allons ajouter des upvotes au scénario :

```ruby
# db/seeds.rb
#Detruire tout ce qui est en base
Product.destroy_all
User.destroy_all

vegeta = User.create!(email: "vegeta@vegeta.com", password: "vegetavegeta")
jiren = User.create!(email: "jiren@jiren.com", password: "jirenjiren")

#puis on créé des seed, le "!" permet de lever une exception si la seed ne passe pas a cause d'une validation par exemple
Product.create!(user: jiren, name: "Kudoz", url: "http://www.site.com", tagline: "tinder for job search", category: "tech")
Product.create!(user: jiren, name: "kamehameha", url: "http://www.kamehouse.com", tagline: "atk of goku", category: "education")
Product.create!(user: vegeta, name: "shumpo", url: "http://www.fly.com", tagline: "fast run", category: "design")

# Upvotes? on peut faire de 2 façons
Upvote.create!(user: vegeta, product: kudoz)
# ou
kudoz = Product.create!(user: jiren, name: "Kudoz", url: "http://www.site.com", tagline: "tinder for job search", category: "tech")
kudoz.upvotes.create! user: vegeta
```

Puis detruire la BDD et la reconstruire :

```
rails db:drop db:create db:migrate db:seed
```

#### Routes

Pour voter et annuler son vote, on a besoin de deux routes :

```ruby
# config/routes.rb
Rails.application.routes.draw do
  # [...]
  # on peut avoir plusieurs "resources" pas de probleme
  resources :upvotes, only: [ :create, :destroy ]
end
```

#### Contrôleur

Ces routes vont arriver dans le `UpvotesController` qu’on peut générer avec la commande suivante :

```
rails g controller upvotes
```

et du coup on a :

```ruby
# app/controllers/upvotes_controller.rb
class UpvotesController < ApplicationController
  def create
    product = Product.find(params[:product_id])
    product.upvotes.create! user: current_user
    redirect_to products_path
  end

  def destroy
    upvote = Upvote.find(params[:id])
    upvote.destroy
    redirect_to products_path
  end
end
```

#### Vue

Dans la vue, on va afficher le compteur de vote, qui va avoir dépendre du fait que le `current_user` a voté pour le produit ou non.

Tout d’abord on a besoin d’un helper dans le modèle `User` :

```ruby
# app/models/user.rb
class User < ApplicationRecord
  # [...]
  def voted_for?(product)
    product.upvotes.where(user: self).any?
  end
end
```

pour ensuite dans la vue `index` des produits avoir (on stipule la methode post car par defaut on utilise la methode GET) :

```ruby
<!-- app/views/products/index.html.erb -->

<% if user_signed_in? %>
  <% if current_user.voted_for?(product) %>
    <%= link_to upvote_path(current_user.upvotes.where(product: product).first), method: :delete, class: 'product-upvote product-upvoted' do %>
      <div class="product-arrow"></div>
      <div class='product-count'>
        <%= product.upvotes.size %>
      </div>
    <% end %>
  <% else %>
    <%= link_to upvotes_path(product_id: product.id), method: :post, class: 'product-upvote' do %>
      <div class="product-arrow"></div>
      <div class='product-count'>
        <%= product.upvotes.size %>
      </div>
    <% end %>
  <% end %>

<% else %>
  <div class='product-upvote'>
    <div class="product-arrow"></div>
    <div class='product-count'>
      <%= product.upvotes.size %>
    </div>
  </div>
<% end %>
```


## COURS N20

(utiliser l'inspecteur d'elements dans le navigateur pour voir la structure de la page, voir aussi l'onglet network et console pour debug)

Je vous invite à lire le code du [commit de ce cours](https://github.com/lewagon/wagon-hunt/commit/4b74c9fce179a46159f4c083888ec9d2f692085b) pour bien comprendre ce qui a été ajouté aux différentes parties du MVC pour rendre la page dynamique.

Je vous invite également à lire [l’article de Rails Guide](https://edgeguides.rubyonrails.org/working_with_javascript_in_rails.html) qui parle de JavaScript dans Rails. Les exemples de code sont en CoffeeScript, vous pouvez les “traduire” simplement avec le site [js2.coffee](http://js2.coffee/)


---

#### Contenue du commit de ce cours :

```css
#app/assets/stylesheets/components/_product.scss
/* Upvote design */
.product-upvote {
+  display: inline-block;
  padding-right: 20px;
  text-align: center;
  transition: all 0.15s ease;
```

```ruby
#app/controllers/upvotes_controller.rb
class UpvotesController < ApplicationController
  def create
    # Upvote?
  -  product = Product.find(params[:product_id])
  -  product.upvotes.create! user: current_user
  -  redirect_to products_path
  +  @product = Product.find(params[:product_id])
  +  @product.upvotes.create! user: current_user
  +  respond_to do |format|
  +    format.html { redirect_to products_path }
  +    format.js
  +  end
  end

  def destroy
    upvote = Upvote.find(params[:id])
  +  @product = upvote.product
    upvote.destroy
  -  redirect_to products_path
  +  respond_to do |format|
  +    format.html { redirect_to products_path }
  +    format.js
  +  end
  end
end
```

```ruby
#app/views/products/index.html.erb
<div class="product">
=begin
          <% if user_signed_in? %>
            <%# Upvote action %>
            <% if current_user.voted_for?(product) %>
              <%= link_to upvote_path(current_user.upvotes.where(product: product).first), method: :delete, class: 'product-upvote product-upvoted' do %>
                <div class="product-arrow"></div>
                <div class='product-count'>
                  <%= product.upvotes.size %>
                </div>
              <% end %>
            <% else %>
              <%= link_to upvotes_path(product_id: product.id), method: :post, class: 'product-upvote' do %>
                <div class="product-arrow"></div>
                <div class='product-count'>
                  <%= product.upvotes.size %>
                </div>
              <% end %>
            <% end %>
          <% else %>
            <div class='product-upvote'>
              <div class="product-arrow"></div>
              <div class='product-count'>
                <%= product.upvotes.size %>
              </div>
            </div>
          <% end %>
=end
      +    <div class="upvote-container" id="product-<%= product.id %>">
      +      <%= render 'upvotes/show', product: product %>
      +    </div>

          <% if product.photo? %>
            <%= cl_image_tag(product.photo.path, height: 117, width: 175, crop: :fill, class: 'product-image') %>
```

```ruby
#TT CE CODE FAIT PARTIE DU COMMIT

#app/views/upvotes/_show.html.erb
<% if user_signed_in? %>
  <% if current_user.voted_for?(product) %>
    <%= link_to upvote_path(current_user.upvotes.where(product: product).first), remote: true, method: :delete, class: 'product-upvote product-upvoted' do %>
      <div class="product-arrow"></div>
      <div class='product-count'>
        <%= product.upvotes.size %>
      </div>
    <% end %>
  <% else %>
    <%= link_to upvotes_path(product_id: product.id), remote: true, method: :post, class: 'product-upvote' do %>
      <div class="product-arrow"></div>
      <div class='product-count'>
        <%= product.upvotes.size %>
      </div>
    <% end %>
  <% end %>
<% else %>
  <div class='product-upvote'>
    <div class="product-arrow"></div>
    <div class='product-count'>
      <%= product.upvotes.size %>
    </div>
  </div>
<% end %>
```

```ruby
#app/views/upvotes/create.js.erb
+ $('#product-<%= @product.id %>').html('<%= j render 'upvotes/show', product: @product %>');
```

```ruby
#app/views/upvotes/destroy.js.erb
+ $('#product-<%= @product.id %>').html('<%= j render 'upvotes/show', product: @product %>');
```

---

### Vue (d’où part la requête AJAX) <a id="67"></a>

Pour rendre un lien dynamique et le forcer à faire partir une requête AJAX plutôt qu’une navigation classique de page, il faut utiliser `remote: true` :

```ruby
#.html.erb
<%= link_to upvotes_path(product_id: product.id),
      remote: true,
      method: :post
    do %>
  <!-- [...] -->
<% end %>
```

### Contrôleur <a id="68"></a>

Lorsqu’on reçoit une requête AJAX dans un contôleur Rails, le format est `js`. Du coup, il faut gérer spécifiquement ce cas, tout en conservant le code pour gérer le cas où la requête n’est pas au format AJAX (on parle de **JavaScript non-obstrusif**) :

```ruby
respond_to do |format|
  format.html { ... }
  format.js
end
```

### Vue (de réponse AJAX) <a id="69"></a>

Du coup, ça va demander d’avoir une vue spécifique, d’extension `.js.erb`. Dans
cette vue, on va pouvoir utiliser les variables d’instances définies dans le contrôleur. Et surtout, ce qu’il faut comprendre, c’est qu’on n’écrit pas du HTML, **on y écrit du JavaScript**. Et donc du jQuery.

```javascript
$('#some-element').html('<%= j render "some/partial" %>');
```

Ne pas y oublier le `j`, un alias du helper `escape_javascript`.


## CONCLUSION

### Resources <a id="70"></a>

#### Rails Guide
Lisez et relisez la [documentation Rails Guide](http://edge.rubyonrails.org/), c’est une mine d’or et la réponse à votre question s’y trouve sans doute. Je vous conseille de lire tous les chapitres sur [ActiveRecord](http://guides.rubyonrails.org/active_record_basics.html) comme un roman.

#### Vidéos
[RailsCasts](http://railscasts.com/) est un projet qui a beaucoup contribué à l’essor de Rails. Mis en sommeil en 2013 par son fondateur, la plupart des vidéos sont encore pertinentes.

[GoRails](https://gorails.com/) est le successeur de RailsCasts. Beaucoup de vidéos récentes et à jour par rapport aux versions 4 et 5 de Rails.

#### Gems
Une des force de Rails est sa communauté open-source et les nombreuses gems à notre disposition pour prototyper vraiment très rapidement. Le repo [awesome-rails](https://github.com/ekremkaraca/awesome-rails) fait une compilation des meilleurs gems dans plein de secteurs, allez fouiner !

Dans un autre style, [Ruby Toolbox](https://www.ruby-toolbox.com/) est très bien pour comparer deux gems d’un même domaine. Les critères à prendre en compte sont la popularité, la maintenance de la gem (date du dernier commit ?), etc. ce que fait Ruby Toolbox dans son calcul de score.

#### Add-ons
(pas obligé d'utiliser Heroku)
Regardez du côté des [Add-ons Heroku](https://elements.heroku.com/addons) il y a plein de choses pour envoyer des emails, des SMS, intégrer de la recherche, etc.

#### Meetups
N’hésitez pas à venir à [Paris.rb](http://www.meetup.com/fr-FR/parisrb/) qui fait un meetup tous les premiers mardis du mois, on y parle de Ruby et Rails. En province, il y a également des meetups nottamment Ruby Nord, Ruby Bordeaux ou encore Lyon.rb (et j’en passe).

#### Newsletter
Vous pouvez vous abonner à [Ruby Weekly](http://rubyweekly.com/) qui paraît chaque jeudi et qui est pas mal du tout pour suivre l’actu de la communauté Ruby.



