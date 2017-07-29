---
layout: post
title: Apprendre Ruby
date: 2017-07-15
tags:
  - backend
  - developpement
description: cours rapide sur Ruby
categories: developpement backend
serie: programmation
published: true
---

>  source: https://github.com/hackademy-io

## **SOMMAIRE**



<a href="#1">1- Les types primitifs String et Numeric</a>

<a href="#2">2- Les types primitifs Array et Hash</a>

<a href="#3">3- Les structures de controle</a>

<a href="#4">4- Variables et identifieurs</a>

<a href="#5">5- Créer une classe</a>

<a href="#6">6- Les accesseurs</a>

<a href="#7">7- L'héritage</a>

<a href="#8">8- La visibilité des méthodes</a>

<a href="#9">9- Les bases de la réflexion</a>

<a href="#10">10- Les symboles</a>

<a href="#11">11- La classe Time</a>

<a href="#12">12- Les classes Date et Datetime</a>

<a href="#13">13- La classe Array</a>

<a href="#14">14- Manipuler des chaînes de caractères</a>

<a href="#15">15- Les expressions rationnelles, partie 1</a>

<a href="#16">16- Les expressions rationnelles, partie 2</a>

<a href="#17">17- Les entrées sorties</a>

<a href="#18">18- Les attributs de fichier</a>

<a href="#19">19- Fichiers temporaires et répertoires</a>

<a href="#20">20- Sérialisation et persistance</a>

<a href="#21">21- Les threads en ruby</a>

<a href="#22">22- Synchroniser les threads</a>

<a href="#23">23- La programmation système</a>

<a href="#24">24- La programmation réseau</a>

<a href="#25">25- Les tests automatisés, partie 1</a>

<a href="#26">26- Les tests automatisés, partie 2</a>

<a href="#27">27- Utiliser le debugger</a>

>

<div id="1"><h2>1- LES TYPES PRIMITIFS STRING ET NUMERIC</h2></div>

Bienvenue dans cette toute nouvelle série dédiée à la découverte du langage Ruby.

Nous allons commencer par des sujets très simples qui vont vous permettre d'acquérir des bases solides avant nous attaquer à des aspects plus complexes du langage.

Cette série sera découpée ne traitant que d'un sujet bien délimité.

Avant de démarrer assurez vous que vous possédez une version récente de Ruby, nous supposons dans cette vidéo que votre version de Ruby est supérieure ou égale à la 2.2.

Vous pouvez vérifier la version actuelle à l'aide de la commande `ruby -v`.

Si votre version de Ruby est trop ancienne, vous pouvez installer une version plus récente grâce à un gestionnaire de version tel que Rbenv ou encore RVM.

Dans ses vidéos nous utiliserons beaucoup un outil très utile livré avec Ruby qui s’appelle IRB. C'est une console interactive qui permet de saisir du code Ruby et de voir en retour le résultat de l'expression évaluée.

C'est donc notamment très pratique pour tester de petits morceaux de code, vérifier une syntaxe ou comparer deux implémentations.

Dans ces vidéos IRB vous permettra de voir en temps réel le résultat d'une expression sans avoir à tester de votre côté en parallèle.

Entrons maintenant dans le vif du sujet en parcourant les types "primitifs" disponibles en Ruby et que vous utiliserez au quotidien.

En Ruby, tout est objet, même ce que nous appelons ici les types primitifs. Quand nous utilisons ces types primitifs nous utilisons donc en fait une instance d'une classe.

Nous appelons ici la méthode `times` sur l'entier 2 ce qui va nous permettre d'afficher deux fois la chaîne "Hello".

Nous appelons ensuite la méthode `upto` sur l'entier 3 avec pour paramètre `5` ce qui va nous permettre d'afficher les entiers de 3 à 5.

Nous créons maintenant une chaîne "Hackademy" sur laquelle nous appelons la méthode `size` qui nous permet de connaître sa taille.

On voit que ses types primitifs sont en fait des objets sur lesquels on peut appeler des méthodes.

### La classe String

Voyons maintenant plus en détail la classe `String`.

Nous stockons ici une chaîne dans la variable `s` puis nous vérifions sa classe à l'aide de la méthode `class`. C'est bien une `String` qu'on a ici.

Nous appelons ensuite la méthode `succ` qui permet d'avoir le successeur de cette chaîne, ici le dernier caractère devient le "z".

Nous changeons maintenant le contenu de cette chaîne par "hackademy" suivi d'un retour à la ligne. Et nous appelons la méthode `chomp` dessus qui permet de supprimer ce retour à la ligne.

Nous changeons à nouveau le contenu de la variable `s` pour y mettre "hackademy". Nous allons appeler la méthode `chop` dessus qui permet simplement de supprimer le dernier caractère.

Nous vérifions maintenant la longueur de la chaîne `s` grâce à la méthode `length`.

Nous appelons maintenant la méthode `capitalize` qui n'agit que sur la première lettre. Puis la méthode `upcase` qui elle permet de transformer toute la chaîne.

### Les numériques : Numeric, Fixnum, Bignum, Integer, Float

Passons maintenant aux `Numeric`, c'est à dire les entiers mais aussi les nombres à virgules flottante.

Nous allons d'abord stocker l'entier "20" dans la variable `i`, vérifier sa classe, c'est un `Fixnum`. Les `Fixnum` sont en fait une classe enfant de la classe `Numeric`.

Cette classe `Numeric` regroupe donc les entiers, les flottants, les très grands entiers.

Nous appelons la méthode `succ` qui permet d'avoir le successeur, c'est ici 21.

Nous faisons une simple addition, 2 + 3 et nous nous rendons compte que c'est en fait un sucre syntaxique pour un appel de méthode : `2.+(3)`.

Vérifions maintenant la classe d'un nombre à virgule flottante, c'est un `Float`. Les `Float` eux aussi sont des enfants de la classe `Numeric`.

### Conclusion

Voilà pour cette présentation rapide des objets des classes `String` et `Numeric` que vous utiliserez au quotidien.
 
Nous n'avons ici qu'effleuré la surface des possibilités de ces classes. Je vous invite donc à en lire la documentation pour découvrir l'étendu des possibilités.


<div id="2"><h2>2- LES TYPES PRIMITIFS ARRAY ET HASH</h2></div>

### Les tableaux : Array

Les tableaux sont très utilisés et vous permettent  de stocker et d'ordonner un jeu d'objets. On peut stocker des objets de différents types au sein d'un même tableau.

On stocker un tableau dans la variable `a`. Ce tableau contient certain nombre d'entiers. Ici 2, 5 et 10.

On va ensuite ajouter un entier supplémentaire à la fin de ce tableau grâce au double chevron qui est un sucre syntaxique pour un vrai appel de méthode, la méthode `push`.

On va maintenant ajouter un entier en début de tableau grâce à la méthode `unshift` et on va essayer de rappeler l'une des valeurs grâce à son index que l'on passe entre crochets. C'est encore une fois un sucre syntaxique pour la méthode `at`.

Nous ajoutons maintenant en fin de tableau deux objet `nil` qui représentent le néant. Et nous allons compacter le tableau, c'est à dire supprimer l'ensemble de ses valeurs `nil`.

On appele donc pour ce faire la méthode `compact!`.

On ajoute maintenant un tableau en fin de tableau et on va donc se retrouver avec un tableau à deux dimensions. On va maintenant aplatir ce tableau grâce à la méthode `flatten!` puis on va rendre les valeurs uniques grâce à la méthode `uniq!`. On a donc ici chaîné deux appels de méthode.

On ajoute maintenant une chaîne "foo" en fin de tableau et on va chercher à connaître son index grâce à la méthode `index`.

On mélange ensuite le tableau grâce à la méthode `shuffle`.

On va maintenant créer un nouveau tableau qui va contenir les valeurs doublées de chaque valeur du premier tableau et pour ce faire on utilise la méthode `map` qui nous permet d'itérer sur chaque valeur du premier tableau et de stocker dans le nouveau tableau la valeur qui est retournée par notre morceau de code, ici la valeur multipliée par deux.

On se retrouve donc bien avec un tableau pour lequel l'ensemble des valeurs ont été doublées et notamment la chaîne qui est devenue "foofoo".

On va maintenant soustraire au tableau `double_a` le tableau `a`, on a donc supprimé les valeurs communes.

On procède ensuite à une jointure entre le tableau `double_a` et le tableau `a`, grâce au `|`

Et on fait maintenant une intersection entre le tableau `double_a` et le tableau `a`. Ce qui nous retourne uniquement les valeurs communes.

### Les tableaux associatifs : Hash

On passe maintenant aux tableaux associatifs représentés en Ruby par la classe `Hash`. On va donc stocker dans la variable `h` un tableau associatif. On utilise donc une accolade ouvrante et un ensemble de clés / valeurs puis on referma avec une accolade fermante.

Ici les clés sont un élément un peu spécial de Ruby qu'on appelle des symboles mais on reviendra sur ce point précis plus tard.

On va ensuite essayer d'afficher la valeur de l'une des clés.

On essaie de récupérer la valeur d'une clé qui n'existe pas ce qui nous retourne `nil` et on va modifier le comportement de ce hash pour qu'il ait une valeur par défaut sur les clés qui n'existent pas, ici la chaîne "Foo".

Si on appelle à nouveau cette clé qui n'existe pas, on a maintenant la valeur par défaut qui nous est retournée.

On recherche maintenant une clé qui existe.

On crée un nouveau hash avec une clé commune au premier hash, le symbole `:a`. Et une clé qui n'existe pas, le symbole `:z` dans lequel on va stocker "baz".

On note que la valeur pour la clé `a` est différente de la valeur pour la clé `a` du premier tableau.

On va maintenant procéder à un merge entre les deux tableaux et on voit donc que la valeur associée à la clé `a` a été modifiée pour prendre celle qui était disponible dans `h2` et la clé `z` est tout simplement ajoutée.

### Conclusion

Voilà pour cette présentation rapide des types `Array` et `Hash` que vous utiliserez trés souvent.
 
Bien évidemment ce n'est ici que approche très succincte et une fois encore je vous invite à aller lire la documentation relative à ces classes.


<div id="3"><h2>3- LES STRUCTURES DE CONTROLE</h2></div>

### Les classiques

Voyons tout d'abord les structures classiques.

Comme vous pouvez vous en douter, il existe en Ruby le mot-clé `if` qui permet de créer une branche conditionnelle dans le code.

On peut donc écrire des choses comme :

```
if 1 == 1
	puts "OK"
end
```

On utilise dans cet exemple le double égal pour comparer deux valeurs entre elles. Si les valeurs sont égales, on utilise la méthode `puts` qui va nous permettre d'afficher une chaîne. On clôt notre condition avec le mot-clé `end`.

On peut aussi créer des conditions à deux branches qui permettent de couvrir le cas où les valeurs sont égales mais aussi le cas où elles ne le sont pas. Pour ce faire, on utilise le mot-clé `else` en coordination avec le mot-clé `if` :

```
if 1 > 2
	puts "1 est plus grand que 2"
else
	puts "1 est plus petit que 2"
end
```

Si la condition n'est pas égale à `true` alors on passera dans la branche `else` ce qui est le cas dans notre exemple.

On utilise ici le chevron pour vérifier si la valeur de gauche est plus grande que la valeur de droite.

Pour aller plus loin, on peut encore ajouter des branches à notre condition grâce au mot-clé `elsif`. C'est un cas plus rare mais c'est une possibilité du langage. On peut donc écrire des conditions du type :

```
if false
	puts "faux"
elsif true
	puts "vrai"
else
	puts "autre"
end
```

C'est donc la branche `elsif` qui remplie la condition et on affiche "vrai".

### Utilisation de `unless`

Très souvent on a besoin d'inverser une condition, on peut donc utiliser le mot-clé `if` avec un point d'exclamation devant la condition pour l'inverser :

```
if !false
	puts "OK"
end
```

mais il existe un idiome en Ruby pour exprimer cette condition inversée, c'est le mot clé `unless`. On peut donc ré-écrire notre condition de la façon suivante :

```
unless false
	puts "OK"
end
```

On gagne donc en lisibilité et les intentions sont plus claires.

### Les conditions post-fixées

Dans bien des cas, on souhaite écrire une condition qui ne va concerner qu'une seule ligne de code. En Ruby, plutôt que d'ouvrir un bloc conditionnel pour une seule ligne, on peut utiliser des conditions post-fixées.

Elles consistent à être placées directement après la ligne de code concernée et sont une fois encore un moyen d'améliorer la lisibilité du code :

```
puts "Ok" if true
```

On peut également utiliser le `unless` en version post-fixée :

```
puts "Ok" unless false
```

### Cas complexes

Pour les cas plus complexes, on utilisera souvent la structure de contrôle `case` qui dans d'autres langages s'exprime avec le mot-clé `switch`.

En Ruby cette structure de contrôle est bien plus puissante. Elle ne se cantonne pas à vérifier une égalité simple pour chaque branche, elle permet d'embarquer des conditions évoluées :

```
case "Ceci est une chaîne"
when "foo"
	puts "Branche 1"
when 1..10
	puts "Branche 2"
when /une/
	puts "Branche 3"
else
	puts "Branche 4"
end
```

Quand on exécute ce code, c'est la branche 3 qui ressort. Pourquoi ?

La première branche permet de vérifier si la valeur testée est égale à la chaîne "foo".

La deuxième vérifie si cette valeur est un entier compris entre 1 et 10. C'est un `Range`, une classe livrée avec Ruby que nous découvrirons par la suite.

La troisième branche compare la valeur à l'expression rationnelle `/une/` délimitée par les slashs. Notre valeur contient bien la sous-chaîne "une" c'est pourquoi la branche 3 ressort.

La branche `else` est le cas par défaut qui est appelé si aucune des conditions précédentes n'a été satisfaite. Cette branche est facultative.

### Conclusion

Vous avez donc maintenant les bases pour mettre en place des structures de contrôle dans votre code Ruby. Ces structures constituent la base d'un programme et vous seront utiles au quotidien.


<div id="4"><h2>4- VARIABLES ET IDENTIFIEURS</h2></div>

### La théorie

En Ruby, les variables et autres identifieurs commencent généralement par une lettre. Les régles de bases sont simples.

Les variables locales commencent par une lettre ou un underscore. Commencer le nom d'une variable par un underscore permet d'avertir l'interpréteur que vous n'allez pas utiliser cette variable mais que c'est intentionnel. Ça évite donc d'avoir un message d'avertissement à l'exécution.

Les conventions en Ruby veulent que si une variable contient plusieurs mots, on les sépare par un underscore.

Des exemples de variables locales pourraient donc être :

```
user = "Nico"
_unused = "Non utilisé"
some_var = 1234
```

Il faut également distinguer des pseudo-variables qui sont générées automatiquement par l'interpréteur. Il s'agit de `self` qui représente l'objet courant ou encore `nil` qui est une instance de la classe `NilClass`.

Il y a également `__FILE__` et `__dir__` qui utilisés dans un fichier Ruby permettent d'obtenir respectivement le chemin absolu vers ce fichier ainsi que le chemin absolu vers le répertoire qui contient ce fichier. Au sein d'IRB ces deux variables n'ont pas réellement de sens.

Viennent ensuite les variables globales qui commencent obligatoirement par un `$`. Ces variables une fois définies sont accessibles à travers tout le programme, quelque soit le fichier dans lequel on se trouve et celui où elles sont définies. Ces variables sont à utiliser avec parcimonie car elles "polluent" l'ensemble du programme et dénotent très souvent un problème de conception.

Voici quelques exemples de variables globales :

```
$version = "1.2.6"
$NOT_A_CONST = 42
```

Nous avons ensuite les variables d'instances qui sont un type de variable très utilisé. Elles sont utilisées au sein d'un objet et représentent des données qui lui sont directement liées. Seul l'objet y a accès.

Ces variables d'instances commencent toujours par un `@` et suivent les mêmes conventions que les variables locales. Voici quelques exemples :

```
@foobar = "baz"
@some_var_123 = 123
```

Nous avons également les variables de classe qui contiennent des données accessibles à l'ensemble d'une classe et des ses instances. Ces variables sont partagées entre tous les objets issus de la classe en question. Les variables de classe commencent par deux `@`. Voici quelques exemples :

```
@@counter = 10
@@file_path = "/some/dir/file.txt"
```

Il reste pour finir les constantes qui doivent commencer par une lettre majuscule. Par convention, de nombreux rubyistes écrivent les constantes avec uniquement des lettres majuscules et séparent les éventuels mots par un underscore.

Les constantes sont destinées à stocker des informations qui ne sont pas appelées à être modifiées. Il faut tout de même être vigilant puisque pour des raisons techniques, il est possible en Ruby de modifier une constante existante. Ça n'empêchera pas le programme de fonctionner, l'interpréteur émettra simplement un message d'avertissement.

Voici quelques exemples de noms de constantes :

```
STATUSES = ["draft", "published", "pinned"]
API_URL = "http://something.com"
```

### En pratique

Dans la pratique, en Ruby, les développeurs aiment encapsuler les logiques métier dans des classes et c'est dans ce contexte qu'on travaille le plus et que nous utilisons ces différents types de variables.

Voyons donc un exemple dans le contexte d'une classe. Ne vous inquiétez pas, nous aurons l’occasion de voir plus en détail le fonctionnement des classes dans les prochains épisodes :

```
class User
	MIN_AGE = 18
	MAX_AGE = 90

	@@count = 0

	def initialize(name)
		@name = name
		@@count += 1
	end

	def self.instances_count
		@@count
	end
end
```

Nous avons donc définie deux constantes, une variable de classe ainsi qu'une variable d'instance qui est initialisée dans le constructeur, la méthode `initialize`.

Cette classe contient deux méthodes, le constructeur qui permet de préparer l'objet lorsqu'on crée une instance et une méthode de classe qui sert ici à retourner le nombre d'instances qui ont été créées par cette classe.

Pour finir utilisons cette classe nouvellement crée :

```
User.new("nico")
User.new("martin")
User.new("jon")

User.instances_count
```

On a donc créé trois instances de la classes `User` et c'est bien ce que nous confirme l'appel à la méthode de classe `instances_count`.

### Conclusion

Vous connaissez maintenant les différents types de variables et d'identifieurs à votre disposition ce qui vous permettra de stocker correctement les informations dans votre programme en fonction de leur contexte.


<div id="5"><h2>5- CREER UNE CLASSE</h2></div>

### La théorie

Ruby propose de base de nombreuses classes qui vous faciliteront le travail quotidien mais dans la plupart des cas, vous aurez besoin de créer vos propres classes.

L'intérêt d'une classe est de permettre d'encapsuler les comportements spécifiques à un objet métier et d'isoler sa logique du reste du code. Cette encapsulation va faciliter la maintenance et l'évolution des fonctionnalités liées à cet objet métier.

