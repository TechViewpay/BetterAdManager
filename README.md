# Documentation d'intégration - BetterAdManager

## Présentation

**BetterAdManager** est le script unifié qui gère automatiquement l'intégration dans votre site des offres Adblock Choice et CTV Press.
Il est tout à fait possible de n'activer qu'une partie des offres disponibles.

### Fonctionnement

```
┌─────────────────────────────────────────────────────────────────┐
│                   VISITEUR SUR VOTRE SITE                       │
├─────────────────────────────────────────────────────────────────┤
│                            │                                    │
│                  Détection automatique                          │
│                            │                                    │
│          ┌─── Si actif ────┴─── Si actif ────┐                  │
│          │                                   │                  │
│          ▼                                   ▼                  │
│  ┌───────────────┐                 ┌───────────────┐            │
│  │ ADBLOCK ACTIF │                 │ PAS D'ADBLOCK │            │
│  │               │                 │               │            │
│  │ → Adblock Wall│                 │ → BetterBanner│            │
│  └───────────────┘                 └───────────────┘            │
└─────────────────────────────────────────────────────────────────┘
```

---

## Intégration rapide

### Méthode 1 : Balise script (recommandée)

Ajoutez cette ligne dans le `<head>` de vos pages :

```html
<script defer src="https://static.bettergroup.fr/scripts/betterAdManager.js?site_id=VOTRE_SITE_ID"></script>
```

> **Note** : Remplacez `VOTRE_SITE_ID` par l'identifiant fourni.

L'attribut `defer` est recommandé pour ne pas bloquer le chargement de votre page.

### Méthode 2 : Initialisation JavaScript

Pour plus de contrôle, vous pouvez initialiser manuellement :

```html
<script src="https://static.bettergroup.fr/scripts/betterAdManager.js"></script>
<script>
  BetterAdManager.init({
    site_id: 'VOTRE_SITE_ID'
  });
</script>
```

---

## API JavaScript

### Méthodes disponibles

| M&eacute;thode | Description | Retour |
|---------|-------------|--------|
| `BetterAdManager.init(options)` | Initialise le manager | - |
| `BetterAdManager.getLoadedProduct()` | Produit actuellement chargé | `'adblockWall'`, `'betterBanner'` ou `null` |
| `BetterAdManager.getConfig()` | Configuration éditeur | `Object` |
| `BetterAdManager.isAdblockDetected()` | Adblock détecté ? | `true` / `false` |
| `BetterAdManager.setDebug(enabled)` | Active le mode debug | - |

### Exemple d'utilisation

```javascript
// Vérifier si un adblock est détecté;
if (BetterAdManager.isAdblockDetected()) {
  console.log('Utilisateur avec adblock');
}
```

---

## Mode debug

Pour déboguer l'intégration, activez le mode debug ou forcer l'affichage du bandeau (sous réserve de pub disponible) :

### Option 1 : Via l'URL
Ajoutez `?debug` ou `?betterads` à l'URL de votre page :
```
https://votresite.com/article?debug
```

### Option 2 : Via JavaScript
```javascript
BetterAdManager.setDebug(true);
```

Les logs apparaîtront dans la console du navigateur avec le préfixe `[BetterAdManager]`.

---

## Configuration 

### Conditions d'affichage du CTV Press

Vous pouvez choisir à partir de combien de pages va se déclencher le CTV Press. Contactez votre account manager pour personnaliser la configuration.

### Rollout progressif - ciblage des devices

Vous pouvez choisir  : 
- activation par device (desktop / mobile)
- % d'utilisateurs touchés (rollout séparé entre desktop et mobile)
- niveau de déclenchement dans la page (hauteur du scroll pour afficher le bandeau)


### Exclusion de pages

Certaines pages peuvent être exclues de l'affichage des produits publicitaires (home, page de don, etc.). Contactez votre account manager pour personnaliser les exclusions. 
Vous pouvez aussi choisir d'exclure certaines IP.

---

## Prérequis techniques

- **HTTPS** : Le script doit être chargé sur des pages en HTTPS
- **Cookies** : Les cookies tiers doivent être autorisés pour le module Adblock Choice
- **JavaScript** : Doit être activé

---

## Support

Pour toute question ou problème d'intégration :
- Email : support@bettergroup.fr

---

## Changelog

| Version | Date | Modifications |
|---------|------|---------------|
| 1.0.0 | - | Version initiale |
