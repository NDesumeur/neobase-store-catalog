# Faire approuver un plugin

Un plugin **approuvé** est un plugin que NeoDex a examiné : son code, ses autorisations, ses dépendances
et son comportement. Il porte une **attestation signée** (ed25519) liée à l'empreinte exacte de son archive.
NeoStore l'affiche « ✓ approuvé », l'installe sans avertissement et peut lui accorder l'accès complet à
NeoDex (jamais d'office : l'utilisateur doit l'accepter à la première ouverture).

Un plugin **non approuvé** reste installable : NeoStore le montre « non vérifié », le fait passer à
l'antivirus et demande confirmation. Il ne peut jamais recevoir l'accès complet.

## Comment demander

1. Publie ton plugin selon le [guide de publication](https://github.com/NDesumeur/neodex-sdk/blob/main/docs/PUBLIER.md)
   (dépôt public, topic `neodex-plugin`, Release avec l'archive).
2. Ouvre une *issue* dans ce dépôt avec le modèle « Proposer un plugin ».
3. Le suivi se lit sur les labels de l'issue : `reçue` → `en cours d'examen` → `approuvée` ou `refusée`.

## Ce qui est examiné

| Point | Ce qu'on vérifie |
|-------|------------------|
| Code | rien de caché ou d'obscurci ; pas de code chargé depuis Internet ; pas d'envoi de données à un tiers sans que l'utilisateur le sache |
| Autorisations | le minimum nécessaire, chacune justifiée dans la demande ; `full` seulement si le plugin ne peut pas faire autrement |
| Données | rangées dans `ctx.folder` ; rien d'écrit ailleurs ; pas de lecture des données d'un autre plugin sans `uses` |
| Dépendances | déclarées dans `dependencies`, elles aussi approuvées |
| Contenu | pas de contenu dont tu n'as pas les droits (images, textes, polices) ; licences indiquées |
| Comportement | s'installe, s'ouvre, se ferme et se désinstalle sans erreur, sans ralentir NeoDex |
| Archive | `plugin.json` valide, `id` et `version` cohérents avec la Release |

Un plugin qui réclame plus d'autorisations que nécessaire ou qui ne s'explique pas est refusé, avec la raison.

## Après l'approbation

- L'attestation (`attestation.json`) est jointe à ta Release et ton plugin est ajouté à `index.json`.
- Elle ne vaut que pour **cette version** : chaque nouvelle version est examinée à nouveau (plus vite
  si seuls quelques fichiers ont changé).
- Ton code reste dans **ton** dépôt ; le catalogue ne le recopie jamais.

## Révocation

Si un problème de sécurité ou de compatibilité apparaît, l'entrée est ajoutée à `revoked` dans
`index.json`, avec la raison. NeoDex refuse alors le plugin, même si sa signature est valide.
