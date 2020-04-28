# fiche_JWT
Le jason web token est un standard ouvert défini dans la RFC 7519. Il permet l'échange sécurisé de jetons (tokens) entre plusieurs parties.
Cette sécurité de l'échange se traduit pas la vérification de l'intégrité des données à l'aide d'une signature numérique qui s'effectue par l'algorithmr HMAC ou RSA.

Un jeton se compose de trois parties :

Un en-tête (header), utilisé pour décrire le jeton. Il s'agit d'un objet JSON.
Une charge utile (payload) qui représente les informations embarquées dans le jeton. Il s'agit également d'un objet JSON.
Une signature numérique.

exemple en-tête : 
{"typ": "jwt", "alg": "HS512"}

exemple charge utile : 
{"name":"Wikipedia","iat":1525777938}

Obtenir la signature :
Il faut tout d'abord encoder séparément l'en-tête et la charge utile avec Base64url défini dans la RFC 46482. Ensuite, on les concatène ensemble en les séparant avec un point. On obtient la signature de ce résultat avec l'algorithme choisi. Cette signature est ajoutée au résultat de la même manière (encodée et séparée par un point).

À noter que pour l'encodage en Base64url, le caractère de remplissage '=' n'est pas obligatoire3 et ne sera pas utilisé dans la création du JSON Web Token pour faciliter la transmission dans une URL.

Procédure étape par étape
À partir de l'exemple ci-dessus, voici les différentes étapes pour obtenir un JSON Web Token.

Encodage de l'en-tête

eyJ0eXAiOiAiand0IiwgImFsZyI6ICJIUzUxMiJ9
Encodage de la charge utile

eyJuYW1lIjoiV2lraXBlZGlhIiwiaWF0IjoxNTI1Nzc3OTM4fQ
Concaténation des deux éléments, séparation par un point

eyJ0eXAiOiAiand0IiwgImFsZyI6ICJIUzUxMiJ9.eyJuYW1lIjoiV2lraXBlZGlhIiwiaWF0IjoxNTI1Nzc3OTM4fQ
Obtention de la signature avec l'algorithme HMAC-SHA5124.

HMACSHA512(concatenation, 'ma super clé secrète')
Encodage de la signature (toujours avec Base64url)

iu0aMCsaepPy6ULphSX5PT32oPvKkM5dPl131knIDq9Cr8OUzzACsuBnpSJ_rE9XkGjmQVawcvyCHLiM4Kr6NA
Concaténation des deux éléments, séparation par un point

eyJ0eXAiOiAiand0IiwgImFsZyI6ICJIUzUxMiJ9.eyJuYW1lIjoiV2lraXBlZGlhIiwiaWF0IjoxNTI1Nzc3OTM4fQ.iu0aMCsaepPy6ULphSX5PT32oPvKkM5dPl131knIDq9Cr8OUzzACsuBnpSJ_rE9XkGjmQVawcvyCHLiM4Kr6NA