Comme vous avez pu le voir dans les épisodes précédents, une classe en Ruby se construit grâce au mot-clé `class` qui permet d'ouvrir une classe pour y définir des attributs et des méthodes.

Ce mot-clé `class` sera suivi du nom de la classe que vous voulez créer. Le nom de la classe est une constante et à ce titre il doit commencer par une majuscule.

Dans une classe on pourra stocker des constantes, des variables de classe, des variables d'instance, des méthodes de classe et des méthodes d'instance.

Les données stockées dans des variables de classe sont disponibles dans tous les objets de cette classe. Les données stockées dans des variables d'instance seront disponibles uniquement dans l'objet qui les a définies.

Il est intéressant de noter que puisqu'en Ruby tout est objet, les classes elles même sont des objets. Ce sont en fait des instances de la classe `Class`.

### La pratique

Créons une classe `Animal` qui permettra de gérer des animaux.

```
class Animal
  WILD = true

  @@counter = 0

  def initialize(name, sex, age)
    @@counter += 1
    @name, @sex, @age = name, sex, age
  end

  def description
    puts "#{@name} is #{@age} years old."
  end

  def self.instances_count
    puts "We created #{@@counter} animals."
  end
end
```

On a donc créé une classe dans laquelle on a définie une constante `WILD`, une variable de classe `@@counter` qui est initialisée à 0 directement dans la définition de la classe.

On a ensuite définie la méthode `initialize` qui sert de constructeur. Cette méthode est appelée automatiquement dès qu'une instance est allouée. On profite de cette méthode pour stocker nos différents paramètres dans des variables d'instance mais aussi pour incrémenter notre compteur. On aura donc un historique du nombre d'animaux qu'on a instancié.

On a également définie une méthode d'instance `description` qui aura pour but d'afficher des informations concernant l'animal, ici on ré-utilise nos variables d'instance `@name` et `@age` pour construire une phrase descriptive.

Finalement on a définie une méthode de classe `instances_count` qui est donc précédée par le mot-clé `self`. Cette méthode a pour but de nous informer sur le nombre d'instances qui ont été créées.

On va maintenant utiliser cette classe pour tester son comportement. On commence par charger notre fichier dans IRB grâce à la méthode `load`

```
load 'animal.rb'
```

On peut utiliser notre classe.

```
a1 = Animal.new('Simba', 'male', 5)
a2 = Animal.new('Cheetah', 'male', 20)

a1.description
a2.description
```

Vérifions maintenant le nombre d'instances créées :

```
Animal.instances_count
```

On peut également accéder à la constante depuis l'extérieur de la classe grâce à la notation `::` :

```
Animal::WILD
```

C'est très souvent utilisé pour accéder à la valeur depuis une autre partie du code.

### Conclusion

Vous connaissez maintenant les bases de la création d'une classe en Ruby. Vous allez donc pouvoir commencer à organiser votre code de façon plus modulaire. Il reste évidemment beaucoup d'autres choses relatives aux classes à découvrir pour prétendre les maitriser, c'est ce que nous verrons dans les prochains épisodes.


<div id="6"><h2>6- LES ACCESSEURS</h2></div>

### La théorie

Dans la vidéo précédente nous avons créé une classe basique qui permet de gérer des animaux.

Bien souvent vous aurez besoin de pouvoir modifier les propriétés d'une instance existante. Le fait d'avoir créé des variables d'instances ne suffit pas à pouvoir les lire ou les modifier depuis l'extérieur de la classe. Pour pouvoir accéder à ces variables d'instances depuis l'extérieur, que ce soit en lecture ou en écriture, vous devez écrire ce qui dans beaucoup de langage s'appelle les "getter" et les "setter".

### Les accesseurs

En Ruby ce sont les accesseurs. Ce sont des méthodes dédiées à la lecture ou à la modification du contenu d'une variable d'instance. Nous allons améliorer notre classe existante pour pouvoir lire et modifier le contenu de la variable d'instance `@age` :

```
class Animal
  WILD = true

  @@counter = 0

  def initialize(name, sex, age)
    @@counter += 1
    @name, @sex, @age = name, sex, age
  end

  def age
    @age
  end

  def age=(age)
    @age = age
  end

  def description
    puts "#{@name} is #{@age} years old."
  end

  def self.instances_count
    puts "We created #{@@counter} animals."
  end
end
```

On a donc ajouter la méthode `age` qui fait office de "getter", son but est simplement de retourner la valeur de la variable d'instance `@age`. On a également ajouté la méthode `age=` qui sert quant à elle de "setter". Elle va permettre de modifier le contenu de la variable d'instance `@age`. On note la présence du `=` dans le nom de méthode. Ce n'est absolument pas obligatoire mais par convention et pour améliorer la lisibilité, les Rubyistes ont pour habitude d'ajouter un `=` au noms de méthodes servant de "setter". Cette méthode prend un paramètre qui sera utilisé comme nouvelle valeur.

Testons cette classe améliorée :

```
load 'animal.rb'

a = Animal.new('Simba', 'male', 5)
a.age
a.description
a.age = 10
a.age
a.description
```

Ça fonctionne donc comme voulu, c'est satisfaisant sur le plan fonctionnel mais ce n'est pas du tout représentatif du code idiomatique à utiliser en Ruby. Ce besoin est tellement courant en Ruby qu’il met à notre disposition des macros permettant de faire ce travail à notre place.

On a donc à disposition trois méthodes qui sont `attr_reader`, `attr_writer` et `attr_accessor` qui permettent respectivement de créer un "getter", un "setter" ou les deux à la fois. On peut donc modifier notre classe pour la simplifier :

```
class Animal
  WILD = true

  @@counter = 0

  attr_accessor :age

  def initialize(name, sex, age)
    @@counter += 1
    @name, @sex, @age = name, sex, age
  end

  def description
    puts "#{@name} is #{@age} years old."
  end

  def self.instances_count
    puts "We created #{@@counter} animals."
  end
end
```

On a donc supprimer nos deux méthodes dédiées à la gestion de l'âge pour les remplacer par un appel à `attr_accessor` suivi du nom de la variable d'instance pour laquelle les méthodes doivent être générées.

On peut recharger notre code dans IRB et vérifier que ça fonctionne toujours. On remarque un message d’avertissement qui nous dit que nous avons redéfinie une constante. Effectivement le fait de recharger notre fichier a écrasé la constante définie lors du premier chargement :

```
load 'animal.rb'

a = Animal.new('Simba', 'male', 5)
a.age
a.description
a.age = 10
a.age
a.description
```

Le comportement est identique mais le code est plus concis et les risques de bugs sont donc réduits.

### Conclusion

Vous connaissez maintenant les bases de la création des accesseurs dans une classe en Ruby. Vous allez donc pouvoir améliorer vos classes existantes et mettre en place des méthodes permettant de manipuler vos attributs d'instances.


<div id="7"><h2>7- L'HERITAGE</h2></div>

### La théorie

Dans la vidéo précédente nous avons amélioré une classe existante qui permet de gérer des animaux.

Nous allons aujourd'hui apprendre à nous servir de l'héritage en Ruby.

L'héritage permet de créer une classe sur la base d'une autre pour en modifier certains aspects. Ça permet donc de refléter des comportements spécifiques qui ne peuvent pas être mis en commun dans la classe parent.

Imaginez que sur la base de notre classe `Animal` nous voulions créer des chiens mais aussi des chats. Le cri de chaque animal est différent et il est donc impossible de le mutualiser dans la classe `Animal`. C'est une méthode que nous devrons mettre en place spécifiquement dans chaque classe enfant. Pour autant on souhaite garder tous les comportements communs pour ne pas avoir à les ré-écrire. C'est ce que permet l'héritage.

### Mise en place de l'héritage

Nous allons donc créer notre première classe qui hérite de la classe `Animal`. Ce sera la classe `Dog`. Dans cette classe, nous allons créer une méthode qui permet à l'animal d'émettre son cri. En Ruby, l'héritage se fait grâce à l'opérateur `<` :

```
class Dog < Animal
  WILD = false

  def cry
    puts "Woof!"
  end
end
```

On a donc défini une classe `Dog` qui hérite de la classe `Animal`. De ce fait elle possède déjà tous les comportements de la classe `Animal` :

```
load 'animal.rb'
load 'dog.rb'

d = Dog.new('Snoopy', 'male', 10)
d.age
d.description
```

Mais cette classe possède également une nouvelle méthode qu'on peut appeler :

```
d.cry
```

Ce qui est impossible sur un objet de la classe `Animal` :

```
a = Animal.new('Simba', 'male', 5)
a.cry
```

Une exception `NoMethodError` est levée.

On voit également qu'on a redéfini la constante `WILD` parce que les chiens ne sont pas des animaux sauvages :

```
Dog::WILD
```

### Redéfinition de méthode

L'héritage laisse aussi la liberté de ré-écrire entièrement ou en partie des méthodes de la classe parent. On va donc modifier la description pour qu'elle soit plus personnelle :

```
class Dog < Animal
  WILD = false

  def cry
    puts "Woof!"
  end

  def description
    puts "I'm #{@name} the dog and I'm #{@age} years old!"
  end
end
```

On a donc complètement écrasé la définition du parent pour avoir un comportement personnalisé :

```
load 'dog.rb'

d = Dog.new('Snoopy', 'male', 10)
d.description
```

On aurait pu vouloir garder le comportement par défaut mais simplement y ajouter du comportement additionnel. C'est possible grâce au mot-clé `super` qui permet d'appeler la méthode correspondante du parent. Modifions notre classe :

```
class Dog < Animal
  WILD = false

  def cry
    puts "Woof!"
  end

  def description
    super
    puts "He's a dog."
  end
end
```

Testons à nouveau :

```
load 'dog.rb'

d = Dog.new('Snoopy', 'male', 10)
d.description
```

On a donc la méthode `description` de la classe `Animal` qui génère la première ligne, puis le méthode `description` de notre classe `Dog` qui génère la deuxième ligne.

### Conclusion

L'héritage est un moyen très flexible pour architecturer vos classes et éviter la redondance. C'est une notion qu'il est nécessaire de maîtriser si vous voulez vous attaquer à des projets ambitieux et bien encapsuler le comportement de chaque entité. Je vous invite donc à faire des essais de votre côté !


<div id="8"><h2>8- LA VISIBILITE DES METHODES</h2></div>

### La théorie

Lorsque vous écrivez une classe en Ruby, il est possible de limiter la visibilité de ses méthodes. Certaines méthodes sont conçues pour être utilisées directement par la classe, elle n'ont pas vocation à être utilisé à l'extérieur de celle ci. En limitant la visibilité, vous empêchez leur utilisation depuis l'extérieur.

Par défaut, les méthodes que vous ajoutez à une classe sont publiques, elle peuvent donc être appelées depuis l'extérieur. Les mots-clés `protected` et `private` permettent de modifier la visibilité des méthodes qui sont définies ensuite.

On a donc trois visibilités à disposition : `public`, `protected` et `private`.

### En pratique

#### Depuis la classe:

Écrivons une classe qui utilise les trois :

```ruby
class Visibility
  def public_method
    puts "public"
  end

  protected

  def protected_method
    puts "protected"
  end

  private

  def private_method
    puts "private"
  end
end
```

Voyons maintenant comment ces trois méthodes se comportent au sein de la classe en ajoutant deux méthodes qui les utilisent :

```ruby
def without_self
  public_method
  protected_method
  private_method
end

def with_self
  self.public_method
  self.protected_method
  self.private_method
end
```

Testons maintenant dans IRB :

```ruby
load 'visibility.rb'
visibility = Visibility.new
visibility.without_self
```

Les trois méthodes sont donc appelées sans le moindre problème avec un receveur implicite.

Testons maintenant la version utilisant les `self`

```ruby
visibility.with_self
```

Dans ce cas les méthodes publique et protégée sont bien appelées mais la méthode privée lève une exception `NoMethodError`.

Il est donc impossible d'appeler une méthode privé avec un receveur explicite, elle ne peut être appelée que sur l'objet courant.

#### À l'extérieur de la classe

Voyons maintenant comment ces méthodes se comportent depuis l'extérieur de la classe :

```ruby
visibility.public_method
```

La méthode publique peut, sans surprise, être appelée de l'extérieur.

```ruby
visibility.protected_method
visibility.private_method
```

Les méthodes protégée et privée lèvent quant à elles une exception `NoMethodError`. Il est donc impossible d'y faire appelle depuis l'extérieur. Elles ont une visibilité limitée et ne font pas partie de l'interface publique de la classe.

### Différence entre `protected`et `private`

Vous devez sûrement vous demander quelle est la différence entre les visibilités `protected` et `private`. Elle est subtile.

Si l'objet qui envoie le message, autrement dit qui appelle la méthode, est du même type que l'objet qui le reçoit alors il peut appeler une méthode protégée. Il reste impossible d'appeler une méthode privée même dans ce cas.

Voyons un exemple :

```ruby
class Extended < Visibility
  def call_methods(other)
    other.public_method
    other.protected_method
    other.private_method
  end
end

class NotRelated
  def public_method
    puts "public"
  end

  protected

  def protected_method
    puts "protected"
  end

  private

  def private_method
    puts "private"
  end
end
```

On ajoute une classe `Extended` qui hérite de `Visibility`. Cette classe implémente une méthode `call_methods` qui permet d'appeler nos trois méthodes mais sur un autre objet passé en paramètre.

Nous ajoutons également une classe `NotRelated` qui implémente nos trois méthodes mais qui n'a aucun lien avec nos deux classes précédentes.

On recharge notre fichier et on teste le comportement :

```ruby
e = Extended.new
e.call_methods(Visibility.new)
```

Les méthodes publique et protégée de l'objet `Visibility` ont pu être appelées depuis l'objet `Extended`. C'est possible car ces deux objets proviennent de la même classe parent :

```ruby
e.is_a?(Visibility)
```

Seule la méthode privée ne peut être appelée.

Essayons maintenant avec un objet qui n'a aucun lien :

```ruby
e.call_methods(NotRelated.new)
```

Ici seule la méthode publique peut être appelée, l'appel à la méthode protégée lève une exception `NoMethodError` car les deux objets ne font pas partie de la même hiérarchie :

```ruby
e.is_a?(NotRelated)
```

L'utilisation la plus fréquente pour les méthodes protégées est de permettre à deux objets du même type de coopérer. Par exemple pour écrire une méthode qui permet de comparer deux objets, disons des personnes et savoir qui est le plus âgé sans pour autant avoir accès publiquement à l'âge dans l'interface.

### Conclusion

Il est important de maîtriser le concept de visibilité des méthodes pour être en mesure d'écrire des classes avec une interface propre. Le plus souvent vous utiliserez des méthodes publiques et privées mais il reste essentiel de savoir utiliser les méthodes protégées pour permettre à vos objets de communiquer entre eux sans polluer l'interface publique.


<div id="9"><h2>9- LES BASES DE LA REFLEXION</h2></div>

### La théorie

La réflexion est la possibilité pour un programme d'analyser son environnement pendant l'exécution. Elle lui permet d'interroger les objets qui le compose et de les étendre ou de les modifier à la volée.

Les possibilités de réflexion en Ruby sont très avancées. Il est par exemple possible de créer des méthodes ou savoir si une variable existe pendant l'exécution. Ces possibilités ouvrent de nombreuses perspectives du point de vue du programmeur qui peut de ce fait créer des programmes très dynamiques qui réagiront de manière spécifique en fonction des conditions dans lesquels ils sont exécutés.

Un programme peut par exemple définir une méthode avec une implémentation complètement différente en fonction du système sur lequel il est exécuté.

Il sera également possible de définir des méthodes relatives à une structure de données qu'on ne connaît pas à l'avance mais qui est découverte au moment de l'exécution.

### En pratique

On peut par exemple utiliser le mot-clé `defined?` qui permet de savoir si un identifieur, une variable par exemple, existe dans le contexte courant :

```ruby
if defined?(some_var)
  puts "some_var = #{some_var}"
else
  puts "some_var n'existe pas"
end
```

De la même façon, la méthode `respond_to?` permet de savoir si un objet répond à une méthode donnée :

```ruby
s = "test"
s.respond_to? :size
s.respond_to? :foo
```

Il devient donc possible de mettre en place des mécanismes évolués dans le code puisqu'on peut interroger les objets à la volée pour savoir s'ils implémentent tel ou tel comportement. Nous n'avons plus besoin de connaître le type de l'objet à l'avance. Il nous suffit de nous renseigner à son sujet.

On peut, à l'exécution, obtenir la classe d'un objet :

```ruby
s.class
123.class
Array.new.class
```

On pourra également savoir si un objet est une instance d'une classe donnée : 

```ruby
s.instance_of?(String)
s.instance_of?(Object)
```

On peut étendre cette demande à l'objet ainsi que ses ancêtres :

```ruby
s.kind_of?(String)
s.kind_of?(Object)
s.kind_of?(Array)
```

Pour poursuivre, on peut récupérer une liste complète des méthodes qui peuvent être appelées sur l'objet :

```ruby
s.public_methods
s.protected_methods
s.private_methods
```

On peut aussi manipuler les variables d'instance de l'objet :

```ruby
s.instance_variables
s.instance_variable_set :@foo, "test"
s.instance_variables_get :@foo
```

Au niveau d'une classe, il est possible de connaître ses ancêtres et modules inclus :

```ruby
Array.ancestors
Array.included_modules
```

Le module `ObjectSpace` contient toutes les informations concernant les objets actuellement disponibles dans l'interpréteur :

```ruby
ObjectSpace.each_object { |o| p o }
ObjectSpace.count_objects
```

C'est notamment ce module qui permet de forcer le lancement du garbage collector, c'est à dire, le nettoyage en mémoire des objets non-utilisés.

Il permet aussi de définir un comportement à mettre en place lorsqu'un objet est détruit.

Finalement l'un des mécanismes les plus utilisés est la définition à la volée de méthodes.

Quand l'interpréteur recherche une méthode, il regarde si elle existe sur l'objet, puis sur la classe de l'objet et finalement si l'un de ses ancêtres la définie. Si elle n'est pas trouvée, Ruby va exécuter la méthode `method_missing` de l'objet si elle existe sinon, une exception `NoMethodError` sera levée :

```ruby
"test".foo

class String
  def method_missing(name, *args, &block)
    puts "La méthode #{name} n'existe pas"
  end
end

"test".foo
```

### Conclusion

Comme vous pouvez le voir, la réflexion est une fonctionnalité extrêmement puissante. On peut, en peu de lignes de code, rendre un programme très dynamique, auto-évolutif et faire en sorte qu'il sache prendre en charge des cas complexes ou des éléments du contexte d'exécution qui ne peuvent pas être connus à l'avance.

