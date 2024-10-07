4 - API

L’api fait le lien entre le client et la base de données, de ce fait, de nombreux facteurs sont à prendre en compte concernant la sécurité de cette dernière. Comme présenté dans le paragraphe 2.4 des précautions sont prises au niveau de la transmission des données, et dans le 2.7 sur la politique des mots de passe. Afin de renforcer les connexions entre client et API les jetons de connexions JWT seront employés avec des durées de vie courtes afin de limiter l’impact d’un éventuel vol de token.



4.1 Server-Side Request Forgery (SSRF)

Contexte: Le SSRF est une faille qui permet à un attaquant de tromper un serveur en le forçant à faire des requêtes HTTP vers des ressources  internes ou externes, sans qu’il soit directement impliqué. 

Solutions : 
Validation et nettoyage des données (sanitisation): Mise en œuvre d’une politique stricte de vérification des entrées utilisateurs afin de vérifier qu’elles ne comportent aucune entrée visant à porter atteinte à l'intégrité de l’application.
Liste blanche de domaine: Pour éviter l’accès au ressources internes du serveur, une liste blanche de noms de domaines sera utilisée pour bloquer par exemple les adresses IP locales (localhost).

4.2 XXE et Configuration de sécurité

Contexte: Le XXE (XML External Entity), ou injection d'entités externes XML, est une vulnérabilité de sécurité qui se produit lorsqu'un parseur XML non sécurisé traite des données XML fournies par un utilisateur. Cette faille permet à un attaquant d'injecter des entités externes XML malveillantes, pouvant entraîner des accès non autorisés aux fichiers du serveur, une exécution de code à distance, des attaques par déni de service (DoS), et même des attaques sur des services internes via des requêtes HTTP. Dans le rapport de l’OWASP sur les failles de sécurité les plus communes, ce type de faille est désormais classé dans la catégorie “Security Misconfiguration “

Solutions:
Désactiver les entités externes dans les parseurs XML: Désactiver au si possible cette fonctionnalité reste le moyen le plus sûr de se prémunir contre cette vulnérabilité.
Validation et nettoyage des entrées utilisateurs: Un contrôle strict des entrées utilisateur permet d’éviter les entités XML externes malveillantes.
Privilégier le JSON.
Limiter les permissions du serveur(moindre privilège): En cas d’attaque XXE réussie, si le serveur n’a que des privilèges minimaux les conséquences seront moindre.
Restreindre le nombre de features installées ou activées:(ports non nécessaires, services, pages, comptes)
Supprimer les comptes par défaut.
Gérer adéquatement les messages d’erreurs: Les messages d’erreurs ne doivent pas donner d’indices sur les dysfonctionnements du service.
Configuration des options du serveur et du framework: Une attention particulière doit être portée aux options de configuration du serveur et du framework, ainsi que des dépendances installées.
