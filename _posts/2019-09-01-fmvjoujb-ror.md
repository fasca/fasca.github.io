---
layout: post
title: fmvjoujb RoR
date: 2019-09-01
tags:
  - backend
  - script
  - ruby
  - rails
  - web
description: debuter avec RoR...
categories: Web
serie: Backend
published: true
---

**Sommaire**

- [Créér un projet Rails](#1) 
- [Description de l'arborescence](#2)
- [Executer le projet](#3)
- [Presentation du projet d'exemple, La Bibliothèque](#4)
- [Exemple du fichier Gemfile pour ce projet d'exemple en utilisant Bundler](#5)
- [Le scaffolding MVC facile](#6)
- [Les routes](#7)
- [La manipulation des donnes](#8)
- [PAPERCLIP](#9)
- [Aller plus loin avec RoR](#10)

---

## Créér un projet Rails <a id="1"></a>

```
$ rails new minimal_project
```

Ceci permet de créer toute l'arborescence n'ecessaire pour un projet Rails en utilisant **Bundler**.


## Description de l'arborescence <a id="2"></a>

app : Contient l'ensemble des données propore à l'application.

bin : Contient certains binaires propre à Ruby on Rails. `Rake` qui permet d'executer certaines tâches et `Rails`qui est un outils en ligne de commande.

config : Contient la configuration de l'application, le démarrage de l'application, l'environnement (developpement, prod et test). Il y a aussi les initialiseur permettant d'initialiser du code. locals contient les traductuons et routes contient les chemins.

* **db** : contient les bases de données

* **lib** : contient les bibliotheques 

* **log** : contient les fichiers de log

* **public** : content les fichiers statiques

* **rakefile** : correspond aux taches executés (qui sont par defaut dans lib/task)

* **test** : posede les tests unitaires

* **tmp** : repertoire temporaire

vendor : repertoire specifique pour les gems 


### Le repertoire `app` plus en detail

le repertoire `app` content:

* **assets** : contient des images, des fichiers JS et le CSS

* **controllers** : contient les controleurs de l'application (MVC)

* **helpers** : contient un ensemble de module, methodes utilisés dans les vues et les controleurs

* **mailers**: permet d'envoyer des mails via Ruby on Rails

* **models** : contient les models (MVC)

* **views** : contient toutes les vues (MVC)


## Executer le projet <a id="3"></a>

Il faut se rendre à la racine du projet puis lancer le serveur WEBrick et récuperer l'url proposée :

```
$ rails s

#ou

$ rails server
```




## Presentation du projet d'exemple, La Bibliothèque <a id="4"></a>

l'uml:

`UTILISATEURS   <--emprunte-->   LIVRES`


Creation de ce projet sans les tests unitaires par défaut de RoR:

```
$ rails new library_online -T
```


## Exemple du fichier Gemfile pour ce projet d'exemple en utilisant Bundler <a id="5"></a>

```
source 'https://rubygems.org'

ruby '2.0.0'

# Bundle edge Rails instead: gem 'rails', github: 'rails/rails'
gem 'rails', '4.0.0'

# POUR AVOIR TOUT LES MSG TRADUIT
# Rails i18n
gem 'rails-i18n'

group :development, :test do
  # Use sqlite3 as the database for Active Record
  gem 'sqlite3'
end

group :production do
  # Use PostgreSQL as the database for Active Record
  gem 'pg'
end

group :production do
  gem 'rails_12factor' # Heroku
end

# PERMET DE GENERER DES FORMULAIRE SIMPLEMENT
# Simple Form
gem 'simple_form', github: 'plataformatec/simple_form'
gem 'country_select'

# Bootstrap SaSS
gem 'bootstrap-sass', '~> 2.3.0.1'

# Use SCSS for stylesheets
gem 'sass-rails', '~> 4.0.0'

# Use Uglifier as compressor for JavaScript assets
gem 'uglifier', '>= 1.3.0'

# Use CoffeeScript for .js.coffee assets and views
gem 'coffee-rails', '~> 4.0.0'

# Devise
gem 'devise', '~> 3.0.1'

# Paperclip
gem 'paperclip'

# See https://github.com/sstephenson/execjs#readme for more supported runtimes
# gem 'therubyracer', platforms: :ruby

# Use jquery as the JavaScript library
gem 'jquery-rails'

# Turbolinks makes following links in your web application faster. Read more: https://github.com/rails/turbolinks
gem 'turbolinks'

# Build JSON APIs with ease. Read more: https://github.com/rails/jbuilder
gem 'jbuilder', '~> 1.2'

group :doc do
  # bundle exec rake doc:rails generates the API under doc/api.
  gem 'sdoc', require: false
end

group :test, :development do
  # RSpec
  gem 'rspec-rails', '~> 2.14.0'

  # Factory girl
  gem 'factory_girl_rails'
  
  # Capybara
  gem 'capybara', '~> 2.1.0'
  
  # Email spec
  gem "email_spec", ">= 1.4.0"
end

# Use ActiveModel has_secure_password
gem 'bcrypt-ruby', '~> 3.0.0'

# Use unicorn as the app server
# gem 'unicorn'

# Use Capistrano for deployment
# gem 'capistrano', group: :development

# Use debugger
# gem 'debugger', group: [:development, :test]

```

Ensuite on instal les gems:

```
$ bundle install
```

Puis on genere l'installation de `SIMPLE FORM` avec Bootstrap:

```
$ rails generate simple_form:install --bootstrap
```


Pour les tests unitaires on instal `RSPEC`:

```
$ rails generate rspec:install
$ bundle binstubs rspec-core
```

On genere une Base de Donnée (initialisation):

```
$ rake db:migrate
```


On configure rspec avec le fichier `spec_helper.rb`:

```
# This file is copied to spec/ when you run 'rails generate rspec:install'
ENV["RAILS_ENV"] ||= 'test'
require File.expand_path("../../config/environment", __FILE__)
require 'rspec/rails'
require 'rspec/autorun'
require 'email_spec'

# Requires supporting ruby files with custom matchers and macros, etc,
# in spec/support/ and its subdirectories.
Dir[Rails.root.join("spec/support/**/*.rb")].each { |f| require f }

# Checks for pending migrations before tests are run.
# If you are not using ActiveRecord, you can remove this line.
ActiveRecord::Migration.check_pending! if defined?(ActiveRecord::Migration)

RSpec.configure do |config|
  # ## Email specs
  config.include(EmailSpec::Helpers)
  config.include(EmailSpec::Matchers)
  
  # ## Mock Framework
  #
  # If you prefer to use mocha, flexmock or RR, uncomment the appropriate line:
  #
  # config.mock_with :mocha
  # config.mock_with :flexmock
  # config.mock_with :rr

  # Remove this line if you're not using ActiveRecord or ActiveRecord fixtures
  config.fixture_path = "#{::Rails.root}/spec/fixtures"

  # If you're not using ActiveRecord, or you'd prefer not to run each of your
  # examples within a transaction, remove the following line or assign false
  # instead of true.
  config.use_transactional_fixtures = true

  # If true, the base class of anonymous controllers will be inferred
  # automatically. This will be the default behavior in future versions of
  # rspec-rails.
  config.infer_base_class_for_anonymous_controllers = false

  # Run specs in random order to surface order dependencies. If you find an
  # order dependency and want to debug it, you can fix the order by providing
  # the seed, which is printed after each run.
  #     --seed 1234
  config.order = "random"
end

```


Puis dans le fichier `application.css` on ajoute en commentaire `=reqyure custom` cela permet d'inclure le fichier `custom.css.scss`:

```
/*
*
*= require_self
*= require custom
*/


Le fichier `custom.css.scss` contient:

```scss
@import "bootstrap";
```

Dans `application.js` on ajoute également ceci:

```javascript
//= require jquery
//= require jquery_ujs
//= require turbolinks
//= require bootstrap
```

Pour tester si l'installation est fonctionnel en utilisant la commande `rake` en lançant les tests par défaut:

```
$ rake
```

Enfin on démarre le serveur et on test la page `0.0.0.0:3000` :

```
$ rails s
```


## Le scaffolding MVC facile <a id="6"></a>


Pour generer du scaffolding (permet de generer la migtration pour la bdd, on a une abstraction de la bdd grâce à `ACTIVE RECORD` et tout ce qu'on a besoin pour le MVC), on a un objet qui decrit la bdd, puis le reste RoR s'en occupe (mysql, sqlite....):

```
$ rails generate scaffold Book title:string author:string
```

la commande precedente genere tout ce qu'il faut pour l'objet crée MVC, BDD, REST etc...

Dans `locales/routes.rb`il faut ajouter:

```ruby
resources books
```

Pour verifier si les routes sont bien disponibles:

```
$ rake routes
```

Puis migrer la base de donnée, pour créer la table `books` directement dans la BDD:

```
$ rake db:migrate
```

RoR crée tout le site avec routes et le formulaire, on peut tester la page `0.0.0.0/books` (ajout, modif, suppr de livres), on peut aussi avoir le rendu en JSON `0.0.0.0/books.json`




## Les routes <a id="7"></a>


les routes sont dans `config/routes.rb`.





## La manipulation des donnes <a id="8"></a>

il est possible de manipuler les données (tels que rails) avec la commande `rails c` ou `rails console` , par exemple `books.all`permet de voir la liste de tout les livre





## PAPERCLIP <a id="9"></a>

paperclip permet de modifier les images avant de les uploader sur S3 par exemple, donc on redimensionne l'image avant d'envoyer, il gere beaucoup de choses, meme le pdf, (creer des aperçu de pdf, mp3, video, photo...)

voir les services cloud AWS tres interessant (ex: pour l'envoie de mails avec SES)


## Aller plus loin avec RoR <a id="10"></a>

Mongodb -> Mongoid

Active_Merchant = permet de payer avec la CB, paypal, etc... pour les change on peut prendre BRAINTREE ils ne sont pas cher

Active_Shipping = pour la gestion des colis, fedex etc...

delayed_job = Permet de faire des actions en tache de fond, exemple avec paperclip on redimentionne l'image et on dit coté frontend "traitement en cours", on peut envoyer des mails en différé etc...

tinymce-rails = permet d'integer l'environement TinyMCE permettant de personaliser les themes

tinymce-rails-imageupload = (ATTENTION NON COMPATIBLE RAILS 4) permet d'uploader des images simplement




