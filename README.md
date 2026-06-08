# REX — Building a RAG with LLMs

Retour d'expérience perso : en construisant un **RAG** (une base de connaissance interrogeable) pour une communauté de modding de jeu vidéo, j'ai fini par répondre à une question que je ne m'étais pas posée au départ — **quand faut-il *vraiment* faire de l'agentique ?**

**▶ Voir le talk (Pecha Kucha, ~6 min) : https://mcreaper.github.io/building-a-rag-with-llms/**

*Présenté lors du meetup [« L'IA agentique en vrai »](https://www.meetup.com/saas-connected-systems-leaders-grenoble/events/314772564/) — SAAS & Connected Systems Leaders, Grenoble ([annonce LinkedIn](https://www.linkedin.com/posts/jean-dupuis-488a053_saas-grenoble-agenticai-share-7464990134212550656-AT4q/)).*

## La thèse

Je voulais un **agent** (un assistant pour les moddeurs). Mais mettre un gros modèle hébergé partout dans le processus de création coûtait trop cher → **pipeline par défaut**, local et déterministe. Ça a tenu partout sauf à **un endroit** : la synthèse du wiki, où mon pipeline triait les sources et **jetait ~95 % de la donnée avant même que le modèle la lise** (pages d'apparence complète, faits omis en silence). Là, l'agent était **obligatoire** — rendre la main au modèle pour qu'il pilote sa recherche.

On ne *décide* pas de faire un agent pour la distillation de la donnée du wiki,: le pipeline par défaut échoue quelque part, et c'est cet échec qui en réclame un — autant d'agents que d'endroits où le pipeline ne suffit pas, pas un de plus. Et même là, on ne le croit pas sur parole, il peut rater certaines informations.

## Le terrain

Rendre interrogeable le savoir d'une communauté de modding (Black Ops 3), éparpillé dans des forums morts, un Discord privé, des wikis à l'abandon; ~19 sources, ~66K entrées, recherche hybride BM25 + vecteurs.

Le moment qui résume tout : l'agent écrit une page sur le thème des « destructibles », propre et sourcée, mais ne décrit qu'un des deux systèmes du jeu — l'autre, je le connaissais, lui non. Je l'ai challengé sans pouvoir prouver qu'il avait tort, et ce doute a fait remonter une source canonique que la base n'utilisait pas, qui a fiabilisé tout le reste. *La qualité s'améliore quand un humain refuse de croire l'agent sur parole, même sans hallucinations de sa part.*

## Le deck

[`index.html`](index.html) — fichier HTML **autonome** (polices embarquées, zéro
dépendance, fonctionne hors-ligne) : 18 diapos × 20 s, défilement auto, notes
orateur (`S`), plein écran (`F`), mode 6:00 (`M`). Les coulisses dans
