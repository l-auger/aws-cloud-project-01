# 🔐 SSH Access Test — Cloud-Projet-01

## 🟢 1. Accès au Bastion Host (depuis Internet)

### 🎯 Objectif

Vérifier que le Bastion est bien le seul point d’entrée SSH accessible depuis Internet.

### ⚙️ Ce que j’ai dû faire

- Récupérer la clé privée bastion-key.pem
- Vérifier les permissions
- Me connecter via l’IP publique du Bastion

### 💻 Commandes utilisées

```bash
chmod 400 bastion-key.pem
```

```bash
ssh -i bastion-key.pem ubuntu@IP_BASTION
```


## 🧠 Explication
Cet accès fonctionne car :
- le Bastion possède une IP publique
- son Security Group autorise uniquement mon IP sur le port 22
- il sert de point d’entrée sécurisé vers tout le réseau privé

## 🟡 2. Accès au Web Server (via Bastion uniquement)

### 🎯 Objectif

Accéder au Web Server en SSH, même s’il possède une IP publique pour HTTP/HTTPS.

###⚠️ Important :
Le Web Server a une IP publique, mais son port 22 n’est pas ouvert à Internet.
Donc SSH = Bastion obligatoire.

### ⚙️ Ce que j’ai dû faire
- Me connecter d’abord au Bastion
- Transférer la clé privée du Web Server vers le Bastion
- Sécuriser la clé
- Me connecter au Web Server via son IP privée

### 💻 Étapes réalisées

#### 1. Connexion au Bastion
```bash
ssh -i bastion-key.pem ubuntu@IP_BASTION
```
####2. Transfert de la clé Web Server vers le Bastion (depuis mon PC)
```bash
scp -i bastion-key.pem webserver-key.pem ubuntu@IP_BASTION:/home/ubuntu/
```

#### 3. Sécurisation de la clé sur le Bastion
```bash
chmod 600 webserver-key.pem
```
#### 4. Connexion au Web Server (depuis Bastion)
```bash
ssh -i webserver-key.pem ubuntu@IP_WEB_PRIVATE
```


## 🧠 Explication

Cet accès fonctionne uniquement via le Bastion car :

- 🔐 le port 22 du Web Server n’est ouvert que pour SG-bastion
- 🌍 son IP publique sert uniquement pour HTTP/HTTPS
- ❌ aucun SSH direct depuis Internet n’est possible

## 🔴 3. Accès au App Server (via Bastion)

### 🎯 Objectif

Valider l’accès à l’instance applicative privée (sans IP publique).

### 💻 Commande utilisée

```bash
ssh -i appserver-key.pem ubuntu@IP_APP_PRIVATE
```

## 🧠 Explication

Cet accès fonctionne car :

- le App Server est dans un subnet privé
- il n’a aucune IP publique
- seul le Bastion est autorisé via Security Group

## 🧠 Conclusion des tests SSH

✔ Le Bastion est le seul point d’entrée SSH depuis Internet
✔ Le Web Server possède une IP publique, mais SSH est privé
✔ Le App Server est totalement isolé (privé + pas d’IP publique)
✔ L’architecture respecte le modèle zero direct access

## 🚀 Résultat global

Cette configuration garantit :

- 🔐 une sécurité renforcée via Bastion Host
- 🧱 une segmentation claire entre public et privé
- 🚫 aucune exposition directe des serveurs internes
- 🏗️ une architecture conforme aux bonnes pratiques AW