Je vous invite toutefois à faire attention à ne pas en abuser. Quand vous pouvez développer une fonctionnalité sans recourir à la méta-programmation, il faut faire sans. Le code qui est évalué et généré au moment de l'exécution sera forcément plus lent que le même code "statique".

Sachez que cette possibilité existe et qu'elle a beaucoup à offrir mais utilisez la avec parcimonie.


<div id="10"><h2>10- LES SYMBOLES</h2></div>

### La théorie

Les symboles sont l'un des éléments du langage les plus utilisés.

Un symbole est une instance de la classe `Symbol`. Pour en déclarer un il suffit d'utiliser les deux-points suivi par un identifieur.

Un symbole ressemble à une chaîne dans son fonctionnement et son usage. Mais contrairement aux chaînes, chaque symbole n'a qu'une seule instance et n'existe donc qu'une seule fois en mémoire :

```ruby
:foo.class

:foo.object_id
:foo.object_id

"foo".object_id
"foo".object_id
```

Il y a donc une différence importante entre ces deux types d'objets qui peut impacter la consommation mémoire ou les performances de votre programme.

Si on crée un tableau comme suit :

```ruby
array = ["foo", :foo, "foo", :foo, :foo]
```

Les deux chaînes "foo" seront des objets distincts en mémoire. Les symboles `:foo` sont quand à eux plusieurs références vers le même objet en mémoire. On peut voir ça comme un objet unique qui a un nom.

### Utilisation


#### Identifieur

L'utilisation la plus commune pour les symboles est de s'en servir pour représenter le nom d'une variable ou d'une méthode. Rappelez-vous dans les épisodes précédents nous avons vu comment ajouter des accesseurs à une classe, nous nous sommes servi de symboles à cette occasion :

```ruby
class Foo
  attr_accessor :something
end
```

Nous aurions très bien pu utiliser une chaîne à la place du symbole, ça aurait tout de même fonctionné. À vrai dire, la plupart des méthodes livrées avec Ruby qui attendent un symbole en argument savent aussi se débrouiller avec un chaîne.

Un symbole est finalement très proche d'un chaîne, il est composé par une suite de caractères. On peut considérer qu'un symbole est un peu comme une chaîne immuable. On peut d'ailleurs simuler le comportement d'un symbole à l'aide d'une chaîne :

```ruby
"foo".freeze.object_id
"foo".freeze.object_id
```

Le fait de geler la chaîne fait qu'elle n'est instanciée qu'une fois et représente toujours le même objet en mémoire.

Mais malgré ces similitudes, il ne faut pas s'y méprendre, les symboles et les chaînes sont des objets différents avec une interface publique différente. Les symboles n'héritent pas de la classe `String`.

```ruby
:foo.kind_of?(String)
```

Il est à noter qu'on peut créer des symboles contenant des caractères spéciaux en entourant l'identifieur de guillemets :

```ruby
:"identifieur peu commun !"
```

On pourrait donc créer des méthodes avec des noms barbares mais ce n'est pas une bonne idée.

#### Énumération

Une autre utilisation fréquente des symboles est de s'en servir pour créer des énumérations :

```ruby
STATUSES = [:draft, :published, :pinned]
NORTH, SOUTH, EAST, WEST = :north, :south, :east, :west
```

C'est plus expressif que d'utiliser, par exemple, des entiers pour définir les points cardinaux.

#### Méta-valeur

Un autre usage assez commun est d'utiliser les symboles comme des méta-valeurs. Ils vont donc pouvoir être utilisés comme code de retour de méthodes qui n'ont pas vocation à être des chaînes qui seront utilisées en tant que tel. C'est une fois encore plus expressif que de retourner des entiers.

### Conversion des symboles en chaîne et vice-versa

Il est très facile de convertir des symboles en chaîne et vice-versa. C'est pratique pour permettre à vos méthodes d'utiliser indépendamment l'un ou l'autre en tant que paramètre par exemple :

```ruby
"foo".to_sym
:foo.to_s

def hello_dude(name)
  puts "Hello #{name.to_s}!"
end

hello_dude("Nico")
hello_dude(:Nico)
```

### Génération de proc

La dernière utilisation commune pour les symboles permet de raccourcir les appels à des méthodes qui acceptent un bloc en paramètre. Disons par exemple qu'on veut capitaliser chaque mot d'un tableau, on pourrait faire :

```ruby
array = ["one", "two", "three"]
array.map { |word| word.capitalize }
```

mais Ruby permet de raccourcir cet appel très commun grâce à l'utilisation d'un symbole qui va permettre de générer le bloc à la volée :

```ruby
array.map(&:capitalize)
```

### Conclusion

Les symboles sont un des piliers de Ruby qu'il est important de maîtriser pour améliorer votre code mais aussi pour comprendre celui des autres. Désormais quand vous créerez une chaîne, demandez vous si c'est vraiment ce dont vous avez besoin. Allez-vous la manipuler en tant que tel ? Si la réponse est non, vous avez certainement besoin d'un symbole pour représenter cette valeur.


<div id="11"><h2>11- LA CLASSE TIME</h2></div>

### La théorie

La manipulation de dates et heures est une nécessité fréquente en programmation. Fort heureusement, en Ruby il est facile de manipuler ce type d'information.

Ruby met à notre disposition la classe `Time` qui permet de faire la majorité des manipulations inhérentes à ce type de données.

En interne, les objets de la classe `Time` sont stockés sous forme d'un entier qui représente le nombre de nano-secondes écoulées depuis ce qu'on appelle "Epoch" qui correspond au 1 janvier 1970 à minuit UTC.

Nous verrons dans une prochaine vidéo que les classes `Date` et `DateTime` apportent quelques outils supplémentaires qui améliorent la flexibilité.

### Création d'objets `Time`

La chose la plus fondamentale qu'on puisse vouloir faire est de connaître la date et l'heure courante :

```ruby
Time.new
```

Nous n'avons pas passé de paramètre à `new` c'est donc l'heure courante qui nous est retournée. Pour ce cas fréquent, il existe une méthode plus explicite :

```ruby
Time.now
```

Il existe plusieurs façon de créer des objets `Time`. Pour le fuseau horaire local, pour le fuseau horaire UTC et finalement pour un fuseau horaire arbitraire :

```ruby
Time.local(2015, 8, 12, 8, 15, 20)
Time.utc(2015, 8, 12, 8, 15, 20)
Time.new(2015, 8, 12, 8, 15, 20, "-05:00")
```

Les paramètres à passer vont de celui ayant la plus grande unité, l'année, à celui ayant la plus petite, la seconde. Seul l'année est un paramètre obligatoire :

```ruby
Time.local(2015, 8, 12, 8)
Time.local(2015, 8, 12)
```

Si vous tentez de créer une date invalide, disons avec un mois qui n'existe pas, vous auriez une exception `ArgumentError` qui serait levée :

```ruby
Time.local(2015, 13)
```

### Affichage des objets `Time`

De nombreuses méthodes sont mises à notre disposition pour manipuler ces dates :

```ruby
t = Time.local(2015, 8, 12, 8, 15, 20)
t.to_s
```

`to_s` nous retourne une version textuel de la date facilement compréhensible par un humain mais également simple à analyser avec un programme.

Il est également possible de formater la représentation à votre guise grâce à la méthode `strftime` :

```ruby
t.strftime("Printed on %d/%m/%Y")
t.strftime("at %H:%M")  
```

Les options de formatage sont très complètes et je vous invite à lire la documentation de `strftime` pour en avoir une liste exhaustive.

On peut par exemple utiliser le formatage suivant pour des dates compatibles ISO 8601 pour nos JSON :

```ruby
t.strftime("%FT%R")
```

### Les méthodes utilitaires

La classe `Time` nous livre aussi une panoplie de méthodes qui nous permettent de savoir si une instance correspond à un jour donné :

```ruby
t.monday?
t.tuesday?
t.wednesday?
t.thursday?
t.friday?
t.saturday?
t.sunday?
```

Nous avons aussi quelques méthodes qui nous permettent de récupérer le jour, le mois etc :

```ruby
t.day
t.month
t.year
t.hour
t.min
t.sec
t.usec
```

On peut également connaître le jour dans l'année que représente notre instance :

```ruby
t.yday
```

### Les fuseaux horaire

Nous avons également de quoi manipuler les fuseaux horaire. Quel est le fuseau horaire ?`

```ruby
t.zone
```

Est-ce que c'est une heure d'été ?

```ruby
t.dst?
```

Est-ce que c'est une heure UTC ?

```ruby
t.utc?
```

Convertir l'heure en heure locale

```ruby
t.getlocal
```

Convertir l'heure en heure UTC

```ruby
t.getutc
```

Quelle est le nombre de secondes de décalage entre mon heure et l'heure UTC ?

```ruby
t.utc_offset
```

### Arithmétique

Pour finir, il est également possible de faire de l'arithmétique sur les objets `Time` :

```ruby
t1 = Time.now
t2 = t1 + 60
```

On voit que `t2` est exactement une minute plus tard que `t1`, soit 60 secondes.

```ruby
t3 = t1 + 120

t1 != t2
t1 < t2

t2 - t1

t2.between?(t1, t3)
```

### Conclusion

La gestion des dates et heures en Ruby est donc quelque chose de très simple grâce à une panoplie de méthodes qui nous facilitent la vie.

Il devient facile d'écrire des méthodes de plus haut niveau pour manipuler de façon avancée ce type de données dans nos programmes. La librairie propose d'ailleurs les extensions `Date` et `DateTime` qui apportent encore plus d'aisance dans la manipulation.

D'autres librairies comme ActiveSupport vont encore plus loin et ajoutent encore plus de naturel dans la manipulation des dates.


<div id="12"><h2>12- LES CLASSES DATE ET DATETIME</h2></div>

### Les classe `Date` et `DateTime` et leurs motivations

La classe `Date` a été créée pour manipuler spécifiquement des dates sans tenir compte de l'heure. La classe `DateTime` quant à elle a été écrite pour apporter quelques méthodes manquantes à la classe `Time`, pour mieux cadrer la validation des dates et heures, gérer les différents types de calendriers et faciliter les analyses.

Il faut savoir qu'historiquement, avant Ruby 1.9, la classe `Time` était plus pauvre et limitée dans les valeurs possibles. Il n'était possible de gérer que des dates allant approximativement de 1901 à 2038.

Depuis la gestion des dates a été revue et le fossé entre la classe `Time` et `DateTime` a largement été réduit. Toutefois `DateTime` apporte encore quelques méthodes supplémentaires. Il est en parti possible de les reproduire dans la classe `Time` grâce à un `require 'time'`.

Les classes `Date` et `DateTime` partagent de nombreuses fonctionnalités et on va donc les présenter en parallèle.

### Pratique

Avant toute chose, il faut charger les classes `Date` et `DateTime` :

```ruby
require 'date'
```

#### Création de dates

On peut maintenant les utiliser :

```ruby
d = Date.today
dt = DateTime.now
```

On peut bien évidemment créer des dates arbitraires :

```ruby
Date.new(2015, 9, 15)
DateTime.new(2015, 9, 15, 8, 10, 30, '+7')
```

On peut aussi créer des dates sur la base de la semaine calendaire et le jour de la semaine en lieux et place des jour et mois absolus :

```ruby
Date.commercial(2015, 5, 6)
```

On peut également créer une date sur la base du jour de l'année :

```ruby
Date.ordinal(2015, 34)
```

Il nous est également possible de faire de la validation de date :

```ruby
Date.valid_date?(2015,2,3)
Date.valid_date?(2015,2,29)
```

#### Analyse des dates sous forme de chaînes

L'analyse de dates sous forme de chaînes est également facilité.

Là où la classe `Time` sera perdue :

```ruby
Time.new("2015-08-05")
```

La classe `Date` sera elle capable d'une analyse assez avancée :

```ruby
Date.parse("2015-08-05")
Date.parse("05/08/2015")
DateTime.parse("01/12/2015 09:43")
```ruby

La classe va même nous apporter quelques méthodes permettant d'analyser des formats de date répandus :

```ruby
DateTime.httpdate("Wed, 26 Aug 2015 15:13:02 GMT")
DateTime.iso8601('2015-02-03T08:10:30+07:00')
DateTime.rfc2822('Sat, 3 Feb 2015 04:05:06 +0700')
```

Si nous devons aller plus loin en supportant nos propres formats, c'est également possible :

```ruby
Date.strptime('03-02-2015', '%d-%m-%Y')
Date.strptime('2015!034', '%Y!%j')
```

Le template de format utilise ici la même syntaxe que `strftime` que nous avons déja vu.

#### Arithmétique sur les dates

Comme pour la classe `Time`, les classes `Date` et `DateTime` nous permettent de faire de l'arithmétique :

```ruby
d + 1
d.next_day

d - 5
d.prev_day(5)

d << 2
d.prev_month(2)
d >> 2
d.next_month(2)

d.prev_year(2)
d.next_year(2)

other_date = Date.new(2015, 8, 2)
d - other_date
d <=> other_date
```

#### Affichage et formattage des dates

Pour ce qui est de l'affichage des dates, nous avons également tout le nécessaire :

```ruby
dt.asctime
dt.to_s
dt.httpdate
dt.iso8601
dt.rfc2822
dt.strftime("%T%:z")
```ruby

Il nous est possible de récupérer le détail des éléments qui composent une date :

```ruby
dt.day
dt.month
dt.year
dt.hour
dt.min
dt.sec
```ruby

```ruby
d.cwday
d.cweek
d.yday
```

Une fois encore il nous est possible de savoir si la date correspond à un jour donné de la semaine :

```ruby
d.monday?
d.wednesday?
```

Au besoin, il est également possible de convertir un objet d'un type vers un autre :

```ruby
d.to_datetime
dt.to_date
dt.to_time
```

Finalement il nous est possible de parcourir des périodes pour y faire des traitements divers et variés :

```ruby
other_date.upto(d).count { |d| d.sunday? } 
d.downto(other_date).count { |d| d.sunday? } 
other_date.step(d, 2).count { |d| d.sunday? }
```

### Conclusion

Comme vous avez pu le voir ici, les classes `Date` et `DateTime` apportent les dernières briques qui permettent de manipuler très naturellement des dates et heures.

C'est une base solide pour l'écriture de méthodes de manipulation de plus haut niveau. Rails, par exemple, les utilise très largement pour manipuler les dates et heures en base de données et bien plus encore.



<div id="13"><h2>13- LA CLASSE ARRAY</h2></div>

### Les déclarations

Nous avons vu qu'il est possible de créer un tableau avec la notation `[]` :

```ruby
a = []
```

Mais il est également possible d'utiliser la syntaxe classique `Array.new` qui peut prendre de zéro à deux arguments :

```ruby
a = Array.new(3)
a = Array.new(3, "foo")
```

Dans le premier cas notre tableau est initialisé à la taille spécifiée avec des éléments vides. Dans le deuxième cas, chaque élément représente ce qui est passé en deuxième argument.

Attention au piège, le tableau contient en fait des références à cet élément, pas des copies. Si vous en modifiez un, vous les modifierez tous :

```ruby
a[0].capitalize!
a
```

Si vous souhaitez que chaque élément soit un objet unique plutôt que de multiples références au même objet, il faut utiliser la syntaxe prenant un bloc :

```ruby
a = Array.new(3) { "foo" }
a[0].capitalize!
a
```

### Sélection et remplacement d'éléments

Il est courant de vouloir récupérer un ou plusieurs éléments en début ou fin de tableau, pour ce faire des méthodes nous facilitent la tâche :

```ruby
a.first
a.first(2)
a.last
a.last(2)
```

On sait qu'on peut également récupérer un élément à un index donné grâce à la notation `[index]` :

```ruby
a[0]
```

Mais on peut également récupérer un jeu d'éléments grâce à deux autres notations :

```
a[1, 2]
a[1..2]
```

La première demande de commencer la récupération à l'index "1" sur une longueur de deux éléments.
La seconde utilise un `Range` pour demander de récupérer les éléments des index 1 à 2 compris.

On peut se servir de cette même notation pour faire de l'affectation :

```
a[1, 2] = ["bar", "baz"]
a

a[1..2] = [2, 3]
a
```

On peut également récupérer plusieurs éléments éparpillés sur des index non-contiguës en une seule opération :

```
a = [10, 20, 30, 40, 50, 60]
a.values_at(0, 1, 4)
a.values_at(0..2, 5)
```

Une fois encore, on a utilisé un `Range`.

Il est également possible de récupérer le premier ou dernier éléments du tableau en le supprimant à la volée ce qui transforme notre tableau en pile :

```ruby
a_dup = a.dup
a_dup.shift
a_dup
a_dup.pop
a_dup
```

### Compter les éléments

Une autre opération commune est de vouloir compter le nombre d'éléments d'un tableau ou d'un sous-ensemble, plusieurs possibilités s'offrent à nous :

```ruby
a.size
a.count
a.count { |el| el > 30 }
```

La méthode `size` est la plus simple mais aussi la plus rapide puisqu'elle vérifie simplement la taille en mémoire du tableau.

La méthode `count` quant à elle est plus puissante puisqu'elle autorise un bloc qui va servir de filtre. Cette méthode est par contre plus lente puisqu'elle parcourt l'ensemble du tableau pour donner le résultat.

On va également pouvoir savoir si un tableau est vide ou s'il contient des éléments :

```ruby
a.empty?
a.any?
a.any? { |el| el > 100 }
```

Là encore, la méthode `any?` autorise un bloc de filtrage.

### Tri et recherche

La classe `Array` propose aussi de nombreuses méthodes permettant de faire du tri ou de la recherche :

```ruby
a.shuffle!
a.sort
a.sort { |a, b| b <=> a }
a.sort.reverse

