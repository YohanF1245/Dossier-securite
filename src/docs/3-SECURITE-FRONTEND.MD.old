3 - FRONTEND

3.1 Cross-Site Scripting (XSS)


Contexte : Une attaque XSS (Cross-Site Scripting) est une technique où un attaquant insère du code malveillant (généralement du JavaScript) dans une application web accessible par d'autres utilisateurs. Ce code est alors exécuté côté client, exploitant la confiance que les utilisateurs ont envers le site pour voler des informations sensibles, modifier le contenu affiché, ou prendre le contrôle de sessions utilisateur.
Solution : 
	Afin de se prémunir des attaques XSS il convient d’appliquer les mesures suivantes:
L’utilisation d'éléments javascript et CSS inline est à proscrire. La structure doit être clairement établie en séparant HTML, JAVASCRIPT et CSS.
Toute modification doit être réalisée via l’API DOM.
Mise en œuvre de Content Security Policy (CSP). CSP permet de contrôler l’origine des ressources accessibles par le navigateur en instaurant une liste blanche. Aussi, une ressource déclarée mais non validée par le CSP se verra bloquée ou ignorée.
Une attention particulière sera apportée aux formulaires et à toute autre situation ou la saisie d’informations est proposée à l'utilisateur (validation des entrées, échappement des caractères HTML, sanitisation)
Vérifier l’intégrité des ressources exploitées qu’elles soient d’origine extérieure ou propres au domaine.


3.2 Cross-Site Request Forgery (CSRF)


Contexte : Le CSRF est une attaque où un pirate incite un utilisateur connecté à un site web à exécuter des actions non voulues, comme changer un mot de passe ou effectuer un paiement. Le site traite ces actions comme légitimes parce que l'utilisateur est déjà authentifié, mais l'utilisateur ne les a pas initiées volontairement.
Solution :
	Afin de se prémunir des attaques de type CSRF il convient d’appliquer les mesures suivantes: 
Jetons CSRF (CSRF Tokens) : Inclure un jeton unique et aléatoire dans chaque formulaire ou requête sensible. Ce jeton est vérifié par le serveur pour s'assurer que la requête provient de l'utilisateur légitime.
Vérification du référent HTTP (HTTP Referer Header) : Vérifier que les requêtes proviennent du même domaine que celui du site web, en validant le header Referer ou Origin de la requête.
Expiration des sessions : Limiter la durée des sessions et forcer une reconnexion après un certain temps d'inactivité.
Limiter le transit des cookies aux flux sécurisés 
Définir une stratégie stricte d’envoi des cookies de session en cross-site. Pour un cookie de session, l’attribut samesite doit être défini.


3.3 Clickjacking

Contexte: Le clickjacking est une attaque qui consiste à tromper un utilisateur en lui faisant cliquer sur un élément invisible ou déguisé dans une page web, souvent avec des conséquences nuisibles (par exemple, validation d'un formulaire ou exécution d'une commande sans son consentement). Pour s'en défendre, plusieurs mesures peuvent être mises en place.

Solution : Afin de se prémunir des attaques de type clickjacking il convient d’appliquer les mesures suivantes: 
Mise en place d’une directive CSP interdisant d’incorporer cette application dans un autre site au moyen d’une iframe autre que notre propre domaine (Content-Security-Policy: frame-ancestors 'self')
Le précédent point sera complété par la directive similaire X-Frame-Options: sameorigin, pour des raisons de compatibilité avec certains navigateurs. Cela contribue à augmenter la défense en profondeur.

3.4 Web Storage, IndexedDB et Cookies

Il convient d’observer quelques règles lors de l’utilisation du stockage local côté navigateur. Un premier élément de sécurité instauré par défaut par le navigateur est la politique de même origine (SoP). A cet égard les précautions suivantes seront mises en place:
Proscrire le stockage d’informations sensibles dans les bases de données locales et dans les bases de données IndexedDB.
L’utilisation de l’API Web Sql Database étant obsolète, son usage se voit aussi interdit.
Les cookies sont une solution de stockage temporaire et au volume réduit disposant d’une durée de vie déterminée. Là aussi le stockage de données sensible est à éviter, néanmoins les propriétés de configuration des cookies font de lui un bon réceptacle pour les jetons de sessions sous réserve de paramétrer ces derniers correctement.

4.5 XHR, CORS et Fetch
	Par défaut, les navigateurs appliquent une politique de même origine (Same-Origin Policy) pour des raisons de sécurité. Cela signifie qu'un script exécuté sur une page web d'une origine donnée ne peut pas accéder aux ressources d'une autre origine. CORS permet de surmonter cette restriction en définissant des règles spécifiques pour autoriser certaines requêtes inter-domaines. Certaines mesures sont à respecter pour limiter les risques:
Appliquer une limite sur les origines autorisées. Il est vital d’être précis dans la définition des domaines autorisés. L’utilisation de de l’astérisque pour autoriser toutes les sources est à proscrire.
Appliquer une limite sur les méthodes HTTP en ne conservant que les méthodes nécessaires (GET, POST, PUT).
Contrôler les en-têtes autorisés. Définir avec précision les en-têtes autorisées dans les requêtes.
Configurer les requêtes preflight pour prendre en charge les requêtes options afin de permettre au navigateur de vérifier les autorisations avant d'effectuer la requête principale.

	XmlHttpRequest et fetch sont deux solutions pour effectuer des requêtes api. Pour la clarté de sa syntaxe, son meilleur support de CORS et sa simplicité, fetch est à privilégier dans la plus grande majorité des cas. XHR peut néanmoins être utilisé de manière raisonnée pour certains usages spécifiques ou pour des raisons de compatibilité avec les navigateurs plus anciens. Les mesures apportées à l'utilisation des apis sont les suivantes : 
Il est impératif de s’assurer de l’utilisation d’une connexion sécurisée (https://) pour contrer les attaques de type Man in the Middle.
S’assurer que le contenu de la réponse soit sous un format non exécutable par le client (JSON ou XML).
Choisir la méthode http adéquate:
Limiter au maximum l’emploi de la méthode GET, et uniquement pour la récupération de données publiques non sensibles sans changer l’état des données.
Utiliser la méthode POST pour limiter le risque de données.
Utiliser la méthode PUT pour limiter le risque CSRF.
Ajouter une une configuration CSP et un contrôle anti CSRF pour contrôler les risques
