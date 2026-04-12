# ☁️ Projet-Cloud — Infrastructure AWS (VPC & Sécurité)

![AWS](https://img.shields.io/badge/AWS-Cloud-orange?style=for-the-badge&logo=amazon-aws)
![VPC](https://img.shields.io/badge/AWS-VPC-blue?style=for-the-badge)
![EC2](https://img.shields.io/badge/AWS-EC2-yellow?style=for-the-badge)
![NGINX](https://img.shields.io/badge/Web-NGINX-green?style=for-the-badge&logo=nginx)
![Status](https://img.shields.io/badge/Status-Terminé-success?style=for-the-badge)

---

## 🎯 Objectif du projet

Ce projet consiste à concevoir et déployer une architecture réseau sécurisée sur AWS afin de comprendre les fondamentaux du cloud computing en environnement réel.

L’objectif est de reproduire une infrastructure de type entreprise avec séparation des réseaux, contrôle des accès et hébergement d’un service web.

---

## 🧠 Compétences développées

✔ Conception d’une architecture cloud AWS  
✔ Création et configuration d’un VPC  
✔ Segmentation réseau (public / privé)  
✔ Gestion des flux avec Security Groups  
✔ Déploiement de machines virtuelles EC2  
✔ Mise en place d’un serveur web (NGINX)  
✔ Analyse des problèmes réseau et debugging SSH  

---

## 🏗️ Architecture

📌 Le projet est basé sur :

- Un VPC isolé
- Un subnet public (serveur web)
- Un subnet privé (application interne)
- Une Internet Gateway
- Des Security Groups pour filtrer les accès

📷 Architecture :
![Architecture](./architecture/schema-vpc.png)

---

## 🌐 Fonctionnement

- Le serveur web est accessible via Internet (HTTP)
- L’instance privée est isolée du réseau public
- Les échanges internes sont sécurisés via SSH contrôlé
- Aucun accès direct Internet sur la machine privée

---

## 🔐 Sécurité mise en place

- Séparation réseau public / privé
- Firewall virtuel via Security Groups
- Accès SSH restreint par IP ou instance source
- Absence d’exposition directe de la machine privée

---

## 🖥️ Technologies utilisées

![AWS](https://img.shields.io/badge/AWS-Cloud-orange?logo=amazon-aws)
![Ubuntu](https://img.shields.io/badge/Ubuntu-22.04-E95420?logo=ubuntu)
![Linux](https://img.shields.io/badge/Linux-Server-black?logo=linux)
![Networking](https://img.shields.io/badge/Network-VPC-blue)

- AWS VPC
- AWS EC2
- AWS Internet Gateway
- AWS Security Groups
- Ubuntu Server 22.04
- NGINX

---

## ⚙️ Problème rencontré

Lors de la mise en place, l’accès SSH à l’instance privée ne fonctionnait pas.

### Cause :
- absence d’accès Internet
- règles Security Group insuffisantes
- mauvaise compréhension des flux réseau internes

### Résolution :
- ajout d’une règle SSH depuis le Security Group du serveur web

---

## 📈 Résultat final

✔ Serveur web accessible depuis Internet  
✔ Serveur privé isolé et sécurisé  
✔ Communication interne contrôlée  
✔ Architecture fonctionnelle et conforme aux bonnes pratiques cloud  

---

## 🚀 Améliorations possibles

- Mise en place d’un Bastion Host 🔐  
- Ajout d’un NAT Gateway 🌍  
- Automatisation avec Terraform ⚙️  
- Load Balancer + scalabilité 📈  

---

## 📚 Conclusion

Ce projet m’a permis de comprendre concrètement l’architecture cloud AWS et les bonnes pratiques de segmentation réseau et sécurité.

Il constitue une première étape vers la conception d’infrastructures cloud professionnelles.