b = ['Nico', 'Victor', 'Jon', 'Martin']
b.sort_by { |el| el.length }
b.sort_by { |el| [el.length, el] }
```

On peut rechercher le premier élément du tableau qui rempli une condition :

```ruby
a.find { |el| el > 20 }
```

ou tous les éléments qui remplissent la condition :

```ruby
a.find_all { |el| el > 20 }
```

Il existe également la méthode permettant de retourner tous les éléments qui ne répondent pas à la condition :

```ruby
a.reject { |el| el > 20 }
```

Dans la même veine nous avons la méthode `grep` qui permet de faire des recherches sur la base d'expressions rationnelles :

```ruby
b.grep(/ic/)
```

On peut éventuellement lui passer un bloc de transformation :

```ruby
b.grep(/ic/) { |el| el.length } 
```

On peut également rechercher les valeurs minimales et maximales :

```ruby
b.min
b.max
b.max { |a, b| a[1..-1] <=> b[1..-1] }
```

### Manipulation diverses

Finalement vous pourriez vouloir regrouper les éléments de deux tableaux, deux par deux, c'est ce que propose la méthode `zip` :

```ruby
c = a.zip(b)
```

et construire une chaîne en concaténant ces éléments :

```ruby
c.join("-")
```

### Conclusion

Nous avons vu ici la majeur partie des possibilités livrées par la classe `Array`, l'ensemble de ses méthodes devraient sans nul doute vous donner toutes les clés pour pouvoir effectuer vos manipulations. Nous avons volontairement omis quelques méthodes plus exotiques. Jetez un œil à la documentation si vous êtes curieux.

Quelques méthodes supplémentaires très pratiques sont mises à disposition par le module `Enumerable` que nous découvrirons plus tard.


<div id="14"><h2>14- MANIPULER DES CHAINES DE CARACTERES</h2></div>

### Les déclarations 

Les chaînes peuvent être déclarées de différentes façons. Tout d'abord avec des guillemets simples ce qui créera la chaîne telle quelle sans transformation, il faudra simplement penser à échapper les guillemets simples :

```ruby
puts 'Ceci est une chaîne'
puts 'Aujourd\'hui'
```

On peut ensuite créer des chaînes en utilisant des guillemets doubles qui apportent plus de puissance puisqu'on pourra utiliser d'autres séquences d'échappement, des tabulations, retours à la ligne, etc. On pourra également interpoler des variables au sein de la chaîne :

```ruby
puts "Une tabulation (\t)"

