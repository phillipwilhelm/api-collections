## Principe général

Toutes les requêtes retournent :
* un code HTTP 200 (OK) : en cas de succès
* un code HTTP 400 (Bad Request) : lorsque des paramètres sont inconnus. 
* un code HTTP 406 (Not Acceptable) : lorsque les données fournies ne permettent de traiter la demande
* un code HTTP 500 (Internal Server Error) : en cas d’erreur indéterminée

Les appels API se font uniquement en HTTPS.

## Authentification

This API uses the authentication system for published data.

Il y a 2 types d'authentification différentes :
* pour controller l'accès aux données publiées par IBOO en utilisant la variable d'environnement publication_api_key
* pour controller l'accès aux ressources internes gérés par IBOO en utilisant la variable d'environnement api_key

Ces 2 authentifications se font via des clés d'API sous la forme d'un en-tête de demande API Key.

Pour la publication, il est possible de la générer en allant dans le menu Paramétrages > Publications > API de publication.

Pour les échanges internes, il est possible de la générer en allant dans le menu Paramétrages > Sécurité
