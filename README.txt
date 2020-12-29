DM POO API et outillages de DEVAUX Camille

lien du projet sur GitHub : https://github.com/Cam-Dvx/DM-POO-API-Outillages-DEVAUX

TP DM noté 1/2 : Réalisation d'une application web avec Springboot

Etape 5 : cherchez une description succinte de chaque dépendance ajoutée

	. Web : créer des applications web MVC
	. JPA : requêtes SQL pour les bases de données 
	. Hibernate : gère les données sur la bdd, mappe des classes java et des tables de données
	. H2 : création de base de données, système de gestion et interface web pour y avoir accès 
	. DevTools : outils de développement 
	. Thymeleaf : pour faciliter le code HTML  

Etape 13 : 

	1 ) Avec quelle partie du code avons-nous paramétré l'url d'appel /greeting?
		L'appel de l'URL /greeting est réalisé grâce au @GetMapping("/greeting") dans le controller 
		
	2 ) Avec quelle partie du code avons-nous choisi le fichier html à afficher? 
		Le fichier HTML est choisi à travers le return "greeting"
	
	3 ) Comment envoyons-nous le nom à qui nous disons bonjour avec le second lien? 
		Le nom est envoyé par le lien grâce au ?nameGET. Pour le récupérer dans le code on utilise @RequestParam (required=false siginifie que le champs n'est pas forcément spécifié, auquel cas on applique une valeurs par défault "World"). Ensuite on envoie cette donnée au modèle via model.addAttribute("nom", nameGET). Thymeleaf se charge de l'interprétation et l'envoie à la page html où on peut afficher la donnée en l'appelant ${nom}.

Etape 17 : Retournez sur la console et remarquez la différence
	
	Oui il y a une différence, il y a une table address qui est apparue et qui contiet pour colonnes les attributs de notre classe java (id, creation et content). Il y aussi une partie "sequence" qui est apparue. 

Etape 18 : Expliquez l'apparition de la nouvelle table 

	C'est hibernate qui a permis de créer la base de données car notre classe dispose de l'annotation @Entity, de ce fait Hibernate a lu la classe et l'a transformée en table de donnée. 

Etape 20 : Voyez vous le contenu de data.sql après une requête de type select sur la table address?

	Oui, quand on fait la requête "Select * FROM Address" le contenu de notre fichier data.sql s'affiche. 

Etape 23 : A quoi sert l'annotation @autowired? 

	@Autowired permet de faire de l'injection de dépendance, c'est à dire que cette annotation permet de lier automatiquement des éléments de l'application. Spring va se charger de chercher les liaisons et faire les injonctions. Ici, la classe AddressController va être instanciée et injectée dans dans l'interface AddressRepository. 

Etape 30 : Expliquez comment vous avez ajouté Bootstrap à votre projet 

	Pour inclure Bootstrap il suffit de mettre "meta name = viewport" en tête de fichier et d'ajouter ces deux lignes de code dans toutes nos pages HTML : 
	<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.0/jquery.min.js"></script>  
	<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/js/bootstrap.min.js"></script>
	
TP DM noté 2/2 : Utilisation d'API web avec Spring Boot

Etape 6 : 

	- Faut-il une clef d'API pour appeler OpenWeatherMap?
	Oui, pour utiliser openWeatherMap une clef d'API est nécessaire, il faut donc se créer un compte pour l'obtenir (ou demander à quelqu'un de prêter la sienne).
	
	- Quelle URL appeler? 
	Il y a plusieurs URL selon les données qu'on souhaite récupérer, on peut aussi choisir un certain nombre de paramètres. Personnellement j'ai utilisé l'url qui suit pour récupérer la météo actuelle selon les coordonées géographiques : 
	http://api.openweathermap.org/data/2.5/weather?lat=lat&lon=lon&units=metric&appid=ed87f66bec8d0f3351aec86a5d3035b9&lang=fr
	On indique la latitude et la longituge grâce à "?lat=lat&lon=lon".
	"unit=metric" permet de choisir les unités des données qu'on récupère (ici on récupèrera des °C, système de mesure français)
	"lang=fr" permet de récupérer les résultats en français (en partie, notamment pour la description de la météo)
	"appid=" permet de renseigner la clef d'API qui est nécessaire pour effectuer la requête. 
	
	- Quelle méthode HTTP utiliser?
	On utilise la méthode GET afin d'utiliser l'API et de récupérer des informations. 
	
	- Comment passer les paramètres d'appel?
	Pour passer les paramètres d'appel il faut "composer" l'URL avec nos données, en les insérant à la place de lat et lon comme je l'ai expliqué dans l'url que j'ai choisi. 
	
	- Où est l'information dont j'ai besoin dans la réponse : 
	Pour avoir la réponse à ses questions, il faut analyser la structure du fichier JSON de réponse à la requête. 
		. pour afficher la température du lieu visé par les coordonnées GPS? 
		On trouve la température dans l'objet Main de la réponse. Cet objet contient plusieurs attributs dont un intitulé "temp" qui contient la donnée qu'on souhaite. 
		. pour afficher la prévision météo du lieu visé par les coordonnées GPS? 
		Pour afficher la prévision météo dans le sens "le temps qu'il fera les prochains jours" il faut utiliser une autre URL pour avoir les bonnes informations. Sinon si c'est juste pour savoir la météo qu'il fait, il faut récupérer l'objet weather de la réponse et récupérer son attribut description.
		