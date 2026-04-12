# ☁️ Cloud-Projet-01 — Architecture Cloud AWS sécurisée

![AWS](https://img.shields.io/badge/AWS-Cloud-orange?style=for-the-badge&logo=amazon-aws)
![VPC](https://img.shields.io/badge/Network-VPC-blue?style=for-the-badge)
![EC2](https://img.shields.io/badge/Compute-EC2-yellow?style=for-the-badge)
![Security](https://img.shields.io/badge/Security-Best_Practices-green?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)

---

## 🎯 Objectif du projet

Ce projet a pour objectif de concevoir et déployer une architecture cloud sécurisée sur AWS.

Il reproduit un environnement proche d’une infrastructure d’entreprise afin de comprendre :
- la segmentation réseau
- la sécurité des accès
- la gestion des flux entre environnements public et privé
- les bonnes pratiques d’administration cloud

---

## 🧠 Compétences démontrées

Ce projet met en avant ma capacité à :

- Concevoir une architecture cloud sur AWS
- Mettre en place un VPC avec segmentation réseau
- Gérer des instances EC2 publiques et privées
- Sécuriser les accès via Security Groups
- Comprendre les flux réseau entre sous-réseaux
- Mettre en place un Bastion Host
- Diagnostiquer et corriger des problèmes de connectivité (SSH / réseau)

---

## 🏗️ Architecture globale

L’architecture est composée de 3 éléments principaux :

- **Bastion Host** (accès sécurisé)
- **Subnet public** (serveur web)
- **Subnet privé** (serveur applicatif)

👉 Le schéma d’architecture est disponible dans `/architecture`.

---

## 🛡️ Bastion Host (point d’accès sécurisé)

Le Bastion Host est une instance EC2 placée dans le subnet public.

### 🎯 Rôle :
- Point d’entrée unique vers le réseau privé
- Accès SSH contrôlé et limité
- Réduction de l’exposition des machines internes

### 🔗 Flux :
Utilisateur → Bastion → Instance privée

### 🔐 Sécurité :
- SSH limité à une IP spécifique
- Aucun accès direct Internet vers les instances privées

---

## 🌐 Fonctionnement de l’architecture

- Le serveur web (EC2 public) est accessible depuis Internet via HTTP
- Le Bastion Host permet un accès sécurisé au réseau interne
- L’instance privée n’est pas accessible directement depuis Internet
- Les échanges internes sont contrôlés via Security Groups

---

## 🔐 Sécurité mise en place

- Isolation réseau via VPC
- Séparation public / privé
- Bastion Host comme point d’entrée sécurisé
- Security Groups appliquant le principe du moindre privilège
- Absence d’IP publique sur les ressources sensibles

---

## 🧩 Problème rencontré

Un problème de connexion SSH vers l’instance privée a été rencontré.

### Cause :
- absence d’accès direct volontaire (subnet privé)
- règles Security Group insuffisantes
- mauvaise compréhension initiale des flux AWS

### Résolution :
- mise en place d’un Bastion Host
- configuration des Security Groups pour autoriser uniquement les flux internes nécessaires

---

## 🖥️ Stack technique

- AWS VPC
- AWS EC2
- Internet Gateway
- Bastion Host
- Security Groups
- Ubuntu Server 22.04
- NGINX
- SSH

---

## 📈 Résultat final

✔ Serveur web accessible depuis Internet  
✔ Instance privée totalement isolée  
✔ Accès sécurisé via Bastion Host  
✔ Architecture conforme à une logique entreprise  
✔ Sécurité et segmentation réseau respectées  

---

## 🚀 Améliorations possibles

- Ajout d’un NAT Gateway pour les mises à jour des instances privées
- Automatisation avec Terraform (Infrastructure as Code)
- Ajout d’un Load Balancer pour la haute disponibilité
- Mise en place de monitoring (CloudWatch)

---

## 📚 Conclusion

Ce projet m’a permis de comprendre concrètement l’architecture cloud AWS et les bonnes pratiques de sécurité réseau.

L’ajout d’un Bastion Host permet de reproduire une architecture plus réaliste utilisée en entreprise, notamment pour sécuriser l’accès aux environnements sensibles.