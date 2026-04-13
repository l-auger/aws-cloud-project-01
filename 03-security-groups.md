# 🔐 Security Groups — Cloud-Projet-01

---

## 🎯 Objectif

L’objectif de cette étape est de sécuriser les accès aux différentes instances de l’infrastructure AWS en utilisant des Security Groups.

Les Security Groups agissent comme des **pare-feux au niveau des instances**, permettant de contrôler précisément les flux réseau entrants et sortants.

---

## 🧠 Concept clé

Dans AWS, aucune communication réseau n’est autorisée par défaut sans règle explicite.

Chaque instance EC2 est associée à un Security Group qui définit :

- les accès autorisés en entrée (**inbound rules**)
- les connexions autorisées en sortie (**outbound rules**)

---

## 🧱 Architecture des Security Groups

Trois Security Groups ont été créés pour segmenter et sécuriser les accès :

- **SG-bastion**
- **SG-web**
- **SG-private**

---

## 🟢 SG-bastion

### 🎯 Rôle
Permettre un accès SSH sécurisé depuis Internet vers le Bastion Host.

### 🔐 Règles

**Inbound :**
- SSH (port 22) → uniquement depuis mon adresse IP

**Outbound :**
- Tout le trafic autorisé (par défaut)

---

## 🟡 SG-web

### 🎯 Rôle
Permettre l’accès public au serveur web.

### 🔐 Règles

**Inbound :**
- HTTP (port 80) → 0.0.0.0/0
- HTTPS (port 443) → 0.0.0.0/0 (optionnel)

**Important :**
- ❌ Aucun accès SSH autorisé depuis Internet

**Outbound :**
- Tout le trafic autorisé

---

## 🔴 SG-private

### 🎯 Rôle
Sécuriser l’accès à l’instance située dans le subnet privé en limitant strictement les connexions autorisées.

### 🔐 Règles

**Inbound :**
- SSH (port 22) → uniquement depuis **SG-bastion**

👉 Contrairement à une configuration classique basée sur une adresse IP, cette règle s’appuie directement sur un autre Security Group.

👉 Cela signifie que **seules les instances associées au SG-bastion (le Bastion Host)** peuvent initier une connexion SSH vers l’instance privée.

👉 Même une instance située dans le même VPC (ex : web-server) ne pourra pas se connecter si elle n’appartient pas à ce Security Group.

**Outbound :**
- Tout le trafic autorisé

---

## 🔄 Fonctionnement global

Grâce à cette configuration :

- L’accès SSH depuis Internet est uniquement possible vers le Bastion Host
- Le serveur web est accessible uniquement en HTTP/HTTPS
- L’instance privée n’est pas accessible directement depuis Internet

👉 Flux réel :

PC → Bastion (SSH autorisé)
Bastion → Instance privée (autorisé via SG)
Autres → Instance privée (refusé)

---

## 🧠 Point important

L’utilisation d’un Security Group comme source (SG-bastion) permet :

- de créer une **relation de confiance entre instances**
- de ne pas dépendre d’une adresse IP fixe
- de renforcer la sécurité globale
- de contrôler précisément les flux internes

👉 C’est une bonne pratique recommandée dans AWS pour les architectures sécurisées.

---

## 🧩 Problème rencontré

Une tentative d’accès SSH direct entre une instance publique et une instance privée a échoué.

### 🔍 Cause :

- absence de règle autorisant explicitement le flux SSH
- mauvaise compréhension initiale du fonctionnement des Security Groups
- isolation normale du subnet privé

---

## 🛠️ Solution

- création d’un Security Group dédié au Bastion
- autorisation du SSH vers l’instance privée uniquement depuis ce groupe
- mise en place d’un accès indirect sécurisé (bastion)

---

## 📸 Captures

### SG-bastion

![SG Bastion](./screenshots/sg-bastion.png)

---

### SG-web

![SG Web](./screenshots/sg-web.png)

---

### SG-private

![SG Private](./screenshots/sg-private.png)

---

## ✅ Résultat

- Accès SSH sécurisé et centralisé
- Isolation complète de l’instance privée
- Réduction de la surface d’attaque
- Architecture conforme aux bonnes pratiques cloud

Les Security Groups jouent un rôle essentiel dans la sécurisation de l’infrastructure AWS.