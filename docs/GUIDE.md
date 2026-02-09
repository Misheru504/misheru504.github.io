# 🛠️ Guide : Recréer ce portfolio from scratch

Ce guide t'explique comment reconstruire ce portfolio terminal étape par étape, pour que tu comprennes chaque partie et puisses le personnaliser à fond.

---

## 📁 Structure du projet

```
portfolio/
├── index.html                  # Page d'accueil
├── pages/
│   ├── projets.html            # Liste des projets
│   ├── a-propos.html           # Page à propos
│   └── projets/
│       ├── flora-engine.html   # Page projet détaillée
│       ├── click-oclock.html   # Page projet détaillée
│       └── _template.html      # Template pour nouveaux projets
├── assets/
│   ├── css/
│   │   └── style.css           # Tous les styles
│   └── img/
│       └── projets/
│           ├── flora-engine/   # Images du projet
│           └── click-oclock/   # Images du projet
└── docs/
    └── GUIDE.md                # Ce fichier
```

---

## 🧱 Étape 1 : Le squelette HTML de base

Chaque page suit cette structure :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Titre | Michel-Ange</title>
    
    <!-- Bootstrap (framework CSS) -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
    
    <!-- Police JetBrains Mono (style terminal) -->
    <link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    
    <!-- Icônes Bootstrap -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.1/font/bootstrap-icons.css">
    
    <!-- Notre CSS personnalisé -->
    <link rel="stylesheet" href="./assets/css/style.css">
</head>
<body>
    <!-- Effet scanlines (lignes de scan CRT) -->
    <div class="scanlines"></div>
    
    <!-- Navigation -->
    <nav class="terminal-nav">...</nav>
    
    <!-- Contenu principal -->
    <main class="container-fluid px-3 px-md-5">
        ...
    </main>
    
    <!-- Pied de page -->
    <footer class="terminal-footer">...</footer>
</body>
</html>
```

### Pourquoi ces éléments ?

| Élément | Rôle |
|---------|------|
| `<meta charset="UTF-8">` | Permet les accents français |
| `<meta name="viewport">` | Rend le site responsive (mobile) |
| Bootstrap | Framework CSS qui fournit une grille et des utilitaires |
| JetBrains Mono | Police monospace qui donne le look "code" |
| Bootstrap Icons | Icônes gratuites (GitHub, email, flèches...) |

---

## 🎨 Étape 2 : Comprendre le CSS

### Les variables CSS (couleurs)

En haut de `style.css`, on définit toutes les couleurs :

```css
:root {
    /* Fonds */
    --bg-dark: #0a0a0f;           /* Fond principal (presque noir) */
    --bg-terminal: #12121a;        /* Fond des fenêtres terminal */
    --bg-card: #16161f;            /* Fond des cartes */
    
    /* Accents */
    --purple-primary: #a855f7;     /* Violet principal (ton 💜) */
    --green-terminal: #4ade80;     /* Vert style terminal */
    --cyan-accent: #22d3ee;        /* Cyan pour les commandes */
    
    /* Texte */
    --text-primary: #e4e4e7;       /* Texte principal (blanc cassé) */
    --text-secondary: #a1a1aa;     /* Texte secondaire (gris) */
    --text-dim: #71717a;           /* Texte discret */
}
```

**Pourquoi des variables ?** → Change une couleur à un endroit, elle change partout.

### Les composants principaux

#### 1. La fenêtre terminal

```html
<div class="terminal-window">
    <div class="terminal-header">
        <!-- Boutons rouge/jaune/vert -->
        <div class="terminal-buttons">
            <span class="btn-close-fake"></span>
            <span class="btn-minimize"></span>
            <span class="btn-maximize"></span>
        </div>
        <span class="terminal-title">nom-du-fichier.md</span>
    </div>
    <div class="terminal-body">
        <!-- Contenu ici -->
    </div>
</div>
```

#### 2. Une ligne de commande

```html
<div class="terminal-line">
    <span class="prompt">$</span>
    <span class="command">la commande</span>
</div>
```

- `.prompt` → Le `$` vert
- `.command` → La commande en cyan

#### 3. Un commentaire

```html
<span class="comment"># Ceci est un commentaire</span>
```

---

## 🧩 Étape 3 : La navigation

```html
<nav class="terminal-nav">
    <div class="nav-content">
        <span class="nav-prompt">~/michel-ange $</span>
        <a href="index.html" class="nav-link">accueil</a>
        <a href="pages/projets.html" class="nav-link active">projets</a>
        <a href="pages/a-propos.html" class="nav-link">à-propos</a>
        <span class="cursor-blink">█</span>
    </div>
