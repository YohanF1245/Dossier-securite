2 - RÈGLES DE SÉCURITÉ TRANSVERSALES


La présente section a pour but de présenter le socle de règles et de bonnes pratiques qui serviront à construire les fondations d’une application sécurisée. Seront présentées dans cette partie les dispositions utiles à toutes les couches de l’application et les éléments de sécurité situés à mi-chemin entre deux couches. Seront détaillés également les concepts plus généraux d’hygiène de sécurité qui ne s’apparente pas spécialement à une couche ou une menace particulière.


2.1 - Défense en profondeur

La défense en profondeur repose sur l'implémentation de multiples mesures de protection indépendantes pour chaque menace identifiée. Ce principe s'applique plus efficacement lorsque le système est segmenté en unités distinctes, avec des interactions bien définies et des mécanismes de sécurité propres à chacune. Une approche incorrecte consisterait à concentrer toutes les protections au niveau de l'entrée du système, laissant ainsi les composants internes vulnérables en cas de faille en amont. Chaque composant logiciel de l'application, ainsi que l'infrastructure d'hébergement, doit idéalement contribuer à la sécurité globale du système.


2.2 Moindre privilège

Ce principe consiste à accorder aux composants et utilisateurs du système uniquement les permissions nécessaires à leur fonctionnement, afin de réduire les risques de vol, d'altération ou de destruction de données en cas de compromission de certains éléments.


	2.2.a RBAC(Role Based Access Control)

	Le contrôle d'accès basé sur les rôles (RBAC) attribue des permissions aux utilisateurs selon leur rôle au sein de l'organisation. Chaque rôle regroupe des droits spécifiques, limitant ainsi l'accès aux données sensibles uniquement à ceux qui en ont besoin pour leur fonction. Cette approche réduit les risques de sécurité et facilite la gestion des accès, renforçant ainsi la protection des données. Il est à noter que la gestion des autorisations des groupes authentifiés doit être complétée d’une politique de gestion des accès pour les utilisateurs non-authentifiés.


2.3 Réduction de la surface d'attaque

La réduction de la surface d’attaque consiste à limiter l'exposition des services, des points d'entrée et des composants logiciels non essentiels pour diminuer les risques d'exploitation des vulnérabilités. Cela implique de désactiver les services inutiles, de restreindre les accès aux interfaces, et d'éliminer les dépendances superflues dans le développement logiciel. En parallèle, il est crucial de segmenter le réseau, d'utiliser des mécanismes de validation et de journaliser les accès pour détecter toute activité suspecte. En intégrant ces pratiques, on renforce la sécurité globale du système.


2.4 Sécurité des échanges de données

La sécurité des échanges de données est cruciale pour garantir que les informations soumises ou reçues ne soient ni interceptées ni modifiées. Ce principe est particulièrement important pour les données personnelles, conformément à la loi informatique et libertés et au RGPD. L’objectif est d’assurer que les données proviennent bien du site consulté et non d’une source frauduleuse. Pour cela, l'utilisation du protocole HTTPS est essentielle, car il chiffre les communications et protège ainsi la confidentialité, l'intégrité et l'authenticité des données échangées sur le Web.


	2.4.a Utilisation de TLS

	La mise en place de TLS (Sécurité de la Couche de Transport) permet d’accroître le niveau de sécurité et de confidentialité lors des échanges client-serveur en satisfaisant trois principes clés :
S’assurer de l’authenticité du serveur contacté (via émission d’un certificat d’authentification asymétrique)
S’assurer de la confidentialité, en chiffrant les données qui transitent
S’assurer de l’intégrité des données (via hashage)


	2.4.b Utilisation de HSTS

	TLS sera utilisé conjointement avec HSTS (HTTPS Strict Transport Security) afin de garantir que absolument tous les échanges se font par HTTPS. Cette restriction a pour but d’empêcher un individu malveillant d’intercepter la communication et la rediriger vers une version non sécurisée du site (HTTP), cette attaque est connue sous le nom de Man-In-The-Middle.


	2.4.c Utilisation de CT

	Mise en place de Certificate Transparency afin de garantir un environnement sain en s’assurant que lors des échanges client-serveur le certificat utilisé est bien référencé dans les journaux tenus à jour par les autorités de certification.


2.5 Conformité du contenu présenté

L'objectif de la conformité du contenu d'un site ou d'une application web est de garantir que le navigateur affiche correctement l'application selon l'intention du développeur, en empêchant toute altération malveillante ou imprévue durant l'échange des données.
2.6 Audit

Au-delà de toutes les mesures prises en termes de sécurité, il est à noter qu’elles sont à accompagner de mesures intra ou post conception telles que :
Les outils de détection de dépendances vulnérables
Les outils de monitoring
Les tests de pénétration
Rentre également dans cette catégorie la mise en place de journaux d'événements permettant de tracer les actions effectuées et les dysfonctionnements du système.



2.7 Politique de mots de passe

Il convient d’observer quelques règles spécifiques afin de garantir une sécurité optimale des mots de passe des utilisateurs. Dans cette optique :
Une vérification devra être effectuée avant de valider un nouveau mot de passe pour attester de :
L’utilisation correcte de caractères minuscules, de majuscule, de chiffre et de caractère spécial.
La longueur minimale est respectée en adéquation avec le type de compte.
Une limite devra de longueur de mot de passe devra néanmoins être appliquée au vu de la nature d’application web du système dans le but de se prémunir d’éventuelles attaques par déni de service.
L'absence de données personnelles telles que le nom, l’âge ou la date de naissance.
Les mots de passe ne devront pas être stockés en clair dans la base de données, on leur préférera une utilisation de la méthode hashage – salage.
La durée des sessions authentifiées sera limitée dans le temps, pour certaines actions (comme la suppression d’un cours), une reconnexion sera exigée.
Le nombre de tentatives de connexions devront être limitées par un captcha au bout de quelques tentatives puis verrouillées dans le temps afin de se prémunir des tentatives d’assaut par force brute
La demande de réinitialisation de mot de passe devra s’effectuer via un lien à durée de vie limitée envoyé sur le mail associé au compte.
Lors de la création de mot de passe, ajouter un texte de sensibilisation aux bonnes pratiques de création d’un mot de passe sécurisé.

