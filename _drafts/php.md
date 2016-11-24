---
published: false
---
du ternaire
value="<?php echo $nom == 'val-par-def' ? '' : $nom; ?>" dans les formulaire pour garder la chaine précedement tapé malgrés le refrech

$_REQUEST['nom'] deconseillé d'utilisé (prends post get cookie)


Pour garder les infos dans le formulaire, il faut utiliser les cookies:
//creation du cookie
	setcookie('nom_du_cookie',$la_valeur, time() + 3600, '/', 'blog.monsite.com', false, true );

- ici timestamp, time() c'est le temps écoulé de 1970 à now + 1h donc le cookie expire dans 1h (si c'est 0 alors le cookie est supprimé quand on quitte le site)
- '/' c'est le path, a partir de quel arbo ce cookie est dispo, ici la racine du site donc tt le site
- 'blog.monsite.com' permet de rendre dispo le cookie que dans ce nom de domaine la, la chaine vide '' est utile pour rendre accessible à tout les sous domaine
- le parametre suivant permet de déterminer si le cookie est sécurisé ou non, si c'est le cas (true) il faut créer le cookie depuis une page HTTPS
- permet de déterminer si le cookie est dispo uniquement par php ou si il est dispo aussi par les langages client comme javascript donc  true empeche JS d'acceder aux cookie car il est dispo juste pour php

ex:
if(isset($_GET['langue'])){
	$langue_affichee=$_GET['langue'];
	setcookie('langue', $langue_affichee, 0, '/', '', false, true);
}
elseif(isset($_COOKIE['langue'])){
	$langue_affichee=$_COOKIE['langue'];
}
PUIS SUPPRIMER LES COOKIES APRES LA DECONNECTION en supprimant la variable puis en supprimant le cookie:
unset($_COOKIE['langue']);
setcookie('langue', $langue_affichee, time() - 60 , '/', '', false, true); //ici on met un timestamp moins 60 secondes pour que le navigateur puisse supprimer le cookie.



syntaxe pratique pour afficher des portions html dans du php
<?php if(---): ?>

<?php else: ?>

<?php endif ?>


on peut verifier la valeur d'un get si elle fait partie d'un tableau:
if(isset($_GET['langue']) && in_array($_GET['langue'],array('uk','fr','it','es')))
Donc il faut voir si la variable existe, effacer les espaces en début et fin de ligne, filtrer et enfin tester si c'est la valeur fait partie des resultats voulu



Pour verifier un string il utiliser les fonctions:
- strip_tags($var)  //supprime les balises html et php d'une chaine
- htmlspecialchars($var) //convertit les caracteres speciaux en entites html
- addslashes // ajout des antislashs dans une chaine
- htmlentities //convertit tous les caracteres éligible en entités html



on peut utiliser les variables de sessions a la place de cookie car c'est plus sécurisé




renvoyer un fichier ddl dans le bon repertoire apres ddl depuis un form:
<form action="" method="POST" enctype="multipart/form-data">
	<input type="file" name="avatar" />

if(isset($_FILES['avatar']) && $_FILES['avatar']['error']==0){
	//var_dump($_FILES['avatar']);  //-> permet de voir en detail les infos sur le fichier
	move_uploaded_file($_FILES['avatar']['tmp_name'], $_SERVER['DOCUMENT_ROOT'].'/test/img/'.basename($_FILES['avatar']['name'])); //deplacer le fichier de son emplacement temporaire vers sa destination definitif
	$_SESSION['image']=basename($_FILES['avatar']['name']) // on affiche l'image dans une balise img...

	pour supprimer un fichier dans l'arbo du serveur:
	utiliser unlink($_SERVER['DOCUMENT_ROOT'].'/test/img/'.$_SESSION['image']);

	fonction pour verifier si ce qui a etait uploadé est vraiment une image, eller renvoie un bool:
	var_dump(getimagesize($_FILES['avatar']['tmp_name']));
	donc on fait:
	$verif_img=getimagesize($_FILES['avatar']['tmp_name']);
	if($verif_img && $verif_img[2]<4)  on test si ca revoie true et que l'img est soit un gif,jpeg ou png (1=gif 2=jpeg 3=png donc Inferieur a 4 permet de tester ça)
}

la variable $_SERVER permet d'avoir des infos sur le serveur, on peut voir le path du site, l'ip, plein d'info...





Pour resoudre le probleme des boutons navbar effet appuyé avec id='active'
il suffit de creer des constantes PHP en début de chaques pages puis quand on include le header
on fait un if le btn equivaut a la page alors echo id='active'

ex:
define('PAGE','index'); // PAGE prend pour valeur index

dans la navbar inclure une balise php <?php if (PAGE == 'index'){echo ' "id=active"';}?>  //ne pas mettre $ devant page


header('Location: v2b.php'); permet de rediriger vers une autre page



ENVOYER UN MAIL VIA PHP:
pour un formulaire contenant les champs (nom, prenom, mail, objet, message)

$destinataire = 'admin@admin.com'
$expediteur = 'client@client.com'  //ici mettre la varialbe mail filtré au préalable...
$enteteMsg = $nom.' '.$prenom.' <'.$exp.'> à ecrit :'."\r\n\r\n";
$message = nl2br($enteteMsg.$message);
$headers = 'MIME-Version: 1.0'."\r\n";
$headers .= 'Content-type: text/html; charset=utf-8'."\r\n";
$headers .= 'Reply-to: '.$exp."\n";
$headers .= 'From: '.$nom.' '.$prenom.'<'.$expediteur.'>'."\n";
if(mail($destinatiare,$objet,$message,$headers)){
	echo "<h3>Votre message a bien été envoyé aux admins</h3>";
	echo "<h3>Nous vous répondrons au plus vite.</h3>";
}else{
	echo "erreur";
}
