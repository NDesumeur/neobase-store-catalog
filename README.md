# Catalogue officiel NeoStore

Ce dépôt est le catalogue central des plugins NeoDex. NeoStore le lit pour afficher les plugins
approuvés, leurs versions et leurs liens, et il refuse les plugins dont l'approbation a été retirée.

- `index.json` — la liste des plugins approuvés et la liste de révocation (voir `catalog.schema.json`).
- La découverte ne se limite pas au catalogue : NeoStore trouve aussi les plugins **proposés** en
  cherchant les dépôts GitHub portant le topic **`neodex-plugin`**. Le catalogue, lui, ne contient
  que les plugins **approuvés** (attestation signée valide).

## Proposer un plugin

Pour proposer un plugin à l'approbation officielle :

1. Publie ton plugin dans un dépôt avec le topic `neodex-plugin` et une Release (voir le SDK).
2. Ouvre une *issue* ici avec le lien du dépôt, la version, les permissions demandées et un résumé.
3. Suivi de la proposition : `reçue` → `en cours d'examen` → `approuvée` ou `refusée`, via les labels
   de l'issue.

Après examen (code, dépendances, permissions, téléchargement, comportement), un plugin approuvé
reçoit une attestation signée et est ajouté à `index.json`. Son code reste dans **son** dépôt : il
n'est jamais recopié ici.

## Révocation

Si un problème de sécurité ou de compatibilité est découvert, l'entrée correspondante est ajoutée à
`revoked` dans `index.json`, avec la raison. NeoDex refuse alors ces plugins même si leur signature
est valide.
