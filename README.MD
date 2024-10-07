# Security strategy
- [1 - Introduction](#1---introduction)
- [2 - Règles générales](#2---regles-generales)
    - [Défense en profondeur](#défense-en-profondeur)
    - [Réduction de la surface d'attaque](#réduction-de-la-surface-dattaque)
    - [RGPD](#rgpd)
- [ - Backend](#--backend)
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

Pour garantir une efficacité maximale de la stratégie de sécurité, nous appliquerons le principe de défense en profondeur. En superposant les règles de sécurités, nous nous couvrons en cas de vulnérabilité de l'une d'entre elle.

### Réduction de la surface d'attaque

L'une des erreurs dans le développement d'application web est la multiplication des points d'entrées de l'application (OS du serveur, librairies, addresses IP). Nous appliquerons le principe de réduction de la surface d'attaque pour limiter les points de vulnérabilité de l'application.

### RGPD

Le traitement de données est hautement encadré. Nous nous conformerons à la réglementation en vigueur via plusieurs règles détaillées plus tard dans les présentations en détail des différentes couches. 

## - BACKEND

### Moindre privilège

Nous appliquerons le principe du moindre privilège afin de réduire la virulence de potentielles attaques venant de comptes utilisateurs compromis. Moins un utilisateur a de droits, moins sa puissance de frappe est grande.

### RBAC

Nous mettrons en place un RBAC pour gérer les permissions des utilisateurs groupe par groupe. Cela va de paire avec le principe du moindre privilège car il nous offrera un moyen simple d'octroyer les autorisations aux utilisateurs (authentifiés ou non).
- Visiteur (non authentifié): consulter des cours (ou un apercu)
- Apprenant : consulter et s'inscrire a des cours
- Coach : rédiger des cours
- Admin : tout les droits de création, suppression, édition ou consultation

## - API
