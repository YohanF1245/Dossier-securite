# Security strategy
- [1 - Introduction](#1---introduction)
- [2 - Règles générales](#2---regles-generales)
    - [Défense en profondeur](#défense-en-profondeur)
    - [Réduction de la surface d'attaque](#réduction-de-la-surface-dattaque)
    - [Conformité RGPD](#conformité-rgpd)
- [3 - Backend](#--backend)
    - [Moindre privilège](#moindre-privilège)
    - [RBAC](#rbac)
- [ - API](#--api)
## 1 - INTRODUCTION

In today’s increasingly interconnected world, securing information systems and data is a critical priority for all organizations. In this regard, it’s crucial to determine the targets, assess the level of protection they require and understand the repercussions in case of a security breach.<br>
The repercussions of security flaws can be particularly frustrating for those involved including:
- The user: Potential target of identity or information theft which can result in a significant loss of trust in the application.
- The application owner: A security breach could cause service interruption and compliance violation leading to legal penalties and financial loss.
- The application developer: Should there be flaws in security, it could impact the organization’s reputation, result in potential lawsuits, and lead to financial losses associated with remediation effort.<br>

This security strategy seeks to establish a comprehensive framework outlining the necessary steps to implement robust protections against the risks we encounter. In this document, we will address each layer involved, identify potential risks, and outline appropriate countermeasures.<br>
The security strategy encompasses several critical layers, such as:
Transversal security rules and good practices
- Frontend vulnerabilities
- Api vulnerabilities
- Database injections and malware threats

This strategy was designed with a keen focus on optimizing the balance between ergonomics and safety


![image](/src/img/barre-intro.png)


The rigorous implementation of this strategy will not only strengthen the trust of our stakeholders but also protect all our business processes from potential compromise.

## 2 - REGLES GENERALES

### Défense en profondeur

Pour garantir une efficacité maximale de la stratégie de sécurité, nous appliquerons le principe de défense en profondeur. En superposant les règles de sécurités à des , nous nous couvrons en cas de vulnérabilité de l'une d'entre elle.
```
Exemple:
Une machine infectée pourrait profiter d'une faille pour tenter une attaque de type cross-site scripting pour injecter du code javascript via un formulaire de commentaire.
Cette attaque va être contrée par la sanitization mise en place qui va rendre inoffensive les balises de type <script>
```

### Réduction de la surface d'attaque

L'une des erreurs dans le développement d'application web est la multiplication des points d'entrées de l'application (OS du serveur, librairies, addresses IP). Nous appliquerons le principe de réduction de la surface d'attaque pour limiter les points de vulnérabilité de l'application.

### Conformité RGPD

Le traitement de données est hautement encadré. Nous nous conformerons à la réglementation en vigueur via plusieurs règles détaillées plus tard dans les présentations en détail des différentes couches. [Voir la section concernée](#rgpd)

## 3 - BACKEND

### Moindre privilège

Nous appliquerons le principe du moindre privilège afin de réduire la virulence de potentielles attaques venant de comptes utilisateurs compromis. Moins un utilisateur a de droits, moins sa puissance de frappe est grande.

### RBAC

Nous mettrons en place un RBAC pour gérer les permissions des utilisateurs groupe par groupe. Cela va de paire avec le principe du moindre privilège car il nous offrera un moyen simple d'octroyer les autorisations aux utilisateurs (authentifiés ou non).
- Visiteur (non authentifié): consulter des cours (ou un apercu)
- Apprenant : consulter et s'inscrire a des cours
- Coach : rédiger des cours
- Admin : tout les droits de création, suppression, édition ou consultation&

## 3.1 - API

### ORM

Nous avons choisi d'utiliser un ORM pour limiter les risques liés aux injections SQL. En passant par cet outil, on évite de manipuler directement les requêtes SQL, ce qui rend l'application plus sûre. L'ORM se charge de gérer les interactions avec la base de données de manière sécurisée, sans qu'on ait à se soucier des failles potentielles liées à des entrées non sécurisées. C'est une manière simple et efficace de renforcer la sécurité de notre projet.


## Sécurisation des connexions

Dans le but de nous prémunir contre les attaques de type Man In The Middle, nous implementerons le TLS afind de rendre les échanges entre le server et le client sécurisé. Ce dernier a pour but de vérifier la source de la communication, rendre les données illibles par les parties extérieures et de vérifier que la contenu n'a pas été altéré. Pour une efficacité maximale, nous le couplerons avec le HSTS afin de s'assurer qu'absolument toutes les connexion utilisent le protocole HTTPS.



## GESTION DES AUTHENTIFICATIONS
Nous appliquerons de bonnes pratiques pour la gestion des autorisations. A commencer par la gestion contrôlée des jetons de connexion. Nous utiliserons la technologie JWT pour sécuriser l'autorisation de connexion côté client de manière sécurisée.<br>
```
Bonnes pratiques mises en place pour le token de connexion:
- Les jetons ne contiendront pas d'informations sensibles
- Les jetons serons chiffrés avec l'algorithme sha-256
- L'émetteur du jeton devra être validé
```

Pour contrer les attaques de tentative de vol de mot de passe par force brute ou par dictionnaire nous limiterons le nombre de tentatives de connexion dans le temps.

## APPELS API
Afin de contrer les attaques de type DDOS nous limiterons le nombres d'appels autorisés dans le temps.

## 3.2 - BASE DE DONNEES

### SAUVEGARDE
Une bonne planification de la stratégie de sauvegarde est nécéssaire afin de garantir la sécurité des données des utilisateurs en cas d'attaque de type ranswomware ou de défaillance technique ou humaine. Dans cette optique nous avons opté pour une automatisation de la sauvegarde de la base dans de données dans la nuit au moment ou le pic d'utilisation est moindre pour éviter d'éventuels dysfonctionnement du système.<br>
Nous avons opté pour la stratégie de sauvegarde 3-2-1 : 
- 3 copies de toutes les données de sauvegardes
- 2 types de stockages différentes
- 1 copie de la sauvegarde sur un site différent (ou cloud)
Nous garderons les quinze dernières sauvegardes et celles-ci seront effectuées chaque jour à minuit, heure à l'actuelle l'affluence de la plateforme sera moindre pour eviter les perturbations du service.

### politique de mot de passe

Il convient d’observer quelques règles spécifiques afin de garantir une sécurité optimale des mots de passe des utilisateurs. Dans cette optique :
Une vérification devra être effectuée avant de valider un nouveau mot de passe pour attester de :
- L’utilisation correcte de caractères minuscules, de majuscule, de chiffre et de caractère spécial.
- La longueur minimale est respectée en adéquation avec le type de compte.
Une limite de tentatives de connexion devra néanmoins être appliquée au vu de la nature d’application web du système dans le but de se prémunir d’éventuelles attaques par déni de service.
- L'absence de données personnelles telles que le nom, l’âge ou la date de naissance.
- Les mots de passe ne devront pas être stockés en clair dans la base de données, on leur préférera une utilisation de la méthode hashage – salage.
- La durée des sessions authentifiées sera limitée dans le temps, pour certaines actions (comme la suppression d’un cours), une reconnexion sera exigée.
- Le nombre de tentatives de connexions devront être limitées par un captcha au bout de quelques tentatives puis verrouillées dans le temps afin de se prémunir des tentatives d’assaut par force brute
- La demande de réinitialisation de mot de passe devra s’effectuer via un lien à durée de vie limitée envoyé sur le mail associé au compte.
- Lors de la création de mot de passe, ajouter un texte de sensibilisation aux bonnes pratiques de création d’un mot de passe sécurisé.



### RGPD

La collecte et le traitement de données personnelles sont réglementés par la RGPD, de fait une attention particulière sera apportée sur ce sujet:
- En commençant par demander le consentement du visiteur pour la collecte et l’utilisation de ses données personnelles.
- En lui exposant de manière claire et transparente comment sont traitées les informations et dans quel but via les mentions légales.
- En ne demandant de renseigner que les données utiles.
- Par ailleurs les données ne seront pas stockées et traitées de la même manière, au vu du caractère sensible de certaines données la CNIL impose des restrictions plus importantes pour certaines données.
- Garder à l'esprit que les visiteurs ayant partagé leurs données personnelles doivent garder le contrôle sur ces dernières. Dans ce cadre trois grands principes seront appliqués:
- Droit de consultation : les utilisateurs doivent être en mesure de consulter librement à tout moment leurs données personnelles.
- Droit de rectification : les utilisateurs doivent être en mesure de pouvoir modifier librement les données qu’ils ont partagées.
- Droit à l’oubli : les utilisateurs ont le droit de pouvoir supprimer de manière complète et définitive les données qu'ils ont communiquées.
- Si le système d’information venait à être compromis, les utilisateurs concernés doivent être avertis sous soixante-douze si la violation représente un risque pour leurs droits et libertés.<br>
Les règles de sécurité proposées tout au long de ce document ont pour vocation d’apporter une sécurité maximale de l'intégrité et de la confidentialité de toutes les données stockées (Privacy by Design) . Cette section a pour but de clarifier les points nécessitant une attention particulière du fait de la réglementation RGPD.


## 4-FRONTEND


### Controle des souces externes

Le contrôle des ressources externes est un facteur a prendre dans notre stratégie de sécurité. Bien qu'une sécurité soit mise en place dans le navigateur du client via Same Origin Policy qui restreint par défaut les ressources accessible a notre propre domaine, elle peut s'avérer limitante, et devrant être contournée. Nous utiliserons des règles CORS bien précises afin de limiter l'acception des ressources provenant d'origines bien définies.<br>
Nous couplerons cette règle avec des limitations sur les types de ressources accéptées via des régles CSP dans le but de n'autoriser que certaines types de ressources bien définies.<br>
Nous vérifierons ensuite l'intégrité des ressources externes demandées avec SRI afin de s'assurer que les ressources demandées soient bien conformes et non altérées comme prévue.
**Exemple d'utilisation avec boostrap**
```
1. Autoriser le domaine cdn.jsdelivr.net (CORS)
2. N'autoriser que les fichiers.css (CSP)
3. Verifier l'integrité dans la balise (SRI)
```

### Gestion des entrées utilisateur

Nous incorporerons une vérification stricte des entrées utilisateur afin de garantir que celles ne comportent pas de risques via l'utilisation de regex. Cela nous garantira de ne laisser passer aucune potentielle injection de script.

**Exemple d'expression de regex pour un mail**
 `^[\w\.=-]+@[\w\.-]+\.[\w]{2,3}$` 


### Obscurcissement des messages d'erreurs
Nous nous assurerons que tout les messages d'erreurs soient le plus cryptique possible afin d'eviter de divulguer des indices sur les données données stockées : 

**Exemple**
```
 John.Doe@exemple.com
Erreur: L'utilisateur John Doe n'existe pas !
```

Cet exemple donne l'information que cet email n'est pas enrigistré dans la base de données.

## 5 - CONCLUSION

Face aux différentes menaces qui existent, l'utilisation d'un framework et d'un ORM, couplée avec une utilisation judicieuse des règles d'hygiène élémentaires de codage nous permettra de sécuriser au maximum l'application. Ces principes seront appliqués a plusieurs niveaux au titre de la défense en profondeur en vue de garantir l'intégrité du système d'informations.




