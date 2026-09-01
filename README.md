# portfolio
# Portfolio Charles Brioix — www.cbrioix.me

Homepage statique : `index.html` + assets. Aucun build, aucune dépendance, rien à compiler.
Tout est déjà configuré pour le domaine **www.cbrioix.me**.

```
site/
  index.html      la homepage (CSS et JS inline)
  merci.html      page de confirmation après envoi du formulaire
  assets/         photos WebP, hero, image de partage (og.jpg)
  logos/          6 logos clients en SVG
  favicon.svg  robots.txt  sitemap.xml
```

---

## La façon la plus simple et gratuite : Netlify Drop

Pas de compte GitHub, pas de terminal, pas de ligne de commande. Tu glisses un dossier, c'est en ligne.
Netlify est aussi le seul hébergeur gratuit qui **collecte les messages du formulaire** sans code
(100 soumissions/mois, anti-spam inclus) — c'est pour ça que je le recommande plutôt que Vercel ici.

### 1. Mettre le site en ligne (2 minutes)

1. Va sur **app.netlify.com/drop**
2. Glisse le dossier **`site`** entier dans la zone de dépôt.
3. C'est en ligne, sur une adresse du type `https://vaillant-tesla-8f3a1c.netlify.app`.
4. Crée un compte gratuit quand il te le propose : sans compte, le site expire au bout de 24 h.
5. **Site configuration → Change site name** → mets `cbrioix` pour obtenir `cbrioix.netlify.app`.

Pour publier une mise à jour plus tard : **Deploys → Drag and drop your site folder here**, tu reglisses
le dossier, la nouvelle version remplace l'ancienne. L'ancienne reste accessible et restaurable en un clic.

### 2. Brancher www.cbrioix.me

Dans Netlify : **Domain management → Add a domain** → saisis `cbrioix.me`.
Netlify propose deux voies — prends la première, elle est plus simple et plus fiable.

#### Voie A (recommandée) : déléguer le DNS à Netlify

Netlify t'affiche 4 serveurs de noms, du type :

```
dns1.p03.nsone.net
dns2.p03.nsone.net
dns3.p03.nsone.net
dns4.p03.nsone.net
```

Dans **Namecheap → Domain List → Manage** (sur cbrioix.me) → section **Nameservers** :
passe de « Namecheap BasicDNS » à **Custom DNS**, et colle les 4 adresses affichées par Netlify.
Sauvegarde. Netlify gère alors le domaine nu, le www, la redirection et le certificat HTTPS tout seul.

⚠️ Copie les serveurs affichés dans **ton** écran Netlify : le numéro (p03, p05…) change selon le compte.

#### Voie B : garder le DNS chez Namecheap

**Namecheap → Manage → Advanced DNS** (Nameservers doivent rester sur *Namecheap BasicDNS*) :

| Type | Host | Value | TTL |
|---|---|---|---|
| ALIAS (ou A) | `@` | `apex-loadbalancer.netlify.com` (A : `75.2.60.5`) | Automatic |
| CNAME | `www` | `cbrioix.netlify.app.` | Automatic |

Puis **supprime les deux enregistrements que Namecheap crée par défaut** : le `CNAME www → parkingpage.namecheap.com`
et la **URL Redirect Record** sur `@`. Tant qu'ils sont là, la vérification échoue.

### 3. HTTPS

Dans **Domain management → HTTPS**, clique **Verify DNS configuration**, puis **Provision certificate**.
Gratuit (Let's Encrypt), renouvelé automatiquement. Compte 10 minutes à 1 heure après le changement DNS.

Enfin, dans **Domain management**, définis `www.cbrioix.me` comme **primary domain** : Netlify redirige
alors `cbrioix.me` vers `www`. C'est cohérent avec le `<link rel="canonical">` de la page — une seule
version indexée, sinon Google voit du contenu dupliqué.

### 4. Le formulaire

Déjà branché sur **Netlify Forms** : rien à configurer. Après le premier déploiement, les messages
arrivent dans **Forms → contact** dans le tableau de bord.

Une seule chose à faire : **Forms → Form notifications → Add notification → Email notification**,
et mets ton adresse — sinon les messages s'empilent dans le dashboard sans que tu sois prévenu.

Le champ piège anti-bots est déjà en place, et l'envoi renvoie vers `merci.html`.

---

## Erreurs fréquentes

| Symptôme | Cause | Solution |
|---|---|---|
| Le site a disparu au bout de 24 h | déploiement Drop sans compte | recrée-le après avoir créé le compte gratuit |
| « DNS verification failed » | anciens enregistrements Namecheap | supprime le CNAME parkingpage et l'URL Redirect Record |
| Le domaine ne répond pas après 1 h | Nameservers pas passés en Custom DNS | Namecheap → Nameservers → Custom DNS → les 4 adresses Netlify |
| HTTPS en erreur | DNS pas encore propagé | attends, puis Verify DNS configuration → Provision certificate |
| Aucun message reçu | notification email non activée | Forms → Form notifications → Email notification |
| Images absentes en ligne, OK en local | casse du nom de fichier | les serveurs sont sensibles aux majuscules, pas ton Mac |

## À vérifier une fois en ligne

- **PageSpeed Insights** sur `https://www.cbrioix.me` — viser plus de 90 sur mobile.
- Affichage à 390 px, 768 px et 1440 px.
- Un envoi de test du formulaire, qui doit arriver dans ta boîte.
- Les 3 liens sortants : agenda Notion, CV Drive, LinkedIn.
- Le **CV sur Drive** doit être partagé en « Tous les utilisateurs disposant du lien », sinon les
  visiteurs tombent sur une demande d'accès.
- L'aperçu de partage LinkedIn (`assets/og.jpg`) via le Post Inspector de LinkedIn.

## Reste à faire

- Page **mentions légales** (obligatoire pour un site professionnel en France) : le lien de pied de page
  pointe vers `/mentions-legales.html`, qui n'existe pas encore.
- Les 4 **études de cas** `/projets/…` — les cartes affichent « bientôt en ligne » en attendant.