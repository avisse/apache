#  Mini-projet Apache — Steve Avisse

> Ce projet a été réalisé dans le cadre de ma préparation à un entretien technique pour un poste de **Chef du service Applications et Bases de données** à la Communauté d’Agglomération Béziers Méditerranée.

Il s’agit d’un **mini-laboratoire personnel** hébergé dans une **machine virtuelle Debian 12**, où j’ai installé, configuré et personnalisé un serveur web Apache. L’objectif : **comprendre réellement ce qu’est un serveur web**, et **être capable d’en parler concrètement** en entretien.

---

##  Objectifs du projet

- ✅ Installer et démarrer Apache2 sur Debian
- ✅ Servir une page web personnalisée (HTML + CSS)
- ✅ Comprendre la structure des fichiers Apache
- ✅ Créer un VirtualHost local (`monprojet.local`)
- ✅ Configurer `/etc/hosts` dans la VM pour simuler un nom de domaine
- ✅ Pousser le projet sur un dépôt GitHub

---

## Environnement utilisé

- **Système d’exploitation** : Debian 12 (VM VirtualBox)
- **Web server** : Apache2 (`apache2` package via APT)
- **Langages** : HTML, CSS
- **Éditeur** : Nano (terminal)
- **Dépôt GitHub** : https://github.com/avisse/apache.git

---

## Étapes réalisées

### 1. Installation d’Apache
```bash
sudo apt update
sudo apt install apache2 -y
sudo systemctl start apache2

2. Création de la page personnalisée
------ Fichier : /var/www/html/index.html
------ Contenu : page HTML stylisée avec CSS intégré (voir plus bas)

3. Test de la page web
Dans Firefox (dans la VM), accès à :

arduino
Copier
Modifier
http://localhost
4. Création d’un VirtualHost
------- Dossier : /var/www/monprojet
-------- Fichier de conf : /etc/apache2/sites-available/monprojet.conf

Contenu du VirtualHost :

apache
Copier
Modifier
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/monprojet
    ServerName monprojet.local
    ErrorLog ${APACHE_LOG_DIR}/monprojet-error.log
    CustomLog ${APACHE_LOG_DIR}/monprojet-access.log combined
</VirtualHost>
Activation :

bash
Copier
Modifier
sudo a2ensite monprojet.conf
sudo systemctl reload apache2
Ajout dans /etc/hosts :

bash
Copier
Modifier
127.0.0.1   monprojet.local
Test :

arduino
Copier
Modifier
http://monprojet.local

 ---- Résultat : affichage de la page custom via un nom de domaine local.

------- Page HTML utilisée (rendu amélioré)
------index.html :

html
Copier
Modifier
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Bienvenue sur mon serveur Apache</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f4f4f4;
      text-align: center;
      padding: 50px;
    }
    .container {
      background: white;
      padding: 30px;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
      display: inline-block;
    }
    h1 {
      color: #d30000;
    }
    p {
      font-size: 18px;
      color: #333;
    }
    footer {
      margin-top: 30px;
      font-size: 14px;
      color: #777;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>🚀 Mini-projet Apache – Steve Avisse</h1>
    <p>Bienvenue sur mon serveur Apache local sous Debian 12.</p>
    <p>Ce site est hébergé et servi par Apache2, configuré manuellement dans ma VM.</p>
    <footer>
      &copy; 2025 - Projet de préparation entretien Béziers Méditerranée
    </footer>
  </div>
</body>
</html>

 ---- Versionning & GitHub
Commandes Git utilisées :
bash
Copier
Modifier
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/avisse/apache.git
git push -u origin main
