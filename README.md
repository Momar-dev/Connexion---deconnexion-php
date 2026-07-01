# 🔐 Connexion/Déconnexion PHP

Système d'authentification complet en PHP avec gestion des sessions et sécurité.

---

## 📝 Description

**Connexion/Déconnexion PHP** est un projet éducatif implémentant un système d'authentification robuste en PHP. Il démontre les meilleures pratiques pour:
- Sécuriser les formulaires (CSRF, validation)
- Hacher les mots de passe
- Gérer les sessions utilisateur
- Implémenter la déconnexion

---

## ✨ Fonctionnalités

- ✅ Formulaire de connexion sécurisé
- ✅ Création de compte utilisateur
- ✅ Hachage des mots de passe (password_hash)
- ✅ Gestion des sessions PHP
- ✅ Déconnexion avec destruction de session
- ✅ Validation des données entrantes
- ✅ Messages d'erreur/succès
- ✅ Protection CSRF

---

## 🛠️ Technologies

- **PHP** - Langage serveur
- **MySQL/MariaDB** - Base de données
- **HTML5** - Markup
- **CSS3** - Styling

---

## 📁 Structure du Projet

```
Connexion---deconnexion-php/
├── index.php
├── login.php
├── register.php
├── logout.php
├── process_login.php
├── process_register.php
├── config.php
├── css/
└── README.md
```

---

## 🚀 Installation & Configuration

### Prérequis
- PHP 7.4+
- MySQL/MariaDB
- Serveur Apache ou Nginx

### Étapes d'Installation

1. **Cloner le repository**
```bash
git clone https://github.com/Momar-dev/Connexion---deconnexion-php.git
cd Connexion---deconnexion-php
```

2. **Configurer la base de données**
```bash
# Créer la base de données
mysql -u root -p < database.sql

# Ou créer manuellement:
CREATE DATABASE auth_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(255) UNIQUE NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

3. **Configurer config.php**
```php
<?php
define('DB_HOST', 'localhost');
define('DB_USER', 'root');
define('DB_PASS', 'your_password');
define('DB_NAME', 'auth_db');
?>
```

4. **Lancer le serveur**
```bash
php -S localhost:8000
```

5. **Accéder à l'application**
```
http://localhost:8000
```

---

## 📖 Flux d'Authentification

### Inscription
```
Registration Form → Validation → Hash Password → Save DB → Login
```

### Connexion
```
Login Form → Validate Credentials → Verify Password → Create Session → Redirect
```

### Déconnexion
```
Logout Button → Destroy Session → Clear Cookies → Redirect to Login
```

---

## 🔒 Sécurité Implémentée

✅ **Hachage des Mots de Passe**
```php
$password_hash = password_hash($password, PASSWORD_DEFAULT);
if (password_verify($password, $hash)) { /* OK */ }
```

✅ **Validation des Entrées**
```php
if (empty($username) || empty($email) || empty($password)) {
    $errors[] = "Tous les champs sont requis";
}
```

✅ **Tokens CSRF** (optionnel)
```php
$_SESSION['csrf_token'] = bin2hex(random_bytes(32));
```

✅ **Préparation des Requêtes SQL**
```php
$stmt = $pdo->prepare("SELECT * FROM users WHERE email = ?");
$stmt->execute([$email]);
```

✅ **Sessions Sécurisées**
```php
session_start();
if (!isset($_SESSION['user_id'])) {
    header('Location: login.php');
    exit();
}
```

---

## 📋 Endpoints/Pages

| Route | Description |
|-------|-------------|
| `/` | Page d'accueil |
| `/login.php` | Formulaire de connexion |
| `/register.php` | Formulaire d'inscription |
| `/process_login.php` | Traitement connexion (POST) |
| `/process_register.php` | Traitement inscription (POST) |
| `/logout.php` | Déconnexion |
| `/dashboard.php` | Tableau de bord (protégé) |

---

## 💡 Exemple d'Utilisation

### Inscription
```html
<form action="process_register.php" method="POST">
    <input type="text" name="username" required>
    <input type="email" name="email" required>
    <input type="password" name="password" required>
    <button type="submit">S'inscrire</button>
</form>
```

### Vérification Session
```php
<?php
session_start();
if (!isset($_SESSION['user_id'])) {
    header('Location: login.php');
    exit();
}

echo "Bienvenue, " . htmlspecialchars($_SESSION['username']);
?>
```

---

## 🐛 Dépannage

### "Erreur de connexion à la base de données"
- Vérifiez les identifiants MySQL dans config.php
- Assurez-vous que le serveur MySQL est actif

### "Session non persistante"
- Vérifiez que session_start() est appelé
- Vérifiez les paramètres cookies du navigateur

### "Mot de passe rejeté"
- Assurez-vous que password_verify() est utilisé
- Vérifiez la version de PHP (7.4+)

---

## 📚 Concepts Couverts

✅ Sessions PHP  
✅ Hachage de mots de passe  
✅ Validation de formulaires  
✅ Requêtes préparées  
✅ Gestion d'erreurs  
✅ Sécurité web (OWASP)  
✅ Authentification côté serveur  

---

## 👨‍💻 Auteur

**Momar Diop** - Développeur PHP

- GitHub: [@Momar-dev](https://github.com/Momar-dev)

---

## 📄 Licence

Projet éducatif - Libre d'utilisation et de modification

---

## 🤝 Contributions

Les améliorations de sécurité sont bienvenues!