# ☁️ Cloud-Projet-01 — Architecture Cloud AWS sécurisée

![AWS](https://img.shields.io/badge/AWS-Cloud-orange?style=for-the-badge&logo=amazon-aws)
![VPC](https://img.shields.io/badge/Network-VPC-blue?style=for-the-badge)
![EC2](https://img.shields.io/badge/Compute-EC2-yellow?style=for-the-badge)
![Security](https://img.shields.io/badge/Security-Best_Practices-green?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)

---

## 🏗️ Architecture globale

![Architecture](./screenshots/aws-architecture.png)

Ce projet simule une infrastructure cloud sécurisée sur AWS, proche d’un environnement d’entreprise.

---

## 🎯 Objectif du projet

L’objectif est de concevoir et déployer une architecture cloud sécurisée afin de comprendre :

- La segmentation réseau dans AWS (VPC / Subnets)
- La gestion des flux entre environnements public et privé
- La sécurisation des accès via Security Groups
- La mise en place d’un Bastion Host
- Les bonnes pratiques d’architecture cloud

---

## 🧠 Compétences démontrées

Ce projet met en avant mes compétences en :

- Conception d’architecture cloud sur AWS
- Administration d’un VPC et de sous-réseaux
- Gestion d’instances EC2 (public / privé)
- Configuration de Security Groups (firewall cloud)
- Mise en place d’un Bastion Host
- Analyse et correction de problèmes réseau (SSH / connectivité)
- Compréhension des flux réseau en environnement cloud

---

## 🌐 Architecture technique

L’infrastructure est composée de :

- Un **VPC (10.0.0.0/16)** isolé
- Un **subnet public (10.0.1.0/24)** pour les services exposés
- Un **subnet privé (10.0.2.0/24)** pour les services internes
- Un **Bastion Host** comme point d’accès sécurisé
- Des **instances EC2** réparties selon leur rôle

---

## 🔄 Flux réseau

- 🌍 Internet → Web Server (HTTP/HTTPS)
- 👨‍💻 Admin → Bastion Host (SSH)
- 🔐 Bastion Host → Instance privée (SSH interne)
- ❌ Aucun accès direct Internet → instance privée

---

## 🔐 Bastion Host

Le Bastion Host est une instance EC2 placée dans le subnet public.

### 🎯 Rôle :
- Point d’entrée sécurisé vers le réseau privé
- Accès SSH contrôlé et centralisé
- Réduction de l’exposition des machines sensibles

### 🔗 Flux :
Utilisateur → Bastion → Instance privée

### 🛡️ Sécurité :
- SSH autorisé uniquement depuis une IP spécifique
- Accès au réseau privé uniquement via règles explicites

---

## 🖥️ Fonctionnement de l’architecture

- Le serveur web est accessible publiquement via HTTP
- Le Bastion Host permet un accès sécurisé aux machines internes
- L’instance privée n’est pas exposée à Internet
- Les communications internes sont strictement contrôlées via Security Groups

---

## 🔐 Sécurité mise en place

- Isolation complète via VPC
- Segmentation public / privé
- Principe du moindre privilège appliqué
- Bastion Host comme point d’entrée unique
- Absence d’IP publique sur les ressources sensibles

---

## 🧩 Problème rencontré

Une tentative d’accès SSH direct entre une instance publique et une instance privée a échoué.

### 🔍 Cause :
- compréhension initiale du modèle de sécurité AWS incomplète
- absence de règle explicite dans les Security Groups
- isolation volontaire du subnet privé

### 🛠️ Résolution :
- mise en place d’un Bastion Host
- configuration des Security Groups selon le principe du moindre privilège
- validation des flux réseau entre subnets

---

## 🧪 Tests réalisés

- Connexion SSH vers Bastion Host
- Connexion SSH Bastion → Instance privée
- Accès HTTP vers serveur web public
- Vérification de l’isolation du subnet privé

---

## 🖥️ Stack technique

- AWS VPC
- AWS EC2
- Internet Gateway
- Security Groups
- Bastion Host
- Ubuntu Server 22.04
- NGINX
- SSH

---

## 📈 Résultat final

✔ Serveur web accessible depuis Internet  
✔ Instance privée totalement isolée  
✔ Accès sécurisé via Bastion Host  
✔ Architecture conforme à une logique d’entreprise  
✔ Sécurité et segmentation réseau respectées  

---

## 🚀 Améliorations possibles

- Ajout d’un NAT Gateway pour les mises à jour des instances privées
- Automatisation avec Terraform (Infrastructure as Code)
- Ajout d’un Load Balancer pour la haute disponibilité
- Mise en place d’un monitoring (CloudWatch)
- Renforcement de la sécurité via IAM roles

---

## 📚 Conclusion

Ce projet m’a permis de comprendre concrètement l’architecture cloud AWS et les bonnes pratiques de sécurité réseau.

La mise en place d’un Bastion Host permet de reproduire une architecture réaliste utilisée en entreprise pour sécuriser les accès aux environnements sensibles tout en conservant une administration centralisée.