s = "Nico"
puts "De l'interpolation #{s}"
```

Il existe également des moyens alternatifs de représenter les chaînes qui deviennent pratique quand la chaîne contient beaucoup de guillemets ou de caractères d'échappement :

```ruby
puts %q(Une chaîne avec des '', des "" et des "\t" et #{s})
puts %Q(Une chaîne avec des '', des "" et des "\t" et #{s})
```

La version minuscule correspond donc à une chaîne à guillemets simples alors que la version majuscule correspond à une chaîne à guillemets doubles.

Pour déclarer les très longues chaînes, les "Here-Documents" sont là pour nous aider. C'est très utile lorsqu'on souhaite créer une chaîne qui s'étend sur plusieurs lignes :

```ruby
puts <<EOF
une chaîne sur
plusieurs lignes
EOF
```

La chaîne doit donc commencer par deux chevrons suivi d'un identifieur. Cet identifieur sera ré-utilisé pour signifier la fin de la chaîne.

### Les utilitaires de la classe `String`

Voyons maintenant les méthodes utiles de la classe `String`. 

Souvent vous aurez besoin de connaître la longueur d'une chaîne :

#### Comptage

```ruby
s.length
```

Ou connaître le nombre d’occurrences d'une sous-chaîne dans la chaîne :

```ruby
s.count("a")
s.count("a-i")
s.count("^a-i")
```

#### Parcourir

On pourra également vouloir parcourir du texte, ligne par ligne :

```ruby
s = <<EOF
Première ligne
Deuxième ligne
Troisième ligne
EOF

s.each_line do |line|
  puts line.chomp + " !"
end
```

Ou encore caractère par caractère :

```ruby
s = "Ruby is awesome!"
s.each_char do |char|
  print char + "-"
end
```

Il sera assez fréquent de vouloir comparer deux chaînes pour savoir laquelle est la plus "grande", on pourra le faire en tenant compte de la casse ou non :

```ruby
"ab" <=> "AB"
"ab".casecmp("AB")
```

#### Découpage

On peut également découper notre chaîne sur l'espace, un caractère quelconque ou encore une expression rationnelle :

```ruby
s.split
s.split("e")
s.split(/\W+/)
```

On pourra même limiter le nombre de champs retournés :

```ruby
s.split(/\W+/, 2)
```

La méthode `scan` quant à elle va permettre de nous retourner un tableau des éléments qui répondent à une expression rationnelle donnée :

```ruby
s.scan(/\w+/)
s.scan(/\w+/) { |w| print "<<#{w}>> " }
```

#### Formater

Ceux qui ont fait du C doivent sans nul doute connaître la fonction `sprintf` qui existe aussi en Ruby et permet un formatage puissant des chaînes :

```ruby
name = "Nico"
age = 34

sprintf("Salut %s, tu as déjà %d ans…", name, age)
```

Jusque là rien de bien épatant, une simple chaîne avec interpolation aurait fait l'affaire. Mais `sprintf` va bien plus loin dans ses possibilités :

```ruby
sprintf("Salut %-20s, tu as déjà %03d ans…", name, age)
```

On peut également ajuster notre texte à l'affichage :

```ruby
name.ljust(15)
name.center(15)
name.rjust(15)
name.center(15, "-")
```

ou encore gérer la casse :

```ruby
s.downcase
s.upcase
s.capitalize
s.swapcase
```

#### Accéder et assigner des sous-chaînes

En Ruby, il est également très facile de travailler avec des sous-chaînes. On peut à la fois accéder à des sous-chaînes mais également les modifier.

D'abord on y accède avec la notation [index de départ, longueur] :

```ruby
s[0, 4]
s[-8, 7]
```

Puis à l'aide de `Range` :

```
s[0..3]
s[-8..-2]
```

L'utilisation d'expressions rationnelles est également possible :

```ruby
s[/a.*e/]
```

On peut également utiliser l'ensemble de ces notations pour accéder à une sous-chaîne et la modifier :

```ruby
s[/a.*e/] = "yummy"
s
```

#### Rechercher dans une chaîne

Il y d'autres façon de faire des recherches dans une chaîne qui conviendront mieux en fonction du cas d'utilisation :

```ruby
s.index("m")
s.index(/.y/)

s.rindex("m")
s.rindex(/.y/)

s.include?("a")
s.include?("uby")
```

On peut aussi obtenir un tableau des occurrences grâce à la méthode `scan` :

```ruby
s.scan("m")
s.scan(/.y/)
```

#### Manipulation diverses

Dans la série des inclassables, il nous reste quelque méthodes à connaître. 

D'abord la possibilité de supprimer un caractère donné dans une chaîne :

```ruby
s.delete("u")
```

Il y a également la possibilité d'avoir la suite logique d'une chaîne :

```ruby
"R2D2".succ
```

Et finalement la possibilité de répéter une chaîne :

```ruby
etc = "Etc. " * 3
```

### Conclusion

Nous avons vu ici la majeur partie des possibilités livrées par la classe `String` qui, de base, est très bien fournie. Ce n'est pas un tour exhaustif des méthodes et de leurs possibilités mais le principal est là. Si vous êtes curieux, je vous conseille de jeter un œil à la documentation.


<div id="15"><h2>15- LES EXPRESSIONS RATIONNELLES, PARTIE 1</h2></div>

### La théorie

Les expressions rationnelles peuvent être déclarées grâce une paire de slashes, avec la notation `%r` ou encore grâce à `Regexp.new` :

```ruby
s = "Ruby"
/Ruby/ =~ s
/[Rr]uby/ =~ s
%r(^abc) =~ s
Regexp.new("xyz%") =~ s
```
 
Il est possible d'utiliser des modifieurs pour modifier le comportement de l'expression rationnelles :

```ruby
/ruby/i =~ "Ruby"
```

Il existe beaucoup d'autres ancres et modifieurs utilisables dans les expressions rationnelles. Une bonne compréhension vous apportera beaucoup de bénéfices dans vos développements.

Faire le tour des possibilités prendrait bien plus de temps qu'on en a pour cette vidéo mais heureusement la documentation officielle de la classe `Regexp` est particulièrement exhaustive.

C'est un sujet tellement vaste que des livres entiers sont consacrés au sujet.

### En pratique

#### Les échappements

Vous voudrez parfois rechercher des caratères qui correspondent à des caractères spéciaux dans les expressions rationnelles. Il faudra donc les échapper.

Vous pourrez les échapper à la main :

```ruby
/./ =~ s
/\./ =~ s
```

mais dans les cas plus complexes, il est préférable d'utiliser la méthode `escape` :

```ruby
Regexp.escape("[*?]")
```

#### Début et fin de chaînes, de lignes et de mots

Les expressions rationnelles sont un bon moyen de détecter les débuts et fin de chaînes, de lignes et de mots.

Chercher un motif en début de ligne utilisera l'ancre "^", pour la fin de ligne on utilisera "$" :

```ruby
s = "abc def ghi"
/abc/ =~ s
/def/ =~ s
/^def/ =~ s
/def$/ =~ s
/ghi$/ =~ s
```

Si on remplace les espaces par des retours à la ligne, les résultats seront différents :

```ruby
s = "abc\ndef\nghi"
/abc/ =~ s
/def/ =~ s
/^def/ =~ s
/def$/ =~ s
/ghi$/ =~ s
```

D'autres ancres nous permettent de rechercher en début et fin de chaîne sans prendre en compte les retours à la ligne :

```ruby
s = "abc\ndef\nghi"
/\Aabc/ =~ s
/\Adef/ =~ s
/def\Z/ =~ s
/ghi\Z/ =~ s
```

On ne cherche donc plus en début ou fin de ligne mais bien en début et fin de chaîne ce qui est tout à fait différent.

De la même façon, on peut repérer les limites des mots ou au contraire tout ce qui n'en est pas :

```ruby
s = "Ruby is awesome"
s.gsub(/\b/, "|")
s.gsub(/\B/, "-")
```

### Conclusion

Les expressions rationnelles sont donc un moyen très puissant d'analyser du texte mais c'est aussi un outil assez difficile à prendre en main. Nous n'avons qu'effleuré les possibilités dans cette vidéo. 

La vidéo suivante nous permettra d'en apprendre un peu plus.


<div id="16"><h2>16- LES EXPRESSIONS RATIONNELLES, PARTIE 2</h2></div>

Bienvenue dans cette vidéo qui fait suite à la découverte de l'utilisation des expressions rationnelles en Ruby.

Nous n'avons la dernière fois pu voir que les bases et nous allons donc essayer d'aller plus loin dans cette nouvelle vidéo.

Continuons donc notre découverte dans IRB.

### Les quantificateurs

Vous aurez souvent besoin de gérer des motifs optionnels ou répétés. Les quantificateurs vous permettent de gérer ça.

On peut par exemple définir un ou plusieurs caractères optionnels, il pourront donc apparaître une fois ou pas du tout :

```ruby
re1 = /ax?b/
re2 = /a[xy]?b/

re1 =~ "ab"
re1 =~ "azb"
re1 =~ "axb"

re2 =~ "ayb"
re2 =~ "acb"
```

On peut également rechercher un caractère qui apparaît au moins une fois :

```ruby
re = /[0-9]+/
re =~ "1"
re =~ "8765432"
```

On peut simplifier cette expression avec l'ancre dédiée à la recherche de numériques :

```ruby
/\d+/ =~ "123"
```

Il est très fréquent de vouloir définir un motif qui peut apparaître de zéro ou une infinité de fois :

```ruby
re = /Yeah!*/
re =~ "Yeah"
re =~ "Yeah!!!!"
```

On peut préciser le nombre d’occurrences qu'on attend :

```ruby
re = /\d{3}-\d{2}-\d{2}/
re =~ "123-45-67"
re =~ "1-45-67"
```

On pourra aussi définir un nombre d’occurrences variable :

```ruby
re = /\d{1,3}-\d{2}-\d{2}/
re =~ "123-45-67"
re =~ "1-45-67"
```

Il faut savoir que les quantificateurs "*", "+" et "{}" sont gourmands par défaut, ils vont essayer de récupérer la plus grande partie de la chaîne qui correspond :

```ruby
s = "Il est à la fois le plus petit et le plus grand"
/.*le/.match(s)
```

Pour n'attraper que la plus petite occurrence, il faut demander à l'opérateur de ne pas être gourmand grâce au "?" :

```ruby
/.*?le/.match(s)
```

### Les groupes

Dans une expression rationnelle, il est possible de créer des groupes ré-utilisables. Chaque groupe pour lequel on a une correspondance sera donc accessible ensuite pour utilisation.

#### Les groupes simples

Un groupe est créé en utilisant les parenthèses :

```ruby
"Ruby".sub(/(.)(.)(.)(.)/, '<\4> <\3> <\2> <\1>')
```

Pour chaque groupe qui aura une correspondance, on obtient un identifieur spécial. On a dans notre exemple quatre jeux de parenthèses et donc les identifieurs de 1 à 4.

La méthode `match` permet d'aller plus loin en retournant un objet `MatchData` :

```ruby
s = "alpha beta gamma delta epsilon"
re = /(b[^ ]+) (g[^ ]+) (d[^ ]+)/
md = re.match(s)
md[1]
md[2]
md[3]
md[0]
md.begin(2)
md.pre_match
md.post_match
```

#### Les groupes nommés

Vous aurez sûrement remarqué qu'il faut compter les groupes pour savoir qui correspond à quoi. Ce n'est pas toujours pratique. Heureusement, Ruby nous permet de mettre en place des groupes nommés :

```ruby
re = /(?<beta>b[^ ]+) (?<gamma>g[^ ]+) (?<delta>d[^ ]+)/
md = re.match(s)
md[:beta]
```

Il suffit donc de commencer le groupe par un point d'interrogation suivi d'un identifieur entre chevrons. On peut ensuite faire référence au groupe grâce à cet identifieur.

L'écriture est plus longue mais la lisibilité est considérablement augmentée.

### Recherche en avant

Dans les expressions rationnelles il est possible de faire de la recherche en avant (lookahead) pour ne les valider que si elles sont suivies ou non par un motif précis. Ce motif ne sera pas retourné dans notre résultat :

```ruby
s1 = "J'aime le Ruby"
s2 = "J'aime le PHP"
s3 = "J'aime le Javascript"

re = /J'aime le (?=Ruby|Javascript)/
re.match(s1)
re.match(s2)
re.match(s3)
```

On voit donc que l'expression n'est vérifiée que si elle est suivi par le mot "Ruby" ou "Javascript".

On peut également faire l'inverse, à savoir ne valider que si ce qui suit ne correspond pas :

```ruby
re = /J'aime le (?!Ruby|Javascript)/
re.match(s1)
re.match(s2)
re.match(s3)
```

Ici seule les correspondances n'étant pas suivies par les mots "Ruby" ou "Javascript" seront validées.

### Recherche en arrière

Il est également possible de faire le même type d'opérations mais en revenant en arrière (lookbehind).

L'utilisation de cette technique est plus difficile à décrire par un cas pratique. Ça pourrait être pour modifier du contenu dans un langage balisé après analyse de ses balises ou encore pour analyser des séquences ADN.

Je vais donc reprendre un exemple d'utilisation connu pour nécessiter les recherches en arrières.

Imaginons que vous vouliez retrouver dans une séquence ADN, toutes les séquences nucléotidiques, de quatre éléments donc, qui suivent un "T". On ne pourrait pas simplement chercher le "T" puisqu'on ne serait plus capable de détecter deux séquences contiguës si la première finie par un "T". Pour illustrer cela utilisons la séquence suivante :

```ruby
adn = "GATTACAAACTGCCTGACATACGAA"
adn.scan(/T(\w{4})/)
```

Il manque donc la séquence "GACA" qui suit la séquence "GCCT" qui est elle même une des correspondances.

En utilisant la recherche arrière, on pourrait palier à ce problème en demandant de vérifier également le caractère précédent :

```ruby
adn.scan(/(?<=T)(\w{4})/)
```

### Conclusion

Les expressions rationnelles permettent donc des recherches très avancées. Ça sera parfois la seule solution à votre problématique.

Il faut par contre avoir conscience qu'elles sont des opérations coûteuses. Si vous pouvez vous en passer votre programme n'en sera que plus réactif.

Pour continuer l'exploration, je vous invite à tester des expressions dans votre console et à lire attentivement la documentation de la classe `Regexp`.


<div id="17"><h2>17- LES ENTREES SORTIES</h2></div>

Bienvenue dans cette vidéo consacrée à la découverte des entrées / sorties en Ruby. Les entrées / sorties sont souvent appelées I/O de l'anglais Input / Output.

La gestion des entrées / sorties est une des bases de la programmation. Même si vous n'en avez pas conscience parce que vous utilisez un framework, vous les utilisez sans cesse. Les usages sont d'une variété quasi infinie.

Aujourd'hui, nous nous pencherons uniquement sur les fichiers classiques, stockés sur un support. Ça nous permettra de creuser le sujet dans les vidéos suivantes.

### Théorie

En Ruby, toute la gestion des entrées / sorties repose sur la classe `IO`. C'est la classe qui définie les comportements communs à toutes les entrées / sorties.

De cette classe découle la classe `File` qui encapsule tous les détails de la gestion de fichiers tels que les permissions, les dates de création, etc.

C'est sur ces fondements que sont réalisées d'autres classes et librairies qui vont permettre de persister des éléments dans des fichiers ou dans des bases de données.

### Ouvrir / fermer des fichiers

Commençons donc à travailler avec les fichiers qui sont le moyen le plus simple et le plus commun pour stocker de l'information persistante.

Les opérations les plus communes sont l'ouverture et la fermeture des fichiers. Entre deux on lira ou écrira des informations.

Pour ouvrir un fichier on utilisera la méthode `File#new` qui prend en premier paramètre le chemin vers le fichier à ouvrir et en deuxième paramètre optionnel le mode d'ouverture.

Le mode d'ouverture sert à indiquer si on ouvre le fichier en lecture, en écriture, en lecture et écriture, etc.

On peut donc ouvrir un fichier en écriture :

```ruby
file1 = File.new("one", "w")
```

ou en lecture:

```ruby
file2 = File.new("one")
```

Quand vous ouvrez des fichiers, il est de bon ton de les fermer une fois que vous avez fini de les utiliser. Si vous ouvrez de nombreux fichiers et que vous les laissez tous ouverts, le système finira par se plaindre.

D'ailleurs si vous ne fermez pas un fichier dans lequel vous avez écrit, il est fort probable que vous perdiez une partie des données.

Fermons donc nos deux fichiers précédemment ouverts :

```ruby
file1.close
file2.close
```

Pour ouvrir des fichiers, vous pouvez également utiliser la méthode `File#open` qui est plus ou moins un synonyme de `File#new` à ceci près que vous pouvez lui passer un bloc et le fichier sera automatiquement fermer à la fin de ce bloc :

```ruby
File.open("test.txt", "w") do |file|
  file.puts "Line 1"
  file.puts "Line 2"
  file.puts "Line 3"
end
```

C'est sans aucun doute la façon la plus élégante de procéder. Nous avons donc ouvert en écriture le fichier "test.txt", qui a été créé s'il n'existait pas.

Nous avons ensuite appelé la méthode `puts`. Nous l'avons déjà largement utilisé jusqu'ici pour afficher des valeurs à l'écran. Par défaut `puts` s'applique sur la sortie standard, ce qui dans la plupart des cas est la console dans laquelle le script est exécuté.

Ici c'est différent, nous l'appelons explicitement sur la variable locale `file` qui représente le fichier que nous avons ouvert ce qui a pour effet d'écrire les chaînes dans ce fichier.

### Mettre à jour un fichier

Si vous veniez à ouvrir à nouveau le même fichier, toujours avec le mode "w", vous écraseriez le contenu existant.

Pour mettre à jour un fichier existant, il faut utiliser le mode adéquat. Pour pouvoir lire et écrire dans un fichier, il suffit d'ajouter "+" derrière le mode utilisé. Il reste maintenant à choisir le mode en fonction de ce que vous souhaitez faire.

Pour mettre à jour un fichier, en partant du début, on utilisera le mode "r+" :

```ruby
f1 = File.new("one", "r+")
```

Pour écraser le contenu du fichier existant ou en créer un nouveau, on utilisera "w+" :

```ruby
f2 = File.new("one", "w+")
```

Finalement pour compléter le fichier, en partant donc de la fin de ce dernier, on utilisera le mode "a+" :

```ruby
f3 = File.new("one", "a+")
```

Notez que les "+" ne sont pas nécessaire à la mise à jour, ils ne sont là que pour indiquer qu'on souhaite pouvoir lire **et** écrire. On pourrait très bien se cantonner à un simple "a" pour faire de la mise à jour de fichier.

### Accès aléatoires

Naturellement quand vous lirez un fichier, la lecture se fera de manière séquentielle. Ce sera donc caractère par caractère ou ligne par ligne.

```ruby
File.open("test.txt", "r") do |file|
  puts file.getc
  puts file.gets
end
```

Pour vous déplacer à un endroit précis, il faudra utiliser la méthode `IO#seek` qui attend qu'on lui passe un entier représentant le nombre de bytes dont on veut avancer dans le fichier :

```ruby
File.open("test.txt", "r") do |file|
  file.seek 7
  puts file.gets
end
```

On a donc avancé de 7 bytes pour passer la première ligne qui contient la chaîne "Line 1" constituée de 6 caractères plus un retour à la ligne ce qui nous permet d'arriver directement à la deuxième ligne.

Par défaut la méthode `IO#seek` commence toujours en début de fichier, on peut aussi lui demander de commencer à la position actuelle en lui passant un deuxième paramètre :

```ruby
File.open("test.txt", "r") do |file|
  file.seek 7
  puts file.gets

  file.seek 0
  puts file.gets

  file.seek 7
  puts file.gets

  file.seek 0, IO::SEEK_CUR
  puts file.gets
end
```

On peut également commencer depuis la fin de fichier grâce à la constante `IO::SEEK_END`.

#### Entrée / sortie par défaut

Comme on l'a expliqué un peu plus tôt, par défaut, les méthodes `Kernel.puts` et `Kernel.gets` si elles sont appelées sans receveur vont tenter d'écrire sur la sortie standard et de lire depuis l'entrée standard.

Ce phénomène s'explique par le fait que l'interpréteur lorsqu'il est lancé met à disposition trois constantes `STDIN`, `STDOUT` et `STDERR`. Ces constantes sont automatiquement affectées à trois variables globales qui sont `$stdin`, `$stdout` et `$stderr`.

Quand vous appelez `puts`, vous appelez en fait implicitement `$stdout.puts`. De la même manière en faisant `gets`, vous faites en réalité un `$stdin.gets`.

En ré-assignant ces variables globales, vous pouvez modifier le comportement par défaut de `puts`, `gets` et autres méthodes similaires ce qui peut se révéler très pratique.

Créons un script dans notre éditeur :

```ruby
file = File.new("io.txt", "w")
puts "Hello"

$stdout = file
puts "Bye"

$stdout = STDOUT
puts "Done"
```

Nous pouvons maintenant l'exécuter en console : `ruby io.rb`

On voit que sur la sortie standard apparaissent les chaînes "Hello" et "Done". Si on consulte le contenu du fichier "io.txt", on voit qu'il contient la ligne "Bye" : `cat io.txt`

#### Gestion des arguments

Une autre constante très utile lorsqu'on écrit des scripts est `ARGF`. Elle contient le contenu des fichiers qui ont été passés au script lors de son lancement.

On pourrait par exemple écrire un script qui affiche le contenu de ces fichiers :

```ruby
puts ARGF.read
```

Puis le lancer : `ruby cat.rb test.txt io.txt`

Plutôt simple n'est-ce pas ?

Une autre constante spéciale existe et permet de lister les arguments passés au script :

```ruby
ARGV.each do |arg|
  puts arg
end
```

On le lance : `ruby args.rb foo bar baz`

C'est un élément indispensable pour quiconque souhaite écrire des scripts.

#### Lire l'entrée standard

Une autre tâche dont vous aurez souvent besoin si vous écrivez des scripts sera de pouvoir lire des entrées utilisateur. Pour ce faire, il nous suffira d'écouter ce qu'il se passe sur `$stdin` :

```ruby
puts "Il y a de l'écho ici !"

while line = $stdin.gets
  puts "echo: " + line.chomp
end
```

On le lance : `ruby echo.rb`

On a donc créé une boucle infinie qui attend une entrée utilisateur puis la répète.

#### Conclusion

Vous connaissez donc maintenant les bases de la manipulation des entrées / sorties. Ces quelques bases vous permettent d'aller déjà assez loin dans l'interaction entre votre script et le système ou l'utilisateur.

Dans les prochaines vidéos nous approfondirons ces concepts pour apprendre à manipuler les attributs des fichiers, travailler avec les fichiers temporaires, les répertoires ainsi que la persistance d'objets.


<div id="18"><h2>18- LES ATTRIBUTS DE FICHIER</h2></div>

Bienvenue dans cette vidéo consacrée à la manipulation des attributs avancés des fichiers. Les usages que nous verrons ici sont particulièrement destinés à des scripts s'exécutant sur des systèmes de type Unix.

### Bloquer les fichiers

Dans vos scripts système il sera parfois nécessaire de bloquer l'accès à un fichier pour éviter qu'un autre processus tente par exemple de le modifier pendant que vous vous en servez.

Plusieurs modes de blocage sont disponibles, ils correspondent à ce qui est mis à disposition par la commande Unix `flock`.

On peut donc bloquer le fichier en mode partagé (`LOCK_SH`) pour lequel plusieurs processus pourront accéder au fichier en parallèle. Aussi longtemps qu'il existera des processus accédant au fichier dans ce mode, il sera impossible d'obtenir un blocage exclusif (`LOCK_EX`).

Le blocage exclusif va lui permettre d'obtenir un accès unique au ficher, souvent pour y écrire. Si d'autres processus veulent accéder au fichier en mode partagé, ils devront attendre que le blocage exclusif soit levé.

On peut en plus ajouter le drapeau `LOCK_NB` aux deux premiers modes. Dans ce cas si un processus tente d'accéder au fichier, une exception sera levé, ça sera impossible. Il n'y aura pas de système de mise en attente de la levée du blocage.

Finalement lorsqu'un processus a fini d'utiliser un fichier, il est de son devoir de lever le blocage grâce au drapeau `LOCK_UN`.

En Ruby, on utilisera ces concepts de la manière suivante :

```ruby
file = File.new("foo", "w")

file.flock(File::LOCK_EX)
file.flock(File::LOCK_UN)

file.flock(File::LOCK_SH)
file.flock(File::LOCK_UN)

file.close
```

Pour faire une analogie, vous pouvez imaginer un prof devant son tableau. Le tableau correspond à notre fichier.

Pendant que le prof écrit au tableau, il y pose un blocage exclusif. Pendant ce temps, personne ne peut le lire. Aucun autre blocage partagé ou exclusif ne peut être obtenu.

Lorsqu'il a fini, le prof s'écarte du tableau et lève le blocage exclusif. Les étudiants peuvent maintenant lire le tableau, c'est à dire accéder au fichier, en y posant un blocage partagé. On peut poser plusieurs blocages partagés en parallèle.

Pendant que des élèves lisent le tableau, il est impossible pour le professeur de le modifier en y posant un blocage exclusif.

### Appartenance et permissions

Il sera également courant de vouloir manipuler l'appartenance des fichiers et les permissions associées.

On pourra tout d'abord vouloir vérifier qui est le propriétaire ou le groupe d'un fichier :

```ruby
s = File.stat("foo")
s.uid
s.gid
```

C'est en fait ici l'identifiant de l'utilisateur et du groupe qu'on obtient. Pour obtenir le nom correspondant il faut passer par le module `Etc` :

```ruby
Etc.getpwuid(s.uid).name
Etc.getgrgid(s.gid).name
```

On va pouvoir, de la même façon, récupérer les permissions associées au fichier :

```ruby
s.mode
```

Par défaut, les permissions sont affichées en mode octal, on peut obtenir un affichage plus classique à l'aide de `sprintf` :

```ruby
sprintf("%o", s.mode)
```

Bien que très standard, cet affichage n'est pas le plus pratique à exploiter, on a donc un ensemble de méthodes qui nous permettent d'obtenir les information plus clairement :

```ruby
s.readable?
s.writable?
s.executable?
```

Bien évidemment il existe aussi des commandes pour modifier les permissions, le propriétaire et le groupe. Vous serez toutefois limité par les permissions de l'utilisateur courant :

```ruby
file = File.new("foo")
file.chmod(0444)
file.chown(502, 20)
```

### Gestion des informations d'horodatage

Lorsque vous utilisez un fichier des horodatages sont mis-à-jour. Depuis Ruby vous pouvez récupérer trois données, la date de dernier accès qu'on appelle "access time", la date de dernière modification appelée "modify time" et finalement la date de la dernière modification, changement de propriétaire ou de permissions inclus, c'est ce qu'on appelle le "change time".

Ces informations peuvent être obtenues directement depuis la classe "File", depuis une instance de cette même classe via des méthodes dédiées, ou encore à travers les informations de la méthode `stat` :

```ruby
File.mtime("foo")

file.mtime
file.atime
file.ctime

s = file.stat
s.atime
```

En plus de la consultation, il est possible de définir les heures de modification et changement en passant par la méthode `utime` :

```ruby
today = Time.now
yesterday = today - 86400
File.utime(today, yesterday, "foo")
```

### Existence et taille des fichiers

Une autre tâche fréquente en administration système que vous voudrez pouvoir automatiser au travers de vos script Ruby est la vérification de l'existence de fichiers et de leur taille.

Vérifions donc l'existence de quelques fichiers :

```ruby
File.exist?("foo")
File.exist?("bar")
```

Bien que notre fichier existe, il est peut-être vide et nous sera donc tout aussi inutile. Ruby met à notre disposition une méthode qui permet de vérifier si le fichier existe **et** s'il n'est pas vide :

```ruby
File.size?("foo")
File.size?("args.rb")
```

Si le fichier existe et qu'il n'est pas vide, sa taille nous est retournée.

Dans la même veine, la méthode `zero?` nous permettra de savoir si le fichier existe et qu'il est vide :

```ruby
File.zero?("foo")
File.zero?("args.rb")
File.zero?("bar")
```

Il est à noter que l'objet `stat` disponible sur l'instance d'un fichier dispose lui aussi des méthodes `size?` et `zero?`.

Il existe bien évidemment la méthode plus directe `size` qui se contentera de donner la taille du fichier. Si le fichier passé en argument n'existe pas, une exception sera levée :

```ruby
file.size
File.size("foo")
File.size("bar")
```
### Caractéristiques spéciales des fichiers

Finalement vous voudrez peut-être pouvoir consulter les caractéristiques spéciales des fichiers.

Vous pourrez par exemple vouloir savoir si un fichier est un terminal :

```ruby
$stdin.tty?
file.tty?
```

Comme tout est fichier sous Unix, il est intéressant de connaître son type :

```ruby
File.file?("foo")
File.directory?("/tmp")
File.pipe?("foo")
File.socket?("foo")
```

Plutôt que de tirer à l'aveuglette quand vous ne connaissez pas le type probable du fichier, vous pouvez passer par la méthode `ftype` :

```ruby
File.ftype("/dev/disk0s1")
```

### Conclusion

Ces quelques pointeurs vous permettront sans aucun doute de vous lancer dans l'écriture de scripts d'administration et de gestion du système de fichier.

Pour compléter vos compétences, nous verrons dans le prochain épisode comment manipuler les fichiers temporaires ainsi que les chemins et répertoires.


<div id="19"><h2>19- FICHIERS TEMPORAIRES ET REPERTOIRES</h2></div>

### Les fichiers temporaires

Dans bien des cas, vous serez amené à manipuler des fichiers temporaires pour stocker de l'information. C'est par exemple nécessaire lorsqu'on écrit une librairie qui gére les envois de fichier.

Quand on crée un fichier temporaire, on veut s'assurer que son nom est unique et qu'il sera bien effacé lorsqu'on aura fini de s'en servir. Biensûr il est possible de gérer ça soit même en écrivant le code nécessaire mais ça peut être fastidieux et sujet à erreur surtout si vous souhaitez avoir un code portable.

Heureusement, Ruby met à notre disposition la classe `Tempfile` dédiée à la gestion de cette opération courante :

```ruby
temp = Tempfile.new("foo")
temp.path
```

Un fichier avec un nom unique, commençant par "foo" a donc été créé dans le répertoire temporaire du système. Ce nom est garanti unique à travers les threads et le processus.

```ruby
temp.puts "On ajoute une ligne"
temp.close

temp.open
temp.gets
temp.close!
```

Si nous n'avions pas détruit le fichier, il l'aurait été automatiquement en fin de processus. Il est recommandé de le faire explicitement pour éviter que le fichier temporaire reste disponible sur le système de fichier jusqu'à ce qu'il soit collecté alors qu'il n'est plus utilisé par notre programme.

Si votre programme stocke des données sensibles qui ne doivent pas être accessibles aux autres processus, vous pouvez supprimer le fichier juste après sa création. Sur les systèmes POSIX, tant que le descripteur du fichier n'est pas clos, vous pouvez toujours vous en servir même s'il n'est plus visible sur le système de fichier :

```ruby
file = Tempfile.new("bar")
file.unlink
file.puts "Fichier toujours accessible"
file.close
```

### Manipuler les chemins

Un autre besoin récurrent est de manipuler les chemins de fichiers. On pourra vouloir connaître le répertoire correspondant :

```ruby
f = File.open("args.rb")
path = f.path

File.dirname(path)
```

Ou simplement le nom du fichier avec ou sans son extension :

```ruby
File.basename(path)
File.basename(path, ".rb")
```

On peut donc préciser l'extension à occulter, quand on ne la connaît pas à l'avance, on pourra utiliser l'étoile.

On va également pouvoir obtenir un chemin absolu depuis un chemin relatif :

```ruby
File.expand_path("~")
```

ou recomposer un chemin depuis ses différents composants en respectant le séparateur du système courant :

```ruby
File.join("usr", "local", "bin")
```

La classe `Pathname` a pour but de regrouper toutes ces fonctionnalités et permet également d'aller un peu plus loin :

```ruby
pn = Pathname.new(path)
pn.directory?
pn.file?
pn.split
pn.extname
pn.size
```

Cette classe offre beaucoup d'autres méthodes très utiles et je vous invite à lire sa documentation. Vous pourrez par exemple pour un répertoire connaître son parent et ses enfants.

### Manipuler les répertoires

Finalement, en plus d'analyser les chemins, on voudra pouvoir se déplacer dans les répertoires, en créer, en supprimer, etc.

Tout d'abord on pourra se renseigner sur le répertoire courant :

```ruby
Dir.pwd
```

puis se déplacer dans un autre :

```ruby
Dir.chdir("Desktop")
Dir.pwd
```

Cette méthode peut prendre un bloc bien pratique puisque le changement de répertoire ne sera effectif qu'à l'intérieur du bloc :

```ruby
Dir.chdir("..") do
  puts Dir.pwd
end
puts Dir.pwd
```

On pourra également lister l'ensemble des entrées d'un répertoire :

```ruby
Dir.chdir("..")
Dir.foreach(".") do |item|
  puts item
end
```

Dans certains cas, on préférera simplement récupérer cette liste sous forme d'un tableau :

```ruby
Dir.entries(".")
```

On va maintenant s'attacher à gérer les répertoires en Ruby en commençant par en créer un :

```ruby
Dir.mkdir("rep_1")
```

Plutôt simple mais comment créer une chaîne de répertoire ? Comme vous le savez sûrement, il est impossible de créer un répertoire si son parent n'existe pas. Il faudrait donc créer les répertoires de la chaîne un par un pour assurer un bon déroulé. C'est un peu fastidieux et Ruby met donc à notre disposition une méthode qui peut le faire pour nous :

```ruby
FileUtils.mkdir_p("rep_2/rep_3/foo/bar")
```

Parfait on peut maintenant passer au renommage d'un fichier et par extension d'un répertoire :

```ruby
FileUtils.mv("rep_1", "rep_10")
```

Pour finir, on voudrait pouvoir supprimer un répertoire. Avec la méthode de base on ne pourra supprimer qu'un seul répertoire à la fois et seulement s'il est vide. S'il n'est pas vide, une exception sera levée :

```ruby
Dir.delete("rep_10")
```

Bien souvent c'est un répertoire et l'ensemble de son contenu que vous voudrez supprimer récursivement. Ruby met à disposition une méthode nous évitant d'avoir à écrire un code fastidieux :

```ruby
FileUtils.rm_r("rep_2")
```

### Conclusion

Vous savez donc maintenant vous déplacer à travers le système de fichier, lister les entrées, en créer et en supprimer.

Vous avez pu voir en bonus comment mettre en place des fichiers temporaires de manière robuste ce qui vous permettra de stocker de l'information qui n'a pas vocation à être conservée et qui ne doit pas être accessible par un autre processus.

Le prochain épisode vous donnera les clés pour sérialiser et persister des objets Ruby dans des fichiers.


<div id="20"><h2>20- SERIALISATION ET PERSISTANCE</h2></div>

Nous verrons aujourd'hui comment persister des objets Ruby sur le disque pour pouvoir les ré-utiliser plus tard.

Plusieurs possibilités s'offrent à nous pour arriver à nos fins.

La brique la plus simple mise à notre disposition est la classe `Marshal`.

### Persistence simple avec Marshal

Dans la plupart des cas, le besoin sera de pouvoir sauver de manière permanente des objets que vous avez créé pendant le cycle de vie de votre programme. Vous pourrez donc, en le relançant plus tard, récupérer ses informations pour les restituer à l'utilisateur ou continuer un traitement.

On pourrait par exemple vouloir gérer une structure consistant en un tableau à deux dimensions. Disons un tableau de chansons, pour chaque chanson on aurait un tableau contenant, l'auteur, le titre et la durée.

Une fois ce tableau construit on voudra le sauver sur le disque pour y accéder à nouveau plus tard.

Mettons cet exemple en pratique. On crée donc notre tableau de musiques :

```ruby
songs = [
  ['Metallica', 'Nothing else matters', 389],
  ['Metallica', 'Sad but true', 325],
  ['Born of Osiris', 'The other half of me', 212]
]
```

On va maintenant créer un fichier pour stocker les informations :

```ruby
File.open("songs", "w") do |f|
  # Et y sérialiser les informations
  Marshal.dump(songs, f)
end
```

On pourra ensuite récupérer ses informations pour s'en servir :

```ruby
File.open("songs") do |f|
  songs = Marshal.load(f)
end
```

Comment faire plus simple ?

Malheureusement cette méthode ne permettra pas de sérialiser tout et n'importe quoi. Les classes de bas niveau ne sont pas sérialisables. On ne pourra pas, par exemple, sérialiser des objets issus des classes `IO` ou `Proc`. Les singletons, classes anonymes ou encore les modules ne peuvent pas non plus être sérialisés.

Vous pouvez par contre sérialisé sans souci vos classes maisons pour peu qu'elles n'embarquent pas un objet de bas niveau.

### Persistence améliorée avec PStore

Avec la classe `Marshal`, vous devez gérer un certain nombre de détails pour vous assurer que vos données persistées restent dans un état cohérent. Si un problème survient en milieu d'exécution, vous risquez d'avoir un fichier corrompu.

Pour faciliter la gestion de ce type de problématiques, Ruby met à disposition la classe `PStore`. Un objet `PStore` peut gérer une hiérarchie d'objets Ruby sous forme de clés / valeurs. La grande différence avec la classe `Marshal` est qu'un objet `PStore` va écrire ses changements sur le disque de façon transactionnel.

Lorsqu'un jeu de données sera modifié tout sera donc modifié avec succès ou sinon rien ne sera modifié. On évite donc de se retrouver avec des données dans un état transitoire sur le disque.

`PStore` se basant sur la classe `Marshal`, il est à noter que les mêmes limitations s'appliquent en ce qui concerne ce qui peut être sérialisé ou pas.

Voyons un exemple d'utilisation :

```ruby
require "pstore"

db = PStore.new("users")
db.transaction do
  db[123] = { name: "Nico", age: 34 }
end
```

Plus tard, nous pourrons récupérer ces informations :

```ruby
db2 = PStore.new("users")
db2.transaction { puts db2[123] }
```

Il est à noter qu'il est possible d'interrompre une transaction à tout moment, soit en conservant les changements effectués jusque là grâce à la méthode `commit`, soit en annulant les changements en utilisant la méthode `abort`.

Tous les changement qui suivront dans la transaction seront ignorés :

```ruby
db2.transaction do
  db2[1] = "test"
  db2.commit
  db2[2] = "foo"
end

db2.transaction do
  p db2[1]
  p db2[2]
end
```

On a donc enregistré les changements qui précédaient le `commit` mais pas les suivants. On aurait pu tout annuler avec `abort` :

```ruby
db2.transaction do
  db2[3] = "foo"
  db2.abort
  db2[4] = "bar"
end

db2.transaction do
  p db2[3]
  p db2[4]
end
```

On voit donc qu'ici rien n'a été persisté.

### Persistance avec YAML

Un autre format de persistance dont vous avez peut-être déjà entendu parler est YAML. L'avantage de ce format de stockage est qu'il est parfaitement lisible par une personne.

Le fait de charger la librairie "yaml" aura pour effet d'apporter une méthode `to_yaml` à chaque objet. Il devient alors possible de sérialiser des instances des classes de bases mais aussi de vos propres classes dans un format facilement compréhensible et exploitable.

Créons une classe simple pour illustrer l'utilisation :

```ruby
class Foo
  def initialize(a, b, c)
    @a, @b, @c = a, b, c
  end
end

foo = Foo.new("test", 123, {a: "foo", b: "bar", c: "baz"})
foo.to_yaml
```
On peut donc sauver ces données dans un fichier comme on le ferait pour stocker n'importe quelle autre chaîne :

```ruby
File.open("data.yml", "w") do |f|
  f.write(foo.to_yaml)
end
```

Voyons à quoi ressemble ce fichier :

```bash
cat data.yml
```

On pourra recharger ces informations plus tard de la manière suivante :

```ruby
file = File.new("data.yml")
YAML.load(file)
```

On a donc à nouveau une instance de la classe `Foo` à disposition. Elle contient les mêmes informations que lors de la sauvegarde.

Ce format de stockage est très apprécié des Rubyistes, notamment pour sa facilité d'édition.

### Stockage clés / valeurs avec DBM

Finalement, une autre option intéressante est la librairie DBM qui est un système de stockage sous forme de ficher basé sur des paires de clé / valeur. Ce sera donc un très bon moyen de persister vos `Hash`.

Il est à noter que les clés et les valeurs doivent être des chaînes. Hormis cela, un objet `DBM` se comporte de la même manière qu'un `Hash` et répond à quasiment toutes ses méthodes :

```ruby
require "dbm"

d = DBM.new("dbm")
d["foo"] = "bar"
d.close

d["foo"]

d2 = DBM.open("dbm")
d2["foo"]
d2.to_hash
d2.close
```

### Conclusion

Vous avez donc maintenant toutes les clés pour travailler avec les entrées sorties et vous pourrez largement en tirer partie dans vos programmes pour améliorer leurs qualités fonctionnelles.


<div id="21"><h2>21- LES THREADS EN RUBY</h2></div>

### Introduction aux threads

Les threads aussi appelés «processus légers» sont un moyen très pratique d'exécuter du code en parallèle sans avoir à lancer un nouveau processus qui serait plus coûteux.

Il faut savoir que les threads en Ruby ne sont pas des threads système mais des threads utilisateur qui fonctionnent indépendamment du système hôte. C'est bien sûr moins performant mais aussi plus portable.

Les threads vous seront particulièrement utiles lorsque vous avez des morceaux de code qui peuvent fonctionner de manière indépendantes ou pour gérer une partie du code qui passe la plupart de son temps à attendre des événements.

Si votre logique métier fonctionne de manière sérialisée alors les threads ne vous aideront pas. Ils ne seront également pas très pratiques si vous devez synchroniser l'accès à de nombreuses données globales.

Sachez qu'un code multi-threadé sera toujours plus sujets aux bugs qu'une version sans threads et qu'il compliquera le débogage.

Il faut donc savoir analyser le besoin, le contexte et le gain potentiel avant de choisir de multi-threader un programme.

### Création et manipulation de threads

Les bases de l'utilisation des threads consiste à en créer, y faire transiter de l'information puis les stopper. On pourra évidemment obtenir une liste des threads, leur état actuel, etc.

#### Créer un thread

Pour créer un thread, il suffit d'utiliser la classe dédiée :

```ruby
thread = Thread.new do
  # something
end
```
On obtient donc en retour une instance de la classe `Thread` qui peut être manipulée depuis le thread principal.

On pourra passer des arguments à un thread lors de sa création :

```ruby
Thread.new("foo", "bar") do |a, b|
  puts a
end
```

Il faut savoir qu'un thread a accès au contexte courant, il peut donc modifier le contenu des variables qui lui sont accessibles au moment de la création. C'est un vrai piège auquel il faut faire attention :

```ruby
a = "foo"
b = "bar"

Thread.new(a) do |a|
 a = "not changed"
 b = "changed"
end

a
b
```

La variable locale `a` qui est passée au thread sous le nom de `a` n'est impactée que localement, par contre la variable `b` qui n'a pas été passée localement est accessible depuis le contexte global. En la modifiant, on modifie sa valeur au niveau global.

#### Accéder aux variable locales des threads

Il est donc clair qu'il est dangereux d'utiliser des variables du contexte extérieur depuis un thread. On voudra pourtant parfois pouvoir passer des données au contexte global depuis notre thread. Heureusement des mécanismes sont mis à notre disposition pour pouvoir faire ça proprement :

```ruby
thread = Thread.new do
  t = Thread.current
  t[:foo] = "Here is foo"
  t[:bar] = 42

  baz = "Not available outside"
end

thread[:foo]
thread[:bar]
thread.key?(:foo)
thread.key?(:baz)
```

On peut donc depuis notre thread, communiquer de l'information à l'extérieur sans polluer le contexte global. C'est beaucoup plus propre ! Ne passez __jamais__ par les variables du contexte global pour communiquer de l'information ou vous vous exposerez à de gros soucis.

#### Connaître et changer le statut d'un thread

La classe `Thread` met à notre disposition des méthodes qui nous permettent d'interroger et de modifier le statut d'un thread donné.

On peut récupérer la liste des threads vivants grâce à la méthode de classe `list` ou encore obtenir une référence vers le thread principal via la méthode de classe `main`. La méthode de classe `current` nous retournera une référence vers le thread en cours d'exécution comme on a pu le voir avant :

```ruby
Thread.current == Thread.main

Thread.new do
  puts Thread.list.size
  puts Thread.current == Thread.main
end

Thread.list.include?(Thread.main)
```

D'autres méthodes vont nous permettent de modifier ou de connaître le statut d'un thread :

```ruby
t1 = Thread.new { loop {} }

t1.status
t1.kill
t1.alive?
t1.stop?
```

On voit que si le thread est en cours d'exécution son statut sera `run`, s'il est en attente à cause d'un `sleep` ou de l'attente d'un retour d'une entrée / sortie alors il sera en statut `sleep`. S'il a fini son travail avec succès le statut sera `false` et `nil` si une exception a été levée.

On est donc en mesure de savoir où en est le déroulement de nos différents thread et donc, par extension, de notre programme principal.

Pour les cas plus complexe, il sera possible de forcer un thread à passer la main à un moment précis de son exécution avec la méthode `pass`, de lui demander d'arrêter son exécution grâce à la méthode `stop` puis de la reprendre plus tard en utilisant la méthode `run` ou encore `wakeup` qui réveillera le thread sans forcer son exécution immédiate.

Pour autant, il ne faudra pas se servir de ces mécanismes pour tenter de faire de la synchronisation. D'autres techniques sont mises à notre disposition spécialement pour ça.

#### Attendre la fin d'exécution d'un thread

Dans bien des cas, vous aurez besoin de faire en sorte que votre programme attende que vos threads aient fini leur travail pour rendre la main. Vous pourriez mettre en place cette vérification dans votre thread principal grâce aux méthodes vues précédemment mais ça deviendrait vite fastidieux.

Fort heureusement, une méthode prête à l'emploi nous est fournie, elle s'appelle `join`. Si cette méthode est appelée sur un thread, le programme principal ne rendra pas la main tant que le thread en question n'aura pas fini son exécution.

Il est donc assez commun, avant la fin de son programme principal de mettre en place un idiome qui permet de s'assurer que tous les threads de l'application ont fini leur travail :

```ruby
Thread.list.each { |t| t.join if t != Thread.main }
```

On a donc listé tous les threads disponibles dans l'application et pour chacun d'entre eux, on a appelé `join` qui garantit que le programme ne peut pas rendre la main avant la fin de leur exécution.

On a simplement ajouté un test qui n'appelle pas `join` sur le thread principal qui serait alors incapable de se terminer.

### Conclusion

Nous avons pu voir dans cet épisode que Ruby met à notre disposition une base solide d'outils qui nous permettent de mettre en place de la concurrence et donc de gagner du temps précieux de traitement lorsqu'une autre partie du programme est en attente d'éléments pour continuer.

Dans l'épisode suivant, nous verrons comment synchroniser les threads entre eux pour assurer la cohérence des données.


<div id="22"><h2>22- SYCHRONISER LES THREADS</h2></div>

Nous verrons cette fois ci comment synchroniser la manipulation des données entre les différents threads. En effet, si aucune synchronisation n'est mise en place il se pourrait que les différents threads se marchent sur les pieds en modifiant une même variable. Les modifications de l'un serait donc écrasées et perdues par l'autre.

C'est ce qu'on appelle avoir un code "thread-safe" qui assure qu'un code qui va être manipuler par plusieurs threads en même temps se comportera comme attendu.

### Démonstration par l'exemple

Voyons un exemple que j'ai déjà écrit pour gagner du temps :

```ruby
x = 0

10.times.map do |i|
  Thread.new do
    puts "avant ajout (#{i}): #{x}"
    x += 1
    puts "après ajout (#{i}): #{x}"
    puts
  end
end.each(&:join)

puts "valeur finale : #{x}"
```

Comme vous le voyez, quand chaque thread démarre, il récupère la valeur courante de `x` pour l'afficher. Ensuite il tente d'ajouter 1 à cette valeur mais le résultat obtenu est variable du fait du traitement en parallèle de cette même variable par plusieurs threads concurrents.

Sans synchronisation, il devient impossible de prédire l'état de la variable `x` et par extension, le comportement de notre méthode. Le résultat retourné sera parfois correct et parfois erroné…

Il faut donc porter une attention particulière aux variables ayant une portée plus large que le thread dans lequel elles sont utilisées.

### Atomicité

Pour obtenir un code thread-safe, il va falloir travailler de manière atomique. Si nos opérations de modifications des valeurs sont faîtes de telle façon que les autres threads ne peuvent ni les lire, ni les écrire pendant qu'on travaille dessus, alors notre code sera thread-safe.

Pour gérer un ensemble d'opération de façon atomique, il nous faut utiliser les `Mutex` dont le rôle est de garantir que les opérations sont traitées d'une traite, comme un ensemble indivisible.

### Notre code thread-safe

Modifions donc notre code pour le rendre thread-safe. Pour cela il suffit d'encapsuler l'ensemble du code à jouer de manière atomique dans un bloc dédié.

Voyons le code :

```ruby
x, mutex = 0, Mutex.new

10.times.map do |i|
  Thread.new do
    mutex.synchronize do
      puts "avant ajout (#{i}): #{x}"
      x += 1
      puts "après ajout (#{i}): #{x}"
      puts
    end
  end
end.each(&:join)

puts "valeur finale : #{x}"
```

Ce simple ajout nous suffit à éviter bien des problèmes et à assurer que notre bloc d'instruction est joué en une seule fois sans être interrompu par un autre thread.

### De l'utilisation d'un code thread-safe

Il ne suffit pas d'utiliser des librairies thread-safe pour que le code qui les utilise le soit aussi. En fait, vous pouvez tout à fait écrire un code non thread-safe lorsque vous utiliser une librairie ou une classe qui l'est.

Prenons par exemple la classe suivante :

```ruby
class Counter
  attr_reader :count

  def initialize
    @count = 0
    @mutex = Mutex.new

    puts 'Counter created'
  end

  def increment!
    @mutex.synchronize { @count += 1 }
  end
end
```

Cette classe est thread-safe puisqu'elle utilise un `Mutex` pour incrémenter atomiquement la valeur.

Créons maintenant une application qui l'utilise :

```ruby
class Application
  def increment!
    counter.increment!
  end

  def counter
    @counter ||= Counter.new
  end

  def count
    counter.count
  end
end

app = Application.new

10.times.map do |i|
  Thread.new { app.increment! }
end.each(&:join)

puts app.count
```

Si on lance plusieurs fois cette application, on notera que parfois son résultat est erroné. Elle devrait toujours renvoyer 10.

Cette application n'est pas thread-safe pour une seule raison, elle initialise l'instance de `counter` grâce à l'opérateur `||=`. Cet opérateur n'est pas atomique. Il va d'abord lire la valeur puis la modifier après coup si nécessaire. Cette valeur a donc pu changer entre temps.

Dans les cas où notre application se comporte anormalement, c'est parce que plusieurs threads ont vu le contenu de la variable `counter` égale à `nil`. Ils ont donc voulu l'initialiser.

En réalité l'un des threads s'occupait déjà de l'initialisation, l'autre thread a ré-initialiser cette variable et écrasé l'existante.

On a donc créé une application qui n'est pas thread-safe sur la base d'une classe qui l'est. Il faut donc être vigilent.

La meilleure façon d'écrire notre application aurait été la suivante :

```ruby
class Application
  attr_reader :counter

  def initialize
    @counter = Counter.new
  end

  def increment!
    counter.increment!
  end

  def count
    counter.count
  end
end
```

L'idée est donc d'éviter que notre instance de compteur puisse être modifiée. Le plus simple est de l'initialiser au démarrage de l'application puis d'utiliser cet instance partout ailleurs.

Ça règle notre souci et ça semble plus performant puisqu'on s'évite un test d'existence inutile à chaque appel à la méthode `counter`.

Quelque soit le contexte dans lequel vous utilisez l'idiome `||=`, essayez d'abord de de voir s'il est possible d'initialiser la variable en amont. Vous y gagnerez un comportement plus sain.

### Pour aller plus loin

D'autres classes livrées avec Ruby permettent de gérer facilement des cas typiques d'utilisation des threads avec notamment les classes `Queue` et `SizedQueue` qui vous permettent de gérer des files de threads avec communication synchronisée. Les threads qui utiliseront la même file d'attente n'auront pas à se soucier des problèmes de synchronisation des données.

Il peut également être intéressant de jeter un œil à la classe `ConditionVariable` qui permet d'interrompre l'exécution d'un thread pour qu'il attende la disponibilité d'une autre ressource avant de continuer son traitement.

### Conclusion

Nous avons donc vu grâce à ces deux épisodes les principales fonctionnalités mises à disposition par les threads, leurs utilité ainsi que les pièges à éviter.

Les threads sont un sujet difficile à appréhender au début mais qui peut vous ouvrir de nombreuses portent vers l'optimisation de portions de code ayant pour résultat des améliorations notables des performances de votre application.


<div id="23"><h2>23- LA PROGRAMMATION SYSTEME</h2></div>

Dans le monde Unix, il n'est pas rare d'exécuter des tâches depuis le terminal, que ce soit pour lancer un ensemble de commandes ou encore faire de l'administration système. Quand ces tâches deviennent répétitives, on a tendance à les encapsuler dans un script pour les automatiser.

La plupart du temps, ces script seront des scripts shell écrit en Bash par exemple. Pourtant, quand on fait du Ruby, il peut très vite devenir intéressant de l'utiliser pour avoir accès à tout notre arsenal habituel.

### Lancer des programmes externes

Le besoin le plus courant pour l'utilisation d'un shell script est de vouloir faire le pont entre deux programmes existants.

Il y a plusieurs façons de lancer une commande externe en Ruby.

#### Équivalent de la librairie standard C

On peut tout d'abord utiliser la commande `system` qui va lancer un sous-shell et exécuter la commande :

```ruby
system("whoami")
```

La sortie de cette commande sera affichée sur la sortie standard. N'importe quelle commande, même évoluée, que vous pourriez entrer directement dans le shell peut être utilisée directement avec la méthode `system`.

On pourrait également utiliser la méthode `exec` mais elle a pour effet de remplacer le processus courant par celui nouvellement créé. Notre programme perdrait donc la main :

```ruby
exec("whoami")
```

#### Récupération de la sortie

Ces deux méthodes sont très pratiques pour une utilisation simple mais il sera fréquent de vouloir récupérer la sortie de la commande pour la stocker dans une variable qu'on va manipuler ensuite. Ruby nous propose l'opérateur backtick pour ça :

```ruby
name = `whoami`
now = `date`
```

Il existe une autre notation pour faire la même chose qui évite d'avoir à se soucier des caractère spéciaux par exemple :

```ruby
%x(uptime)
%x(ls -l).split("\n").size
```

### Manipuler les processus

Maintenant qu'on sait lancer des commandes externes et récupérer leur sortie penchons nous sur la manipulons des processus.

#### Créer des sous-processus

Depuis un programme Ruby, il est possible de lancer un autre processus dans lequel nous exécuterons du code de manière indépendante du processus principal.

C'est possible grâce à la méthode `fork` directement calquée sur la fonction Unix du même nom :

```ruby
fork do
 puts "Je suis un enfant"
end

Process.pid
```

On a donc bien deux processus différents confirmés par les PID différents.

On peut demander à notre programme principal d'attendre qu'un enfant ait fini son travail avant de reprendre la main grâce à la méthode `wait`, on peut même attendre la fin d'un processus donné grâce à la méthode `waitpid` :

```ruby
pid = fork { sleep 10; exit 1 }
Process.waitpid pid
```

Au sein d'un processus, il est possible de connaître le pid du processus parent :

```ruby
parent_pid = Process.pid

fork { p Process.ppid == parent_pid }
```

#### Tuer des processus

Maintenant que nous savons comment créer de nouveaux processus, il pourrait être intéressant de voir comment tuer des existants.

Comme pour le reste, la méthode proposée par Ruby est très similaire à la fonction unix `kill`. Cette méthode est `Process.kill` et prend deux paramètres. En premier, le signal à envoyer, le second étant le PID du processus à tuer.

On peut donc simplement faire un programme qui tue d'autres programmes sur le système en fonction de leur état, de leur consommation de ressource ou sur n'importe quelle autre base mais on peut aussi mettre en place des systèmes interne de dialogue entre processus dans notre code Ruby :

```ruby
pid = fork do
   Signal.trap("SIGTERM") { puts "Parent asked me to quit!"; exit }
   loop { } # Do something
end

Process.kill("SIGTERM", pid)
```

On peut donc depuis un processus, envoyer un signal à un autre processus pour le faire réagir en conséquence.

### Arguments et options en ligne de commande

#### OptParse

Si vous écrivez des scripts en Ruby, il y a de fortes chances que vous vouliez pouvoir passer des arguments et des options à votre script lors de son lancement.

C'est souvent le meilleur moyen de le rendre flexible. Fort heureusement, c'est facile à faire et d'ailleurs Ruby propose même des librairies pour simplifier le travail. Ma préférée étant `OptParse`, voici un exemple d'utilisation :

```bash
$ ruby options_parser.rb
$ ruby options_parser.rb -v
$ ruby options_parser.rb -d --upcase
$ ruby options_parser.rb -d --upcase file1 file2 other
$ ruby options_parser.rb -unknown
```

On peut donc très facilement et de façon élégante gérer les options passées à notre programme, récupérer les arguments, afficher une aide à l'utilisation ou encore gérer le cas des options inconnues.

#### ARGF et ARGV

Si vous le souhaitez, vous pouvez descendre à plus bas niveau grâce à deux constantes pré-remplies au moment du lancement de votre script.

Vous avez tout d'abord `ARGF` qui représente un pseudo fichier concaténant tout le contenu des différents fichiers passés en arguments au lancement du programme. On pourra donc écrire par exemple :

```ruby
puts ARGF.readline
```

qui reviendrait ni plus ni moins à cloner le fonctionnement basique de la commande unix `cat` :

```bash
ruby argf_reader.rb file1 file2
```

`ARGV` permet quant à elle de connaître la liste des arguments qui ont été passés sous la forme d'un simple tableau:

```ruby
puts "count: #{ARGV.size}"
puts "args: #{ARGV.join(", ")}"
```

```bash
$ ruby argv_reader.rb
$ ruby argv_reader.rb --help foo bar
```

### Accéder aux variables d'environnement

Pour finir, on voit assez régulièrement des scripts qui tirent parti des variables d'environnement mises à leur disposition. C'est également possible d'y avoir accès depuis Ruby :

```ruby
ENV.keys
ENV["RBENV_VERSION"]
```

Vos programmes pourraient donc récupérer de l'information extérieure de cette manière et même proposer des variables d'environnement spécifiques  qui pourraient être ajustées par l'utilisateur au moment du lancement de votre programme.

### Conclusion

Nous avons donc ici toutes les bases nécessaires pour nous lancer dans l'écriture de scripts d'administration. Ajouter à cela tout ce qu'on a pu voir précédemment avec la vidéo sur les entrées / sorties et la disponibilités de classes dédiées à la gestion de systèmes Unix. Je pense par exemple à la classe `Etc`, nous voilà prêt à automatiser nos tâches de gestion du système.


<div id="24"><h2>24- LA PROGRAMMATION RESEAU</h2></div>
Dans de nombreux projets, on souhaite pouvoir faire communiquer plusieurs programmes entre eux à travers le réseau. On peut vouloir écrire un client pour communiquer avec un service existant. On peut aussi vouloir créer un serveur qui fournira des services à des clients externes (chat, jeu, ferme de calcul, peer to peer, etc). Finalement on voudra parfois écrire le client et le serveur.

Voyons donc quelques exemples de cas concrets pour vous permettre d'appréhender ce qu'il est possible de faire.

### Écrire un serveur

Un serveur passe son temps à attendre l'arrivée d'une requête pour renvoyer une réponse. Ce qu'il fait entre deux peut être divers et varié. Ça peut être un traitement très simple ou des opérations très lourdes.

Pour ce faire le serveur pourra ne répondre qu'à une réponse à la fois ce qui est le plus simple à programmer. Il pourra aussi utiliser des threads pour être capable de répondre à plusieurs clients en simultané.

#### Cas simple

Commençons avec quelque chose de très simple, un serveur de temps dont le but sera simplement de renvoyer l'heure courante au client.

La version simple, sans thread, et qui donc ne pourra répondre qu'à un client à la fois pourrait ressembler à ça :

```ruby
require "socket"

server = TCPServer.new(4567)

loop do
  client = server.accept
  client.puts Time.now
  client.close
end
```

On voit donc qu'on charge la librairie `socket` pour pouvoir écrire facilement notre serveur. Puis on crée une instance d'un serveur TCP sur le port 4567.

On implémente finalement la logique de notre serveur qui consiste à écouter en boucle les connexions entrantes. Lorsqu'une connexion est détectée, on y envoie une chaîne qui correspond à l'heure courante sur le serveur. Pour finir, on ferme la connexion avec le client.

On peut maintenant tester notre serveur :

```bash
$ ruby time_server.rb
```

Un simple appel à telnet suffirait à effectuer le test :

```bash
$ telnet localhost 4567
```

#### Serveur multi-threads

C'est satisfaisant mais pour avoir un serveur réellement utilisable, il faudrait qu'il puisse pouvoir répondre à plusieurs requêtes en simultané. Modifions donc notre code :

```ruby
require "socket"

server = TCPServer.new(4567)

loop do
  Thread.start(server.accept) do |client|
    client.puts Time.now
    client.close
  end
end
```

On a donc simplement enrobé notre logique de réponse dans un thread ce qui suffit à ne pas bloquer la boucle principale lorsqu'on répond à un client.

Une fois encore on peut tester notre serveur avec telnet :

```bash
$ ruby threaded_time_server.rb
$ telnet localhost 4567
```

### Écrire un client

#### Un client pour notre serveur de temps

Pour le plaisir, on pourrait aussi écrire le client plutôt que de passer par telnet :

```ruby
require "socket"

HOST = ARGV[0] || "localhost"

session = TCPSocket.new(HOST, 4567)
puts session.gets
session.close
```

Une fois encore on charge la librairie `socket` pour nous faciliter la tâche.

On définie ensuite une constante qui sera remplie avec le premier argument fourni lors de l'appel de notre client ou "localhost" si aucun argument n'est passé.

On ouvre une connexion sur le serveur, puis on lui demande de nous envoyer du contenu qu'on affiche en local par la même occasion.

Finalement, on clos la connexion.

Difficile de faire plus simple !

#### Un client de nombres aléatoires

On a parfois besoin de générer des nombres aléatoires. Comme vous le savez sûrement, les librairies de génération de nombres aléatoires sont souvent pseudo-aléatoire. Dans certaines situation vous voudrez pouvoir générer des nombres réellement aléatoires et non-prédictibles. Il existe des services en ligne pour faire ça et notamment random.org qui est un service qui utilise le bruit atmosphérique pour générer des nombres aléatoires.

Créons un client qui nous permet de simuler un jet de 5 dès qui pourrait servir de base pour un jeu de hasard :

```ruby
require "net/http"
require "openssl"

uri = URI.parse("https://www.random.org/integers/?num=5&min=1&max=6&col=1&base=10&format=plain")
http = Net::HTTP.new(uri.host, uri.port)
http.use_ssl = true

resp = http.get(uri.request_uri)

puts resp.body if resp.is_a?(Net::HTTPSuccess)
```

On a donc chargé les librairies `net/http` pour ouvrir un connexion HTTP et `openssl` pour pouvoir accéder à une URL en HTTPS, ce qui est le cas du service que nous voulons utiliser.

On parse notre URL pour obtenir un objet URI plus pratique à manipuler. Dans notre URL, on voit qu'on demande 5 entiers, compris entre 1 et 6, affichés avec un résultat par ligne. Les nombres attendus devront être en base 10, rendus au format texte.

On crée ensuite un objet `Net::HTTP` auquel on passe en paramètre l'hôte et le port à contacter. On autorise ensuite l'utilisation de SSL.

On lance ensuite une requête en GET sur notre URI puis on vérifie si la réponse a été un succès. Si c'est le cas, on peut afficher nos résultats.

```bash
ruby random_numbers.rb
```

Alors biensûr, on peut faire plus simple et plus concis en Ruby grâce à la librairie `open-uri` mais ça aurait été moins drôle et instructif :

```ruby
require "open-uri"

puts open("https://www.random.org/integers/?num=5&min=1&max=6&col=1&base=10&format=plain").read
```

```bash
ruby random_numbers_2.rb
```

### Conclusion

Nous avons donc vu ici les bases des accès réseaux tout d'abord avec des sockets TCP puis ensuite un peu plus spécialisé avec `net/http`. Il y a encore beaucoup à dire sur le sujet, on aurait pu par exemple écrire un client pour un vrai serveur de temps en utilisant `net/telnet`, ou encore accéder à un serveur IMAP avec `net/imap` puis discuter avec un serveur SMTP pour envoyer des emails via `net/smtp`. On pourrait imaginer monter un pont entre un canal d'un serveur IRC et un newsgroup, les possibilités sont infinies.

Ce qu'il faudra retenir c'est que vous avez à disposition les outils bas niveau pour créer vos propres protocoles client / serveur mais que si vous souhaitez utiliser un protocole établi, alors Ruby met certainement déjà à votre disposition un lib pour vous faciliter le travail. Si ce n'est pas le cas, vous trouverez sans aucun doute un gem qui le fait.


<div id="25"><h2>25- LES TESTS AUTOMATISES, PARTIE 1</h2></div>

La mise en place de tests automatisés pour votre code peut sembler rédhibitoire si vous n'y êtes pas habitués mais s'avère vite indispensable sur des projets voués à évoluer et dépassant les quelques dizaines de ligne de code.

C'est l'assurance pour vous et les autres développeurs du projet que les modifications que vous apportez ne cassent pas le comportement d'une autre partie de l'application. Vous gagnez donc en confort et vous vous évitez des suées à chaque modification d'une portion de code que vous connaissez mal.

### Les outils à disposition

Plusieurs librairies dédiées à la mise en place de tests sont disponibles pour Ruby bien que deux options majeures sortent du lot. Si vous regardez les tests d'un projet libre écrit en Ruby, ils seront sûrement écrit à l'aide de RSpec qui a longtemps largement dominé la place grâce à ses nombreuses fonctionnalités et surtout parce qu'il a été le premier à proposer une écriture façon "spec" qui rend l'écriture et la lecture des tests plus naturelle.

Toutefois, depuis quelques temps, la librairie Minitest gagne beaucoup de terrain. Elle plaît de plus en plus aux développeurs car elle est très simple à prendre en main, utilise peu de magie pour fonctionner et reste très proche du langage Ruby de base. Pour ne rien gâcher, elle est très rapide à l'exécution et est livrée de base avec l'interpréteur Ruby !

C'est donc Minitest, dans sa version Minitest::Spec que nous allons utiliser pour profiter de l'écriture des tests à la manière "spec".

### Premiers tests

Supposons que nous avons une classe `Person` qui peut prendre en entrée un nom et un prénom et que nous voulions mettre en place une méthode d'instance qui permettra d'avoir le nom complet :

```ruby
class Person
  def initialize(first_name:, last_name:)
    @first_name, @last_name = first_name, last_name
  end

  def full_name
    [@first_name, @last_name].join(" ")
  end
end
```

On a donc le constructeur qui prend deux paramètres nommés. Ces valeurs sont stockées dans des variables d'instance pour être ré-utilisables.

On a ensuite une méthode qui permet de générer le nom complet en utilisant un tableau contenant le prénom et le nom. Ces éléments sont ensuite joins par un espace.

Pour s'assurer que notre classe fonctionne correctement, nous devons écrire les tests adéquats :

```ruby
require "minitest/autorun"

require_relative "person"

describe Person do
  it "should return person full name" do
    Person.new(first_name: "foo", last_name: "bar").full_name.must_equal "foo bar"
  end
end
```

C'est un bon début. Nous chargeons `minitest/autorun` qui permet de lancer automatiquement les tests lorsque le fichier est exécuté.

On charge ensuite le code de notre classe `Person`.

C'est maintenant le moment de passer au vif du sujet, à savoir l'écriture des tests.

La première chose remarquable est l'instruction `describe` qui permet de créer un contexte. Chaque fois qu'on souhaite grouper de manière logique un ensemble de tests, on peut utiliser un contexte. On peut d'ailleurs imbriquer les contextes.

Ici notre contexte est tout simplement la classe `Person`.

Une fois dans un contexte, on peut écrire des tests grâce au mot-clé `it` suivi d'une chaîne qui décrit ce qu'on va tester. Ici on souhaite vérifier qu'on peut obtenir le nom complet de la personne.

On va donc instancier un objet `Person` puis appeler la méthode qu'on souhaite tester, ici `full_name`. Il ne nous reste qu'à valider que la valeur retournée correspond à ce qu'on attend. C'est ce qu'on appelle une assertion.

Ici notre assertion consiste à dire que le résultat de la méthode doit être égale à la chaîne "foo bar".

Plutôt simple n'est-ce pas ?

Lançons nos tests pour voir si tout fonctionne comme attendu :

```bash
ruby person_spec.rb
```

Minitest met à notre disposition tout un tas d'assertions qui permettent de vérifier des choses diverses et variées comme l'égalité, la différente, la nullité, l'inclusion ou encore le fait qu'on objet réponde ou non à une méthode.

Toutes les assertions disponibles sont listées dans la documentation de Minitest. Il y a aussi l'aide-mémoire de [Matt Sears](http://www.mattsears.com/articles/2011/12/10/minitest-quick-reference/) qui est très bien fait.

L'idée est de tester tous les comportements de votre classe pour vous assurer que vous ne passez pas à côté de quelque chose et que vos tests garantirons le bon fonctionnement de votre classe lorsque vous la modifierez.

### TDD

L'une des grandes tendances dans le domaine du test est d'écrire les tests avant même d'écrire le code fonctionnel. Ça peut paraître étrange au premier abord mais c'est en fait un très bon moyen de bien réfléchir ses besoins et d'architecturer correctement son code.

Bien souvent quand on écrit les tests après le code fonctionnel, on a tendance à ne tester que l'implémentation présente plutôt que de tester réellement le comportement attendus pour l'ensemble des cas qu'on souhaite gérer.

On va donc procéder de cette manière pour la suite. Disons qu'à l'initialisation de notre objet, on veut pouvoir passer un deuxième prénom facultatif. Il faudrait modifier nos tests pour signifier ce besoin :

```ruby
require "minitest/autorun"

require_relative "person"

describe Person do
  describe "#full_name" do
    it "should return first name and last name when there's no middle name available" do
      Person.new(first_name: "foo", last_name: "bar").full_name.must_equal "foo bar"
    end

    it "should return first name, middle name and last name when all available" do
      Person.new(first_name: "foo", last_name: "bar", middle_name: "baz").full_name.must_equal "foo baz bar"
    end
  end
end
```

On a ajouter un contexte `full_name` pour regrouper les tests relatifs à cette méthode.

Le premier test est le même qu'avant, nous avons simplement changé son nom pour être plus explicite sur ce qui est testé.

Nous avons finalement ajouté un test pour vérifier que si le second prénom est disponible, il sera utilisé dans la chaîne générée.

L'idée est donc de lancer notre test pour voir s'il passe ou non. Il ne doit logiquement pas passer puisque nous n'avons jamais prévu ce cas.

```bash
ruby person_spec.rb
```

On a bien une erreur qui nous explique que le paramètre `middle_name` est inconnu de la méthode `initialize`. Ajoutons le :

```ruby
def initialize(first_name:, last_name:, middle_name:)
  @first_name, @last_name, @middle_name = first_name, last_name, middle_name
end
```

puis relançons nos tests:

```bash
ruby person_spec.rb
```

Nous avons maintenant deux erreurs… L'une d'entre elle nous dit qu'on a essayé d'initialiser l'objet sans passer de `middle_name`. Corrigeons déjà ça puisque effectivement ce paramètre est facultatif:

```ruby
def initialize(first_name:, last_name:, middle_name: nil)
  @first_name, @last_name, @middle_name = first_name, last_name, middle_name
end
```

Si on relance nos tests:

```bash
ruby person_spec.rb
```

On voit qu'il ne nous reste qu'une erreur qui nous dit que la chaîne obtenue ne correspond pas à la chaîne attendu. C'est donc à nous de jouer et de modifier notre code pour qu'il réponde au besoin :

```ruby
def full_name
  [@first_name, @middle_name, @last_name].compact.join(" ")
end
```

Lançons à nouveau nos tests :

```bash
ruby person_spec.rb
```

Et tous nos tests passent ! Voilà un exemple parfait de développement basé sur les tests plus connus sous le nom de "TDD".

### Conclusion

Cette introduction rapide vous permettra de commencer à mettre en place des tests pour garantir le bon fonctionnement de votre code et éviter l'introduction de régression. Elle vous montre également comment mettre un pied à l'étrier pour utiliser le TDD qui est une pratique qui devient indispensable lorsqu'on la maîtrise.

Dans le prochain épisode nous verrons comment éviter la redondance à travers les différents tests mais aussi comment maîtriser le contexte d'exécution des tests pour pouvoir tester des cas complexes dépendant d'éléments extérieur à priori non maîtrisables.


<div id="26"><h2>26- LES TESTS AUTOMATISES, PARTIE 2</h2></div>
Maintenant que nous avons vu les bases de la mise en place de tests à l'aide de Minitest::Spec, nous allons aller un peu plus loin et découvrir les outils que Minitest met à notre disposition pour éviter la redondance et gérer des cas complexes dans lequels le contexte doit être maitrisé pour pouvoir écrire des tests robustes.

### Callbacks et accesseurs paresseux

#### before / after

Vous aurez souvent besoin, pour plusieurs tests d'un même contexte, d'initialiser pour chaque test un objet ou un environnement identique.

Plutôt que refaire cette initialisation dans chaque test ou d'écrire une méthode privée que vous appellerez manuellement dans chaque test, Minitest met à votre disposition des callbacks qui sont `before` et `after` et qui seront respectivement appelés avant et après chaque test du contexte.

```ruby
require "minitest/spec"
require "minitest/autorun"

require_relative "person"

describe Person do
  before do
    puts "Avant le test"
  end

  after do
    puts "Après le test"
  end

  it "should do something" do
    puts "dans le test"
  end

  it "should do something else" do
    puts "dans l'autre test"
  end
end
```

On voit donc que les blocs `before` et `after` sont bien exécutés avant **et** après **chaque** test.

C'est donc l'endroit parfait pour initialiser des données qui seront utilisés dans chaque test ou nettoyer une base de données après chaque test.

```ruby
require "minitest/spec"
require "minitest/autorun"

require_relative "person"

describe Person do
  describe "#full_name" do
    before do
      @person = Person.new(first_name: "Nico", last_name: "C.")
    end

    after do
      puts "Cleaning DB"
    end

    it "should include first name" do
      @person.full_name.must_include("Nico")
    end

    it "should include last name" do
      @person.full_name.must_include("C.")
    end
  end
end
```

Ces tests sont bizarrement constitués je vous l'accorde mais permettent de bien mettre en évidence l'utilisation de `before` et `after`.

On a donc profité du bloc `before` pour initialiser une instance de la classe `Person` qu'on stocke dans une variable d'instance. On va donc pouvoir ré-utiliser cette variable à travers tous nos tests du contexte. On s'épargne donc l'initialisation dans chaque test.

Dans notre exemple, le bloc `after` fait prétendument un nettoyage de la base de donnée après chaque test.

#### Lazy accessors

Un autre besoin encore plus courant est de mutualiser le contenu d'une variable entre plusieurs tests d'un même contexte. C'est ce que nous avons fait avant avec le `before` mais en pratique on le réservera plutôt à de la configuration d'environnement.

Bien souvent, on utilisera les accesseurs paresseux pour gérer les variables à partager entre plusieurs tests. Ces accesseurs paresseux sont déclarée à l'aide de `let` qui attend un bloc de code qui ne sera exécuté que lors du premier appel dans un test. Le bloc n'est donc pas exécuté s'il la variable n'est pas utilisée. De plus ce bloc ne sera exécuté qu'une fois par test. C'est donc la méthode la plus efficace et performante pour gérer des variables partagées.

On pourrait donc remplacer notre code de test précédent par :

```ruby
require "minitest/spec"
require "minitest/autorun"

require_relative "person"

describe Person do
  describe "#full_name" do

    after do
      puts "Cleaning DB"
    end

    let(:person) { Person.new(first_name: "Nico", last_name: "C.") }

    it "should include first name" do
      person.full_name.must_include("Nico")
    end

    it "should include last name" do
      person.full_name.must_include("C.")
    end
  end
end
```

On a donc supprimé le bloc `before` pour le remplacer par un appel à `let` qui définie un accesseur paresseux qui sera générée à son premier appel. Ce n'est pas une variable mais plutôt une méthode qui nous retourne le résultat d'un bloc au premier appel puis sa version cachée ensuite.

Dans nos tests, on appelle donc l'accesseur `person`  plutôt que la variable d'instance `@person`.

### Stubs

Lorsqu'on teste, on a aussi régulièrement besoin de pouvoir forcer certains objets à répondre de manière attendu. C'est particulièrement vrai quand l'une de vos méthodes manipule des heures et dates ou des données aléatoires.

Dans ce cas il est particulièrement utile de pouvoir demander à une méthode de toujours répondre de la même manière lorsqu'on l'appel à un certain endroit ou avec certains paramètres.

Disons que notre classe `Person` peut retourner l'âge de la personne en secondes, on serait tenté d'écrire le test comme suit:

```ruby
describe "#age_in_seconds" do
  it "should return person age in second from now" do
    thirty_years_ago = 30 * 365 * 24 * 60 * 60
    borned_at = Time.now - thirty_years_ago

    p = Person.new(first_name: "foo", last_name: "bar", birthday: borned_at)
    p.age_in_seconds.must_equal Time.now - borned_at
  end
end
```

On crée une date qui correspond à un age de 30 ans, puis on utilise cette date pour définir l'âge de notre personne.

On appelle ensuite la méthode `age_in_seconds` et on la compare à l'heure courante moins 30 ans.

On ajoute ensuite la méthode à notre classe ainsi que l'attribut `@birthday`:

```ruby
def age_in_seconds
  Time.now - @birthday
end
```

Si on lance notre test on a une erreur. Le souci ici est qu'on va avoir un décalage de quelques millisecondes entre la création de la date anniversaire et le retour de notre méthode, il s'est passé quelques millisecondes dans le programmes.

Le plus simple est donc de faire en sorte que la méthode `Time.now` réponde avec une valeur fixe qui nous permet de tester dans des conditions connues :

```ruby
current_time = Time.now

Time.stub :now, current_time do
  # …
end
```

On a donc stubber la méthode `now` de la classe `Time` pour que la valeur retournée soit toujours `current_time`. Tous les appels à `Time.now` dans le bloc retourneront donc la valeur de `current_time` y compris celui fait par notre méthode `age_in_seconds`.

Il ne faut évidemment pas en abuser et ne l'utiliser que dans le cas où contrôler la valeur de retour d'une méthode est une nécessité.

#### MiniTest::Mock

Le dernière fonctionnalité de MiniTest que je souhaite vous présenter est MiniTest::Mock dont le but est de créer un objet factice qui sera capable de recevoir des appels de méthode et de retourner des valeurs. Il permettra également de vérifier que les méthodes attendues ont bien été appelées pendant notre test. On pourra même vérifier qu'elles ont été appelées avec les bons arguments.

C'est particulièrement utile lorsque vous souhaitez simuler les appels à un service externe que vous ne maîtrisez pas.

De manière générale, c'est une bonne pratique de "mocker" tous les appels à des services externes. Ça permet de lancer les tests sans avoir de connexion réseau ou même encore si le service externe ne répond pas. Ça permettra d'ailleurs de tester le cas où le service est indisponible. Dans tous les cas, vos tests seront plus rapides.

On pourra donc simuler des appels à un serveur IMAP, à une base de données, une API, etc.

Créons donc une classe dédiée à l'envoie de message sur des plate-formes variées, Twitter par exemple.

Nous pourrions mettre en place une classe qui utilisera une interface commune pour envoyer les messages, il suffira donc de passer à l'initialisation de notre objet un autre objet qui implémente l'interface en question.

Ici les objets passés devront au moins répondre à la méthode `post` pour pouvoir être utilisés. Le reste de leur interface et le fonctionnement interne nous est égale :

```ruby
class SocialMedia
  def initialize(media)
    @media = media
  end

  def post(message)
    @media.post("#{message} from SocialMedia class")
  end
end
```

On a donc une classe `SocialMedia` qui lors de son instanciation attend un paramètre qui est en fait le client pour l'API visée. Cette instance du clent sera donc capable de s'identifier, poster un message, etc.

Notre classe déclare ensuite une méthode `post` dont le but est d'utiliser le client fourni et d'appeler sa méthode `post` avec un message retravaillé.

L'implémentation est fantaisiste, personne n'aurait d'intérêt à utiliser ça mais l'idée est là. On isole les responsabilités pour avoir une architecture propre.

On écrit maintenant les tests pour notre classe :

```ruby
require 'minitest/autorun'

require_relative 'social_media'

describe SocialMedia do
  before do
    @twitter  = MiniTest::Mock.new
  end

  let(:social_media) { SocialMedia.new(@twitter) }
  let(:content) { "I'm social!"}

  it "should append a watermark from the class" do
    @twitter.expect :post, true, ["#{content} from SocialMedia class"]
    social_media.post(content)

    assert @twitter.verify # verifies tweet and hashtag was passed to `@twitter.update`
  end
end
```

Dans le bloc `before` nous avons créé un mock de l'objet servant à communiquer avec l'API de tweeter puisque dans nos test nous ne souhaitons pas réellement contacter l'API de twitter mais simplement simuler son comportement.

Nous déclarons ensuite deux accesseurs paresseux, l'un instanciant notre classe avec en paramètre le mock de l'API Twitter puis un autre qui contient simplement le contenu à envoyer sur le réseau social.

Ensuite on déclare notre test qui va s'assurer que notre classe ajoute bien une chaîne l'identifiant à la fin du message original.

On fait savoir à notre mock qu'il doit normalement être appelé via sa méthode `post` avec en paramètre la chaîne "#{content} from SocialMedia class" et que dans ce cas il retournera true.

On appelle ensuite la méthode de notre classe qui est censée déclencher l'appel à la méthode `post` de l'API en lui passant le contenu d'origine.

Finalement, on s'assure avec `assert` que notre mock a bien été appelé comme prévu.

Si le test passe, on a donc l'assurance que les objets utilisés en interne dans notre méthode on bien été appelés avec les paramètres attendus. Dans notre cas, ça revient à confirmer que notre classe appelle bien la méthode `post` de l'objet API fourni et lui passe en argument la chaîne modifiée.

### Conclusion

Vous connaissez maintenant toutes les bases vous permettant d'écrire des tests automatisés. Vous verrez que très rapidement l'écriture de tests deviendra naturelle et que vous ferez de plus en plus de TDD sans vous en rendre compte.

Les tests sont sans aucun doute possible l'un de vos meilleurs alliés pour écrire un code de qualité et que vous pourrez faire évoluer sur le long terme sans vous tirer les cheveux.


<div id="27"><h2>27- UTILISER LE DEBUGGER</h2></div>

Quelque soit l'attention que vous portez à l'architecture et
l'écriture de votre code, vous finirez un jour par être confronté à un
bug. Parfois les bugs sont très simples à trouver et vous n'aurez
besoin d'aucun outil pour le repérer et le corriger. Le reste du
temps, il vous faudra comprendre ce qui se passe, analyser ce que vous
avez en entrée et pourquoi ce que vous avez en sortie n'est pas
conforme à ce qui est attendu.

Vous devrez alors suivre l'exécution du code, passer de méthodes en
méthodes pour analyser ce qu'il se passe. Beaucoup de développeurs se
cantonnent à l'utilisation de messages de débogage pour vérifier les
valeurs des éléments clés à différents endroits. Il ne sera donc pas
rare de voir un développeur mettre des `puts` dans son code ou de
façon un peu plus élégante en utilisant un logger avec quelque chose
comme `logger.debug`.

Quand on sait dans quelle méthode se trouve le problème et que cette
méthode ne fait pas des dizaines de lignes, ce qui ne devrait
d'ailleurs jamais être le cas, ces méthodes d'analyse peuvent
suffir. Pour les cas plus complexes, il existe un outil bien plus
adapté qu'on retrouve dans tous les langages, le debbuger.

En Ruby plusieurs outils sont disponibles pour faire du
debbugage. Bien évidemment, Ruby propose de base un outil qui permet
de poser un point d'arrêt dans le code et de lancer la console
interactive pour analyser l'état courant puis continuer à avancer dans
le code. Bien que tout à fait honorable, il existe des alternatives à
cet outil qui permettent d'accéder à plus de flexibilité.

Aujourd'hui on a principalement `pry` et `byebug`. Nous allons
utiliser ce dernier dans cette vidéo mais gardez à l'esprit que
quelque soit l'outil utilisé, ils partagent tous les mêmes
fonctionnalités de base.

### Installation de byebug

`byebug` n'est pas livré de base avec Ruby, il faut donc
l'installer. On va utiliser la commande `gem` :

```shell
$ gem install byebug
```

### Placer un point d'arrêt

Pour l'utiliser, il nous suffit maintenant de charger `byebug` dans
notre code et d'appeler la méthode `byebug` à l'endroit où l'on
souhaite que l'exécution s'arrête.

Voici un exemple de script que j'ai préparé pour démontrer
l'utilisation :

```ruby
require 'byebug'

class Computer
  def initialize(a, b)
    @a = a
    @b = b
  end

  def sum_and_double
    sum = sum(@a, @b)
    double(sum)
  end

  private

  def sum(a, b)
    a + b
  end

  def double(a)
    a * a
  end
end

computer = Computer.new(2, 3)
res = computer.sum_and_double

puts res
```

On a écrit une classe qui prend deux paramètres. Son but est de
faire la somme des deux paramètres puis de doubler ce résultat et le
retourner.

Évidemment l'exemple est extrêmement simple, difficile de faire une
erreur, on peut même se demander pourquoi faire une classe. C'est
uniquement pour vous montrer l'utilisation du debugger dans un
contexte très simple à comprendre.

Comme vous pouvez le voir, j'ai le constructeur qui stocke nos valeurs
initiales. J'ai ensuite une méthode principale qui permet de faire le
traitement attendu.

Cette méthode principale délégue les deux parties du traitement
(l'addition et la multiplication) à des méthodes privées. Avec cette
structuration découpée, on se retrouve avec une architecture assez
proche d'un cas réel.

Comme vous l'aurez remarqué, ce code comporte un bug grossier. La
multiplication ne double pas la valeur mais retourne son carré. Faites
comme si vous ne l'aviez pas vu et que ce bug est très difficile à
détecter.

Si on lance notre programme, on a bien un résultat erroné :

```shell
$ ruby buggy.rb
```

Ajoutons donc un point d'arrêt pour suivre le déroulé et comprendre ce
qu'il se passe.

Et relançons notre script.

### Naviguer dans les sources

On se retrouve dans une console interactive qui nous présente
l'instruction sur laquelle on s'est arrêté. Juste après notre
instruction `byebug`, donc juste avant la première instruction de la
méthode `sum_and_double`.

Comme c'est notre première session `byebug`, on peut commencer par
afficher la liste des commandes avec la commande `help` puis l'aide
d'une commande donnée, ici la commande next.

Une commande intéressante est la commande `list` qui comme son aide
l'indique (taper help list) permet de lister les lignes de code autour
d'une ligne donnée. Par défaut la ligne courante. Essayons:

```ruby
list 3-5
```

On a donc les lignes 3 à 5 de notre fichier courant, on peut également
afficher le contexte autour de la ligne en cours d'exécution :

```ruby
list=
```

On peut évidemment lister les lignes qui précédent :

```ruby
list-
```

### Analyser l'état courant

Passons maintenant à l'analyse des variables de notre script. On peut
simplement appeler une variable par son nom, si elle existe dans le
contexte, son contenu sera affiché :

```ruby
@a
```

mais on peut aussi afficher toutes les variables d'un type donné pour
le contexte courant:

```ruby
var
var instance
```

Nos variables d'instance sont donc bien conformes à ce qu'on
attendait. On va donc demander l'exécution de l'instruction suivante
et voir où ça nous mène. Les debuggers nous offrent deux possibilités
pour avancer dans le code, on peut soit exécuter l'instruction et
s'arrêter à la suivante ou alors exécuter en entrant dedans pour
exécuter son code ligne par ligne. C'est ce que nous allons faire ici :

```ruby
step
```

On se retrouve donc dans la définition de la méthode `sum`. C'est
l'occasion de découvrir une autre fonctionnalité intéressante qui
permet de savoir comment on est arrivé là où on se trouve :

```ruby
backtrace
```

On sait donc qu'on se trouve dans la méthode `Computer.sum` qui a été
appelée par `Computer.sum_and_double` elle-même appelée par le
programme principal. C'est particulièrement pratique dans de grosses
applications où les points d'entrée sont nombreux comme une
application Rails par exemple.

On pourrait se déplacer dans l'un des appels parents et obtenir le
contexte de cet appel parent :

```ruby
frame 1
```

On peut donc voir l'état des variables et autres éléments comme si
nous venions juste de passer dans le parent. C'est l'une des grandes
force des debuggers. Vous avez une machine à voyager dans le temps qui
vous permet d'analyser le comportement qu'a eu votre programme tout au
long de son exécution.

Continuons notre inspection à la recherche de notre bug:

```ruby
next
```

On est sortie de notre méthode `sum`, on peut vérifier le contenu de
notre variable avant de continuer :

```ruby
sum
```

Notre variable contient la valeur attendue, notre bug est donc plus
loin, continuons :

```ruby
next
res
```

La valeur obtenue en sortie de la méthode `double` est erronée, on
peut donc supposer que l'erreur se trouve dans cette méthode. En y
regardant, on comprendra que la multiplication devrait en fait être
une addition.

Voici à quoi peut ressembler une chasse au bug avec un debugger. Son
utilisation prend tout son sens avec des programmes plus complexes.

### Encore plus

`byebug` a encore plus à offrir, je vous invite à décortiquer son
aide, vous pouvez par exemple :

- ajouter des points d'arrêt à la volée
- lister l'ensemble des points d'arrêt
- lister les threads et passer de l'un à l'autre
- attraper les exceptions
- lancer l'édition d'un fichier à un endroit précis
- relancer le programme
- tracer des variables globales
- sauver une session de débogage et la restaurer plus tard
- créer des points d'arrêt conditionnels
- etc

### Conclusion

Le debugger, quelque soit le langage utilisé, est l'arme par
excellence pour résoudre des cas complexes. Par expérience je sais
que cet outil est trop sous-estimé, particulièrement par les
développeurs qui n'ont jamais utilisé des langages compilés ou qui
n'ont jamais dû gérer eux-mêmes l'utilisation de la mémoire dans leurs
programmes.

Le prochaine fois que vous rencontrez un bug, plutôt que de mettre des
`puts` un peu partout, essayer de placer un ou plusieurs points
d'arrêts aux endroits stratégiques et lancer votre debugger. Même si
ce n'est pas naturel au début, vous deviendrez vite accro à cet outil
indispensable.


