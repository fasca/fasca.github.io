---
layout: post
title: Ruby
date: 2017-07-15
tags:
  - backend
  - developpement
description: cours rapide sur Ruby
categories: developpement backend
serie: programmation
published: true
---

## **SOMMAIRE**

* **Les types primitifs String et Numeric**
* **Les types primitifs Array et Hash**
* **Les structures de controle**
* **Variables et identifieurs**
* **Créer une classe**
* **Les accesseurs**
* **La visibilité des méthodes**
* **Les bases de la réflexion**
* **Les symboles**
* **La classe Time**
* **Les classes Date et Datetime**
* **La classe Array**
* **Manipuler des chaînes de caractères**
* **Les expressions rationnelles, partie 1**
* **Les expressions rationnelles, partie 2**
* **Les entrées sorties**
* **Les attributs de fichier**
* **Fichiers temporaires et répertoires**
* **Sérialisation et persistance**
* **Les threads en ruby**
* **Synchroniser les threads**
* **La programmation système**
* **La programmation réseau**
* **Les tests automatisés, partie 1**
* **Les tests automatisés, partie 2**
* **Utiliser le debugger**


## LES TYPES PRIMITIFS STRING ET NUMERIC

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

## LES TYPES PRIMITIFS ARRAY ET HASH

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

## LES STRUCTURES DE CONTROLE

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

## VARIABLES ET IDENTIFIEURS

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

## CREER UNE CLASSE

## LES ACCESSEURS

## LA VISIBILITE DES METHODES

## LES BASES DE LA REFLEXION

## LES SYMBOLES

## LA CLASSE TIME

## LES CLASSES DATE ET DATETIME

## LA CLASSE ARRAY

## MANIPULER DES CHAINES DE CARACTERES

## LES EXPRESSIONS RATIONNELLES, PARTIE 1

## LES EXPRESSIONS RATIONNELLES, PARTIE 2

## LES ENTREES SORTIES

## LES ATTRIBUTS DE FICHIER

## FICHIERS TEMPORAIRES ET REPERTOIRES

## SERIALISATION ET PERSISTANCE

## LES THREADS EN RUBY

## SYCHRONISER LES THREADS

## LA PROGRAMMATION SYSTEME

## LA PROGRAMMATION RESEAU

## LES TESTS AUTOMATISES, PARTIE 1

## LES TESTS AUTOMATISES, PARTIE 2

## UTILISER LE DEBUGGER