</nav>
```

- `.nav-prompt` → Le chemin style terminal
- `.nav-link` → Les liens
- `.active` → Le lien de la page actuelle (surligné)
- `.cursor-blink` → Le curseur qui clignote

### ⚠️ Attention aux chemins relatifs !

Selon où tu es dans l'arborescence, les liens changent :

| Depuis | Vers index.html | Vers projets.html |
|--------|-----------------|-------------------|
| `index.html` | `index.html` | `pages/projets.html` |
| `pages/projets.html` | `../index.html` | `projets.html` |
| `pages/projets/flora.html` | `../../index.html` | `../projets.html` |

---

## 📦 Étape 4 : La grille Bootstrap

Bootstrap utilise un système de 12 colonnes :

```html
<div class="row">
    <div class="col-lg-6">Moitié gauche (sur grand écran)</div>
    <div class="col-lg-6">Moitié droite</div>
</div>
```

- `col-lg-6` → 6 colonnes sur 12 = 50% de largeur (sur écrans larges)
- `col-lg-4` → 4 colonnes = 33%
- `col-12` → Pleine largeur

Le `lg` signifie "large screens". Sur mobile, tout passe en pleine largeur automatiquement.

---

## 🖼️ Étape 5 : Ajouter des images

### Placeholder (avant d'avoir l'image)

```html
<div class="screenshot-placeholder">
    <i class="bi bi-image"></i>
    <span>Description</span>
</div>
```

### Vraie image

```html
<img src="../../assets/img/projets/flora-engine/screenshot1.png" 
     alt="Description de l'image"
     class="screenshot-img">
```

---

## 📝 Étape 6 : Les sections d'un projet

Une page projet se compose de sections. Chaque section suit ce pattern :

```html
<section class="study-section">
    <!-- Ligne de commande (titre visuel) -->
    <div class="terminal-line">
        <span class="prompt">$</span>
        <span class="command">cat section.md</span>
    </div>
    
    <!-- Contenu -->
    <div class="study-content">
        <h2>Titre de la section</h2>
        <p>Contenu...</p>
    </div>
</section>
```

### Sections recommandées

| Section | Commande | Usage |
|---------|----------|-------|
| Contexte | `cat contexte.md` | Pourquoi ce projet existe |
| Processus | `git log ./processus` | Les étapes de création |
| Screenshots | `ls ./screenshots/` | Visuels |
| Défis | `grep "CHALLENGE" ./` | Problèmes & solutions |
| Stack | `cat requirements.txt` | Technologies |
| Apprentissages | `echo $LESSONS_LEARNED` | Ce que t'as appris |
| Dev logs | `tail -f ./devlog.md` | Journal de développement |

---

## 🎯 Étape 7 : Créer une nouvelle page projet

1. **Copie** `pages/projets/_template.html`
2. **Renomme** en `mon-projet.html`
3. **Modifie** les chemins CSS :
   ```html
   <link rel="stylesheet" href="../../assets/css/style.css">
   ```
4. **Modifie** les liens de navigation :
   ```html
   <a href="../../index.html" class="nav-link">accueil</a>
   ```
5. **Remplis** le contenu

---

## 🔧 Personnalisations courantes

### Changer la couleur principale

Dans `style.css`, modifie :
```css
--purple-primary: #a855f7;  /* Remplace par ta couleur */
```

### Changer la police

Remplace JetBrains Mono par une autre police Google Fonts :
```html
<link href="https://fonts.googleapis.com/css2?family=Fira+Code&display=swap" rel="stylesheet">
```
```css
--font-mono: 'Fira Code', monospace;
```

### Désactiver les scanlines

Supprime ou commente dans le HTML :
```html
<!-- <div class="scanlines"></div> -->
```

---

## 🌐 Hébergement

### GitHub Pages (gratuit, statique)
- ✅ HTML, CSS, JS
- ❌ PHP, bases de données

### Pour du PHP
- Hostinger (~3€/mois)
- OVH (~5€/mois)
- PlanetHoster
- Infomaniak

---

## 📚 Ressources pour apprendre

- [MDN Web Docs](https://developer.mozilla.org/fr/) — La bible du HTML/CSS
- [Bootstrap Docs](https://getbootstrap.com/docs/) — Documentation Bootstrap
- [CSS-Tricks](https://css-tricks.com/) — Astuces CSS
- [Google Fonts](https://fonts.google.com/) — Polices gratuites

---

## 🐛 Problèmes courants

### Les styles ne s'appliquent pas
→ Vérifie le chemin vers `style.css` (relatif à ta page)

### Les images ne s'affichent pas
→ Vérifie le chemin et l'extension (`.png` vs `.jpg`)

### Le site est cassé sur mobile
→ Assure-toi d'avoir `<meta name="viewport" ...>` dans le `<head>`

### Les liens ne marchent pas
→ Vérifie les chemins relatifs (`../` pour remonter d'un dossier)

---

*Tu peux maintenant reconstruire ce site de zéro et le personnaliser comme tu veux ! 🚀*
