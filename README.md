🇫🇷 Explication détaillée du projet : Rick and Morty GraphQL API Explorer

Ce projet est un parcours d’apprentissage complet qui te fait progresser étape par étape, depuis les bases de GraphQL jusqu’à la construction d’une application React/Next.js entièrement fonctionnelle qui interroge une vraie API :
👉 Rick and Morty GraphQL API : https://rickandmortyapi.com/graphql

L’idée est de te faire apprendre :

comment écrire des requêtes GraphQL,

comment interagir avec une API GraphQL,

comment connecter cette API à un frontend moderne (Next.js + Apollo Client + TypeScript),

comment afficher ces données dans une interface utilisateur.

🧭 Structure globale du projet

Le projet est divisé en 4 niveaux (4 dossiers) :

Dossier	Niveau	Contenu principal
alx-graphql-0x00	Niveau 0	Écrire des requêtes GraphQL pures
alx-graphql-0x01	Niveau 1	Installer Next.js + TypeScript + Apollo Client
alx-graphql-0x02	Niveau 2	Faire des vraies requêtes GraphQL dans React
alx-graphql-0x03	(plus tard)	Features plus avancées

L’objectif : passer d’un simple fichier .graphql à une vraie application web complète.

🎯 Objectifs d’apprentissage
✅ Niveau 0 — Les bases de GraphQL

Tu apprends à :

écrire une requête GraphQL qui demande exactement les champs nécessaires

utiliser des arguments (id, page)

récupérer :

un personnage

une liste paginée de personnages

un épisode

comprendre ce qu'est :

query

les champs (id, name, etc.)

la pagination GraphQL (info.pages, info.next, etc.)

Ici tu n’as pas encore de frontend, uniquement des fichiers .graphql.

✅ Niveaux 1 & 2 — Intégration GraphQL dans une app React (Next.js)

Tu apprends à :

créer une application Next.js avec TypeScript

installer Apollo Client

connecter ton frontend à un endpoint GraphQL réel

exécuter une requête GraphQL avec useQuery

gérer l’état de pagination page

afficher les résultats dans des composants React

C’est ici que ton projet devient une vraie application web.

🔑 Concepts clés utilisés dans le projet
1. GraphQL Query Language

Tu écris des requêtes du genre :

query {
  character(id: 1) {
    id
    name
  }
}

2. Types GraphQL

L’API Rick & Morty fournit :

Character

Episode

Info

3. Pagination

L’API utilise un bloc info:

info {
  pages
  next
  prev
}

4. Apollo Client

C’est lui qui communique avec l’API GraphQL :

il envoie les requêtes

il gère le cache

il gère loading/error

il fournit useQuery

5. TypeScript

Tu crées des interface :

export interface EpisodeProps {
  id: number
  name: string
  air_date: string
  episode: string
}

🌍 OÙ UTILISE-T-ON GRAPHL POUR APPELER “RICK AND MORTY API” ?

Voici l’endroit exact où ton projet fait appel à l’API Rick and Morty.

⭐ 1. Dans apolloClient.ts
const client = new ApolloClient({
  link: new HttpLink({
    uri: "https://rickandmortyapi.com/graphql"
  }),
  cache: new InMemoryCache()
})


👉 Ici tu dis à Apollo :
“Toutes mes requêtes GraphQL iront vers cette URL : https://rickandmortyapi.com/graphql”

⭐ 2. Dans queries.ts
export const GET_EPISODES = gql`
  query getEpisodes($page: Int, $filter: FilterEpisode) {
    episodes(page: $page, filter: $filter) {
      info { pages next prev count }
      results { id name air_date episode }
    }
  }
`;


👉 Ici tu définis quoi tu veux demander à l’API Rick & Morty.

⭐ 3. Dans pages/index.tsx (Niveau 2)
const { loading, error, data, refetch } = useQuery(GET_EPISODES, {
  variables: { page: page }
})


👉 C’est ici que GraphQL est réellement exécuté depuis le frontend.

Apollo envoie la requête GET_EPISODES à l'API Rick and Morty.

La réponse est mise dans data.

Si page change → refetch() relance une requête.

🏗️ Résumé du fonctionnement complet

Voici le pipeline complet de ton projet :

Next.js → Apollo Client → Rick and Morty GraphQL API
                            ↓
                        Renvoie JSON
                            ↓
        Apollo stocke dans le cache → React affiche dans les composants

📦 Explication détaillée de chaque tâche
✨ Tâche 0 — Récupérer un personnage par ID

Tu écris :

character(id: 1)


Objectif : apprendre à cibler un item précis.

✨ Tâche 1 — Récupérer une liste paginée

Tu utilises :

characters(page: 2)


Objectif : comprendre la pagination.

✨ Tâche 2 — Récupérer un épisode par ID

Tu écris :

episode(id: 3)


Objectif : comprendre les Types GraphQL.

✨ Tâche 3 — Construire l’app Next.js (alx-graphql-0x01)

Tu installes :

TypeScript

Tailwind

Apollo

GraphQL

Tu configures :

apolloClient.ts

queries.ts

_app.tsx

👉 L'application peut maintenant appeler l'API.

✨ Tâche 4 — Afficher les données Episodes (alx-graphql-0x02)

Ici tu fais :

un composant EpisodeCard

un système de pagination

une vraie requête GraphQL dans React

une interface stylée Tailwind

👉 L’application affiche les épisodes en temps réel depuis l’API Rick & Morty.

🎉 Conclusion

Tu viens de créer un projet qui :

✔ apprend les bases de GraphQL
✔ construit une application Next.js moderne
✔ interroge un vrai endpoint API
✔ affiche les résultats dans une UI claire et paginée
✔ utilise TypeScript, Tailwind, Apollo Client

C’est un workflow professionnel, utilisé dans les vraies applications web modernes.