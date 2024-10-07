5 - BASES DE DONNÉES

5.1 Injections SQL(SQLi)

Contexte : Une vulnérabilité où un assaillant injecte du code malveillant dans le but de compromettre l’intégrité de la base de données.

Solutions :

Utilisation d’un ORM :  Du fait de sa propension à transformer des objets en requêtes SQL, Object-Relational Mapping est un bon candidat pour ajouter une couche de protection contre les injections SQL.
Mise en place de requêtes préparées: Dans le cas où les restrictions apportées par les ORM ne permettent pas de communiquer avec la base de données de la manière souhaitée, les prepared statements doivent être préférés à toute autre méthode. Les concaténations sont à proscrire impérativement.
Principe du moindre privilège : En ne donnant que les permissions adéquates à chaque type d’utilisateurs, le risque de détérioration est amoindri (un élève n’a pas besoin d’écrire dans la table des cours par exemple).
Validation et nettoyage des entrées : Mise en place d’un système de regex qui permet de valider les entrées (le format d’une adresse e-mail), de limiter la taille des entrées où de supprimer des caractères potentiellement dangereux.
Journalisation des activités : Mise en place d’un journal retraçant l’historique des requêtes et surveillant les éventuelles tentatives d’injection SQL.
Web Application Firewall : Mise en place d’un pare-feu applicatif permettant d’analyser le contenu des requêtes et tenter de repérer des motifs suspects. En outre il permet, via des règles prédéfinies d’identifier des requêtes suspectes en se souciant de certains mots-clés spécifiques (exemple : SELECT, UNION, INSERT) où s’adapter à une logique spécifique via des règles personnalisées.


5.2 Attaques par déni de services (DoS)

Contexte : Une attaque visant à saturer en multipliant les requêtes vers un serveur le rendant indisponible pour les utilisateurs.

Solutions :
Rate limiting : Mise en place d’une limitation du nombre de requêtes par utilisateur sur une période donnée visant à réduire le risque d’épuisement des ressources serveur.
Surveillance : Mise en place d’un outil permettant d’analyser le trafic afin de détecter les pics qui pourraient suggérer une attaque DoS.
Réplication et répartition de charge : Mise en place de plusieurs serveurs pour la base de données permettant de répartir le trafic et limiter le risque de surcharge d’un serveur.
Caching : Mise en place d’un système de cache de requêtes pour stocker temporairement les requêtes fréquemment utilisées afin de réduire le nombre d’appel à la base de données.
Web Application Firewall : Mise en place d’un pare-feu qui va analyser le trafic en amont et bloquer les requêtes suspectes avant qu’elles n’atteignent la base de données. Les pare-feux offrent un système de liste noire qui permet de bloquer les adresses IP malveillantes connues.

5.3 Élévation de privilèges

Contexte : Dans le cas où un assaillant arrive à bénéficier de privilèges plus élevés qu’il ne devrait avoir, la sécurité de la base de données serait hautement compromise.

Solutions :
Principe du moindre privilège : En ne donnant que les privilèges nécessaires à l’utilisation prévue pour chaque groupe d’utilisateurs, le risque d’élévation de privilège se voit amoindri.
Sécurité renforcée sur les comptes dits « sensibles » :  Limite du nombre de comptes à haut niveau de privilèges et mise en place de mesures plus draconiennes sur la sécurité des comptes avec le plus de privilèges, notamment dans le cas du compte administrateur. Une attention particulière sera accordée à ce dernier (longueur minimum plus longue, sessions d’authentification plus courtes, mot de passe a durée de vie limitée)


5.4 Sauvegarde des données

Afin de préserver les données des utilisateurs en cas de défaillance matérielle ou logicielle, ou de les protéger contre des attaques de type ransomware visant à rendre les données inutilisable, il est nécessaire d’adopter une stratégie de sauvegarde de la base de données journalière, a une heure ou le pic d’utilisateur est au plus bas afin de ne causer aucune interruption de service. Toutefois il est nécessaire de mettre conjointement en œuvre une stratégie d’effacement des données rétroactive pour se conformer aux obligations légales liées aux concepts de rétention d’informations et de droit à l’oubli.

5.5 Protection des données

Afin de se conformer aux obligations légales imposées par la CNIL, un chiffrement des données sensibles sera mis en place. En outre, on imposera pour ces dernières un UUID comme identifiant. De par leur nature universellement unique, les UUID participent à la sécurité en ne révélant rien de la logique interne (contrairement à l’auto incrémentation).
