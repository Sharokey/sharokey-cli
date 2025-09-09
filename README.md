# Sharokey CLI - Outil de Partage Sécurisé de Secrets en Ligne de Commande

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Téléchargements](https://img.shields.io/github/downloads/Sharokey/sharokey-cli/total.svg)](https://github.com/Sharokey/sharokey-cli/releases)
[![Version](https://img.shields.io/github/v/release/Sharokey/sharokey-cli)](https://github.com/Sharokey/sharokey-cli/releases/latest)

👉 **Découvrez la plateforme complète** : Sharokey - Partage Sécurisé de Secrets

Sharokey CLI est un outil en ligne de commande permettant de créer, gérer et partager des secrets chiffrés avec une sécurité Zero Knowledge.
Idéal pour partager des mots de passe, clés API, identifiants de base de données et fichiers sensibles en toute sécurité, avec expiration automatique, nombre de vues limité et chiffrement de niveau entreprise.

## 🔐 Chiffrement Zero Knowledge

Sharokey CLI utilise le **chiffrement AES-GCM-256 côté client** avec dérivation de clé PBKDF2 (10 000 itérations). Vos secrets sont chiffrés sur votre appareil avant transmission - **le serveur ne peut pas déchiffrer vos données**.

### Fonctionnalités Clés :
- **Perfect Forward Secrecy** : Clés jamais stockées côté serveur
- **Chiffrement côté client** : Données chiffrées avant de quitter votre ordinateur
- **Algorithmes standards** : AES-GCM-256, PBKDF2, SHA-256

## 🚀 Démarrage Rapide

### Installation

Téléchargez la dernière version pour Windows :

```bash
# Télécharger et installer
curl -L https://github.com/Sharokey/sharokey-cli/releases/latest/download/sharokey.exe -o sharokey.exe

# Configurer avec votre token API
sharokey config --token votre_token_api_ici

# Tester la connexion
sharokey test
```

### Utilisation de Base

```bash
# Créer un secret avec mot de passe et expiration
sharokey create "Mot de passe BDD : admin123" --password "secure123" --hours 24 --views 1

# Partager des identifiants API avec plusieurs couches de sécurité
sharokey create "Clé API : abc123xyz" --otp-email "admin@entreprise.com" --ip-whitelist "203.0.113.5" --hours 48

# Envoyer des fichiers confidentiels en sécurité
sharokey create "Fichiers contrat" --attach contrat.pdf --attach conditions.pdf --password "legal2024" --hours 72
```

## 🛡️ Fonctionnalités de Sécurité

### Protection Multi-Niveaux
- **Vérification CAPTCHA** - Protection basique contre les bots
- **Protection par mot de passe** - Exigence de mot de passe personnalisé
- **OTP Email** - Mot de passe à usage unique par email
- **OTP SMS** - Mot de passe à usage unique par téléphone (sécurité maximale)
- **Liste IP autorisées** - Restreindre l'accès à des adresses IP publiques spécifiques
- **Géolocalisation** - Limiter l'accès par codes pays

### Système de Priorité de Sécurité
Quand plusieurs options de sécurité sont spécifiées, seul le niveau le plus élevé s'applique :
```
CAPTCHA < Mot de passe < OTP Email < OTP Téléphone (le plus élevé)
```

## 📁 Support des Pièces Jointes

Partagez des fichiers sensibles avec chiffrement zero-knowledge :

### Formats Supportés (40+)
- **Documents** : PDF, DOCX, XLSX, PPTX, TXT, RTF, ODT, ODS, ODP
- **Images** : JPG, PNG, GIF, BMP, WEBP, SVG
- **Audio** : MP3, WAV, FLAC, M4A, AAC, OGG
- **Vidéo** : MP4, AVI, MKV, MOV, WMV, WEBM
- **Archives** : ZIP, RAR, 7Z, TAR, GZ

### Limites
- **Fichiers maximum** : 10 par secret
- **Taille totale** : 10MB pour tous les fichiers
- **Chiffrement** : Tous les fichiers chiffrés côté client avant upload

## 🔧 Référence des Commandes

### Commandes Principales
| Commande | Description | Exemple |
|----------|-------------|---------|
| `create` | Créer un secret chiffré | `sharokey create "password" --hours 24` |
| `list` | Lister vos secrets | `sharokey list --status active --limit 10` |
| `get` | Obtenir les détails d'un secret | `sharokey get ABC123 --verbose` |
| `delete` | Supprimer un secret | `sharokey delete ABC123` |
| `stats` | Voir les statistiques | `sharokey stats` |
| `config` | Gérer la configuration | `sharokey config --token TOKEN` |

### Demandes de Secrets
| Commande | Description | Exemple |
|----------|-------------|---------|
| `create-request` | Demander des secrets à d'autres | `sharokey create-request --email-to vendeur@entreprise.com` |
| `list-requests` | Lister les demandes actives | `sharokey list-requests --status active` |
| `get-request` | Obtenir les détails d'une demande | `sharokey get-request 123` |
| `delete-request` | Annuler une demande | `sharokey delete-request 123` |

## 🎯 Cas d'Usage

### Équipes DevOps & IT
```bash
# Partager des identifiants de base de données en sécurité
sharokey create "BDD Prod : user=admin pass=secret123" --otp-email "devops@entreprise.com" --hours 8 --views 2

# Distribuer les clés d'accès serveur
sharokey create "Clé SSH Privée" --attach serveur.key --password "deploy2024" --ip-whitelist "203.0.113.50" --hours 24
```

### Business & Juridique
```bash
# Partager des documents confidentiels
sharokey create "Documents NDA" --attach nda.pdf --attach contrat.pdf --otp-phone "+33123456789" --hours 48

# Identifiants clients sécurisés
sharokey create "Accès Portail Client" --geolocation "FR,BE" --password "client123" --hours 168 --views 5
```

### Usage Personnel
```bash
# Partager temporairement des mots de passe WiFi
sharokey create "WiFi Invités : MonReseau / PassTemp123" --captcha --hours 24 --views 10

# Envoyer des photos sensibles en sécurité
sharokey create "Photos Famille" --attach photo1.jpg --attach photo2.jpg --password "famille2024" --hours 72
```

## 📊 Fonctionnalités Entreprise

### Gestion des Quotas
- Suivre l'utilisation des secrets dans votre organisation
- Surveiller l'activité des équipes et la conformité
- Définir des politiques d'expiration et limites de vues

### Journalisation d'Audit
- Logs complets de toutes les opérations sur les secrets
- Suivi des modèles d'accès et événements de sécurité
- Export des logs pour rapports de conformité

### Collaboration d'Équipe
- Demander des secrets aux membres de l'équipe
- Partager des identifiants avec accès basé sur les rôles
- Gestion centralisée des secrets

## ⚙️ Configuration

### Emplacement du Fichier de Paramètres
- **Windows** : `%APPDATA%\Sharokey\config.json`
- **Linux/Mac** : `~/.config/sharokey/config.json`

### Options Disponibles
```bash
# Configuration API
sharokey config --token VOTRE_TOKEN_API --timeout 60

# Journalisation
sharokey config --logs-enabled --log-level Debug

# Voir les paramètres actuels
sharokey config --show
```

## 🔍 Dépannage

### Problèmes Courants

**Erreurs d'Authentification**
```bash
# Vérifier votre token
sharokey config --show
```

**Timeouts Réseau**
```bash
# Augmenter le timeout
sharokey config --timeout 120
```

**Secret Non Trouvé**
```bash
# Vérifier le statut et l'expiration du secret
sharokey get SLUG_SECRET --verbose
```

**Erreurs d'Upload de Fichiers**
- Vérifier que les formats de fichiers sont supportés (40+ formats disponibles)
- Vérifier la limite de taille totale (10MB maximum)
- S'assurer que les fichiers sont accessibles et non corrompus

### Mode Debug
```bash
# Activer la journalisation détaillée
sharokey config --log-level Debug --logs-enabled

# Tester la connectivité avec sortie verbeuse
sharokey test --verbose
```

## 📚 Documentation

- **Documentation Complète** : [Guide CLI Complet](https://docs.sharokey.com/fr/libraries/cli/)
- **Référence API** : [Documentation API](https://docs.sharokey.com/fr/api/)
- **Livre Blanc Sécurité** : [Architecture Zero Knowledge](https://docs.sharokey.com/fr/security/)

## 🤝 Support

- **Issues GitHub** : [Signaler bugs et demandes de fonctionnalités](https://github.com/Sharokey/sharokey-cli/issues)
- **Documentation** : [https://docs.sharokey.com/fr](https://docs.sharokey.com/fr)
- **Support Email** : support@sharokey.com

## 📄 Licence

Ce projet est sous licence MIT - voir le fichier [LICENSE](LICENSE) pour les détails.

## 🔗 Projets Connexes

- **Application Web Sharokey** : [https://sharokey.com](https://sharokey.com)
- **Extension Navigateur** : [Extension Sharokey](https://github.com/Sharokey/browser-extension)
- **SDK API** : [SDK JavaScript](https://github.com/Sharokey/js-sdk)

---

**Mots-clés** : partage sécurisé secrets, gestionnaire mot passe cli, partage fichier chiffré, chiffrement zero knowledge, outil sécurité ligne commande, gestion secrets devops, chiffrement AES cli, partage identifiants sécurisé, gestion mot passe entreprise, partage pièce jointe chiffrée, sécurité informatique France, RGPD conformité, cybersécurité entreprise
