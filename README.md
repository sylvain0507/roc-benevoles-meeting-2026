# ROC · Bénévoles du Meeting Royan Atlantique 2026

Application mobile et ordinateur pour proposer son aide au meeting des **24 et 25 octobre 2026** et aux missions de préparation.

- 39 postes et créneaux repris de « Planning postes » dans ROC_Natation_Recensement_Benevoles_Meeting_2026.xlsx.
- Besoins minimum et idéal du fichier ; les cinq postes Officiels FFN / jury ont un besoin à définir par le club.
- Un poste proposé par séance pour éviter de compter une même personne deux fois sur des postes simultanés. Les heures précises ne figurent pas dans le fichier et restent à communiquer par le club.
- Les propositions deviennent des affectations confirmées après validation par le club. Le suivi compare les confirmés aux besoins ; l’idéal est une cible et ne bloque pas les propositions supplémentaires.
- E-mail et code personnel à quatre chiffres pour retrouver, ajouter ou annuler ses postes. Les codes sont hachés côté serveur et les tentatives limitées.
- Espace club protégé : validation et réaffectation, suppression, coordonnées, besoins, fermeture des inscriptions et actions logistiques.
- Export Excel local avec trois onglets : Bénévoles, Répartition, Actions logistiques. Textes explicitement stockés comme textes pour éviter les formules injectées.
- Aucun paiement, e-mail, achat ou invitation n’est envoyé par cette application.

## Hébergement et données

GitHub Pages héberge l’interface. Le service Sites / Cloudflare D1 conserve les inscriptions partagées. Les coordonnées, affectations nominatives, actions internes, codes privés et le fichier Excel original ne sont jamais déposés sur GitHub. Les seuls éléments visibles publiquement sont le planning, les besoins et les effectifs agrégés.

ADMIN_KEY est une variable secrète du service. Ne jamais inclure sa valeur dans les sources. Les deux affectations initiales et les huit actions logistiques sont importées uniquement dans la base privée, via une opération d’administration idempotente.

## Développement

`npm install`, `npm run db:generate`, puis `npm run build`. `db/schema.ts` définit la base et `drizzle` contient ses migrations. Ne jamais modifier une migration publiée. `worker.js` exécute les contrôles serveur et les écritures atomiques ; une contrainte empêche les doubles affectations sur la même séance. Un déclencheur protège les postes fermés, y compris en cas d’inscriptions concurrentes.

Le dépôt sert les fichiers de `public` à sa racine ; `source-complete.zip` contient les sources du service, l’interface et les migrations sans données personnelles.
