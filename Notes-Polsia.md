Le modèle de Next.js canonique pour les applications clients générées par Polsia.
Ce dépôt est un échafaudage avec la base de l’interface utilisateur shadcn intégrée. Il expédie le Le framework prend par défaut toutes les applications dès le premier jour : Next.js 16 App Router, React 19, Tailwind 4, câblage client Prisma, Biome, Vitest, en-têtes de sécurité, un système piloté par le jeton et un large décor primitif Shadcn. Des capacités produit telles que l’authentification, La facturation, l’email, l’analytique, les tableaux de bord et les flux de travail multi-locataires sont installés de .Polsia-Inc/modules
Qu’est-ce que c’est
Ceci est un modèle, pas une application de démarrage personnalisée à la main. L’ingénierie de la Polse L’agent lit la carte de propriété, installe les modules lorsque nécessaire, et ne modifie que le Zones délimitées appartenant à l’application. La forme de répertoire et sont le contrat qui conserve les fichiers du framework, les fichiers de modules et le code client séparés..polsia/ownership.json
L’id du modèle canonique est ; le dépôt GitHub est .polsia-next-v2Polsia-Inc/template-next
Ce qui est inclus
<ul><li>Next.js 16 App Router, React 19, TypeScript et Tailwind 4.</li><li>Base d’interface utilisateur shadcn : , , un ensemble primitif engagé dans , sonner toasts, next-themes, et theme tokens dans .components.jsoncn()src/components/ui/**src/app/globals.css</li><li>Configuration client Prisma 6 : , , et le singleton serveur uniquement dans . La base de données elle-même est externe ; La Polsia fournit des Postgres et injecte.prisma/schema/_base.prismaprisma.config.tssrc/lib/db.tsDATABASE_URL</li><li>Validation de l’environnement typée via .src/lib/env.ts</li><li>Exemples de plans de données : un contrat ZOD partagé, un gestionnaire de route, et une page client qui utilise ./api/exampleapiFetch</li><li>CSP et en-têtes de sécurité dans , , et .proxy.tsnext.config.tssrc/lib/csp.ts</li><li>Plomberie SEO : , , , , , une route d’image Open Graph par défaut, et une route (llmstxt.org) pour les robots IA/LLM sélectionnés via .src/lib/brand.tssrc/lib/site.tsrobots.tssitemap.tsmanifest.ts/llms.txtsrc/lib/llms-config.ts</li><li>Tests unitaires couvrant la carte de propriété, la posture CSP, la validation de l’environnement, et le Exemple de contrat de données.</li></ul>Ce qui n’est pas inclus
<ul><li>Pas d’authentification, de facturation, d’emails, d’analyses, de tableaux de bord ou d’autres modules produit.</li><li>Pas de serveur de base de données, Dockerfile, fichier compose ou Procfile.</li><li>Pas de vrais fichiers d’environnement. documente les variables attendues ; Déploiements recevoir des valeurs réelles de la plateforme..env.example</li><li>Aucune action serveur. Les pages produit appellent les gestionnaires de routes via ./api/*src/lib/api-client.ts</li></ul>Modèle de propriété
Lisez toujours , , et avant de monter..polsia/installed.json.polsia/ownership.json.polsia/overrides.json
PaliersExemplesQui édite
framework_owned
src/lib/db.ts, , , , , , src/lib/utils.tscomponents.jsonprisma.config.tsAGENTS.md.polsia/installed.json.polsia/ownership.json
Framework ou possession d’un module uniquement.
user_owned
src/components/ui/**, , , , , , , src/app/(setup)/page.tsxsrc/app/(custom)/**src/lib/brand.tssrc/lib/nav.tspublic/**README.md.polsia/overrides.json
L’agent de l’application ou le client.
shared
src/app/globals.css, , , , , , src/lib/env.tssrc/app/layout.tsxproxy.tsnext.config.tspackage.json.env.example
Édition uniquement via les emplacements déclarés ou la stratégie de fusion documentée.
.polsia/ownership.json est la source de la vérité. Les bannières sources sont lecteur signalisation uniquement.
Quoi ne pas modifier
<ul><li>Anything marked in . Comment-capable source files carry banners as signage, but the ownership map is the authority.framework_owned.polsia/ownership.json@polsia:framework-owned</li><li>Anything outside declared slot markers in shared files such as , , , , and .next.config.tsproxy.tssrc/lib/env.tssrc/app/layout.tsxsrc/app/globals.css</li><li>.polsia/installed.json and . They are generated state files. Use for hand-editable module policy..polsia/ownership.json.polsia/overrides.json</li></ul>Platform Rules
<ul><li>Keep Cache Components off unless the platform explicitly changes that policy.</li><li>Use ; do not add .proxy.tsmiddleware.ts</li><li>Keep data and mutations behind route handlers. Do not add Server Actions./api/*</li><li>Keep Prisma datasource and generator declarations in . App or module schema files add models only.prisma/schema/_base.prisma</li><li>src/app/(auth)/** and pages are user-owned — build and restyle them freely. Don't hand-roll the auth security surface (, , the prisma auth schema, /): those are framework-owned, installed by the auth module.src/app/(dashboard)/**src/lib/auth.tssrc/app/api/auth/**require-authrequire-admin</li><li>Put recurring work in ; do not use in-process schedulers for product behavior.polsia.toml[[crons]]</li></ul>Agent Workflow
<ol><li>Read and the three state files.AGENTS.md.polsia/</li><li>Decide whether the request is app-specific UI/business logic or a reusable capability that should come from a module.</li><li>Install modules through the Polsia module installer when a module owns the capability. Do not clone module files by hand.</li><li>Write app-specific code in user-owned areas:</li><li><ul><li>Routes: src/app/(custom)/<feature>/page.tsx</li><li>API handlers: src/app/api/<resource>/route.ts</li><li>Contracts: src/lib/contracts/<resource>.ts</li><li>Logique métier : src/lib/business/<feature>.ts</li><li>Composants personnalisés : src/components/custom/<feature>.tsx</li><li>Refrains : src/hooks/use-<feature>.ts</li></ul></li><li>Remplacez la maison de démarrage en modifiant sur place, ou Supprime le groupe de routes avant d’ajouter une autre page qui se résout en .src/app/(setup)/page.tsx(setup)/</li><li>Définir l’identité produit dans , mettre à jour pour des pages publiques accessibles, et s’appuient sur les robots intégrés, le plan du site, les métadonnées, et la plomberie Open Graph.src/lib/brand.tssrc/lib/nav.ts</li><li>Gardez chaque fonctionnalité accessible depuis la page d’accueil ou, pour authentifiée fonctionnalités, le tableau de bord.</li><li>Effectuez les vérifications nécessaires avant l’expédition.</li></ol>Les installations de modules passent par l’installateur de modules Polsia. L’installateur possède écritures de fichiers de modules, mises à jour de la carte de propriété, hachages d’installation et validateurs de modules. Ne clonez pas les fichiers de modules ni ne les copiez à la main.
Plan de données
Les pages produit sont des composants clients. Ils appellent les gestionnaires de routes via , passant un schéma zod partagé pour valider la réponse à l’exécution.apiFetch
Chaque ressource devrait avoir un contrat partagé dans . Le gestionnaire de route valide les formes de requête et de réponse avec ce contrat, et Le client importe le même schéma.src/lib/contracts/<resource>.ts
Les erreurs de validation des gestionnaires de route utilisent :
{ errors: { fieldName: 'Message' } }
Les formulaires clients correspondent à ces erreurs avec . Succès transitoire ou Le retour de panne inattendu doit utiliser depuis .applyServerErrorstoastsonner
UI
Le modèle inclut déjà un ensemble large de primitives shadcn sous . Composez d’abord ces primitives, restylez selon le thème jetons et variantes composantes, et ajouter de nouvelles primitives avec :src/components/ui/**
npx shadcn@latest add <name> --yes
L’interface utilisateur réutilisable spécifique à une application appartient à .src/components/custom/**
Guide d’annuaire
.<br>├── .polsia/                          Generated state and ownership map<br>├── prisma/<br>│   ├── schema/_base.prisma           Datasource + generator only<br>│   └── migrations/migration_lock.toml Project-level migration lock<br>├── public/                           Customer assets<br>├── src/<br>│   ├── app/<br>│   │   ├── (setup)/page.tsx          Starter home served at /<br>│   │   ├── (custom)/example/page.tsx Data-plane example page<br>│   │   ├── api/example/route.ts      Data-plane example route<br>│   │   ├── health/route.ts           Deploy healthcheck<br>│   │   ├── layout.tsx                Root layout and providers slot<br>│   │   └── globals.css               Tailwind theme and brand token slot<br>│   ├── components/<br>│   │   ├── ui/                       shadcn primitives<br>│   │   ├── custom/                   App-owned compositions<br>│   │   └── theme-provider.tsx        next-themes wrapper<br>│   ├── hooks/                        App-owned React hooks<br>│   ├── lib/<br>│   │   ├── api-client.ts             Client transport helper<br>│   │   ├── brand.ts                  Product name and description<br>│   │   ├── contracts/example.ts      Example shared zod contract<br>│   │   ├── csp.ts                    CSP builder<br>│   │   ├── db.ts                     Prisma singleton<br>│   │   ├── env.ts                    Typed env schema<br>│   │   ├── forms.ts                  Server error mapping<br>│   │   ├── nav.ts                    App navigation config<br>│   │   └── utils.ts                  cn()<br>│   └── modules/                      Vendored module installs<br>├── tests/unit/                       Vitest unit tests<br>├── next.config.ts                    Next config and security headers<br>├── proxy.ts                          CSP nonce and middleware chain slot<br>├── polsia.toml                       Deploy manifest and scheduled jobs<br>└── AGENTS.md                         Engineering agent operating manual<br><br>
En-têtes de sécurité
next.config.ts définit des en-têtes de réponse de base :
<ul><li>Strict-Transport-Security</li><li>X-Content-Type-Options</li><li>X-Frame-Options</li><li>Referrer-Policy</li><li>Permissions-Policy</li><li>Cross-Origin-Opener-Policy</li><li>Cross-Origin-Resource-Policy</li></ul>proxy.ts Définit une politique de sécurité de contenu par demande. reste strict avec un nonce et ; permet des styles en ligne donc Radix et Le positionnement en temps dur SHADCN fonctionne en production.script-srcstrict-dynamicstyle-src
Validateurs du jour 1
Le plancher de validation de l’échafaudage nu est déclaré en . Les validateurs spécifiques à chaque module sont ajoutés par Les modules se manifestent lors de l’installation des modules..polsia/installed.json#day_1_floor
<ul><li>no-secrets-in-client-bundle</li><li>server-only-import-on-secret-modules</li><li>agent-has-no-prod-db-credentials</li><li>db-ssl-required</li><li>parameterized-queries-only</li><li>security-headers-present</li><li>lockfile-committed-and-pinned</li><li>lifecycle-scripts-disabled</li><li>next-version-not-affected-by-cve-2025-29927</li></ul>Développement local
Utilisez npm ; Le fichier verrouillé est validé.
npm install<br>npm run typecheck<br>npm run lint<br>npm run test<br>SKIP_ENV_VALIDATION=1 npm run dev
npm run dev et valider et quand ne sont pas définis. Sur un clone local Sans base de données provisionnée, soit régler les variétés requises dans ou préfixez la commande par .npm run buildDATABASE_URLNEXT_PUBLIC_APP_URLSKIP_ENV_VALIDATION.env.localSKIP_ENV_VALIDATION=1
typecheck, , et ne nécessitent pas d’env. Sans modules installés, sert de placeholder jusqu’à ce qu’une page racine créée par un module ou une application prend le relais.linttest/(setup)
CI/CD
.github/workflows/ci.yml exécute à chaque poussée et PR à : , , (avec ), alors . Chaque porte fonctionne même si une précédente a échoué, donc une porte rouge La build montre tous les problèmes en même temps.mainnpm run lintnpm run testnpm run buildSKIP_ENV_VALIDATION=1npm run typecheck
La vérification de type s’exécute volontairement après la compilation : inclut , où Next génère des types de gestionnaire de route et de prop de page. Courant avant qu’une construction ne les saute silencieusement.tsconfig.json.next/types/**tsc
Les sorties sont en deux phases. release.yml (onglet Actions, manuel) prend un bump // , un exact , ou un aperçu. Ça re-exécute contre le commit en cours de publication, fait un bump sur une branche, la pousse, et imprime un lien pour ouvrir le PR. Vous ouvrir cette PR — une PR créée ne déclenche jamais ses propres vérifications, Donc ses vérifications obligatoires ne seraient jamais signalées. Le fusionner déclenche tag-release.yml, ce qui crée le tag et le GitHub Libérez.patchminormajorversiondry_runci.ymlpackage.jsonrelease/v<version>GITHUB_TOKENv<version>
Le bump passe par un PR plutôt qu’un push direct à cause d’un ensemble de règles de branche Exiger des vérifications de statut rejette un nouveau commit envoyé directement à , et GitHub refuse un acteur de contournement qui n’est pas enregistré sur l’organisation.mainIntegration
Rien n’est publié sur npm (ce paquet est ). Le bump de version C’est sur quoi converge la flotte : le backend tire ce modèle et le compare à la version du modèle épinglé de chaque code base, donc un bump se déclenche Rien à lui seul — chaque entreprise réestampe à la fin de son prochain succès Run d’ingénierie.private: truemainpackage.json
Versions
Des versions exactes épinglées sont utilisées pour la pile de cadre :
<ul><li>Next.js 16.2.6, routeur d’applications</li><li>Réaction 19.2.7</li><li>Tailwind CSS 4.3.0, CSS d’abord @theme</li><li>shadcn/ui style new-yorkais</li><li>Sonner 2.0.7</li><li>TypeScript 5.5.4, mode strict</li><li>Biome 2.3.1, peluches et format</li><li>Vitest 3.2.6</li><li>Prisma 6.19.3</li><li>Nœud >=20.18.1</li></ul>Sécurité dans la dépendance transitive patchée par broches les versions qui ne peuvent pas atteindre les broches de framework par elles-mêmes.overridespackage.json
<br> 
Fichiers à ne pas modifier sans raison
.polsia/ownership.json
.polsia/installed.json
prisma.config.ts
AGENTS.md
Zones modifiables
README.md
src/app/(custom)/**
src/lib/brand.ts
public/**
Architecture
Next.js
React
TypeScript
Prisma
Tailwind
Shadcn UI
Sécurité
CSP
Security Headers
Validation Zod
Validation d'environnement
À retenir
Le projet a été généré depuis le template : polsia-next-v2
