# ☁️ Cloud-Projet-01 — Architecture Cloud AWS sécurisée

![AWS](https://img.shields.io/badge/AWS-Cloud-orange?style=for-the-badge&logo=amazon-aws)
![Networking](https://img.shields.io/badge/Network-VPC-blue?style=for-the-badge)
![EC2](https://img.shields.io/badge/Compute-EC2-yellow?style=for-the-badge)
![Security](https://img.shields.io/badge/Security-Best_Practices-green?style=for-the-badge)
![Status](https://img.shields.io/badge/Project-Completed-success?style=for-the-badge)

---

## 🎯 Objectif du projet

Ce projet consiste à concevoir et déployer une architecture réseau sécurisée sur AWS afin de reproduire un environnement proche d’un cas réel en entreprise.

L’objectif n’est pas uniquement de “faire fonctionner des machines”, mais de comprendre la logique d’architecture cloud :
- isolation réseau
- exposition contrôlée des services
- gestion des flux internes
- séparation des responsabilités réseau

---

## 🧠 Ce que ce projet démontre

Ce projet met en avant ma capacité à :

- Concevoir une architecture cloud cohérente et sécurisée
- Comprendre les flux réseau dans un VPC AWS
- Segmenter un environnement en zones publiques et privées
- Sécuriser des instances via Security Groups
- Identifier et corriger des problèmes de connectivité (debug réseau)
- Déployer et configurer un service web sur une instance Linux

---

## 🏗️ Architecture mise en place

L’infrastructure repose sur une architecture simple mais réaliste :

- Un **VPC isolé**
- Un **subnet public** pour les services exposés
- Un **subnet privé** pour les services internes
- Une **Internet Gateway** pour l’accès sortant/public
- Des **Security Groups** pour contrôler les flux entrants/sortants

👉 Le schéma d’architecture est disponible dans le dossier `/architecture`.

---

## 🌐 Logique de fonctionnement

- Une instance EC2 publique héberge un serveur web (NGINX)
- Cette instance est accessible depuis Internet via HTTP
- Une seconde instance EC2 est placée dans un subnet privé
- Elle n’est pas accessible directement depuis Internet
- L’accès entre les deux instances est contrôlé via des règles de sécurité

Cette séparation permet de simuler une architecture multi-niveaux utilisée en production.

---

## 🔐 Sécurité et bonnes pratiques appliquées

- Isolation réseau via VPC
- Absence d’IP publique sur les ressources sensibles
- Restriction des accès SSH par source autorisée
- Utilisation de Security Groups comme firewall applicatif
- Principe du moindre privilège appliqué aux flux réseau

---

## 🧩 Problème rencontré et résolution

Un problème majeur a été rencontré lors de la tentative de connexion SSH à l’instance privée.

### Cause
- absence d’exposition réseau volontaire (subnet privé)
- règles Security Group insuffisantes entre instances
- mauvaise compréhension initiale des flux internes AWS

### Résolution
- ajout d’une règle SSH autorisant uniquement le Security Group de l’instance publique
- compréhension du rôle des Security Groups comme firewall stateful

---

## 🖥️ Stack technique

- AWS VPC
- AWS EC2
- Internet Gateway
- Security Groups
- Ubuntu Server 22.04
- NGINX
- SSH

---

## 📈 Résultat

L’architecture finale permet :

- Un accès public contrôlé au serveur web
- Une isolation complète des ressources privées
- Une communication interne sécurisée entre instances
- Une base d’architecture cloud proche des standards industriels

---

## 🚀 Améliorations possibles

Pour aller plus loin dans une approche production :

- Ajout d’un Bastion Host pour l’accès aux ressources privées
- Mise en place d’un NAT Gateway pour les mises à jour sortantes
- Automatisation de l’infrastructure avec Terraform
- Mise en place d’un Load Balancer pour la haute disponibilité

---

## 📚 Conclusion

Ce projet m’a permis de comprendre concrètement les bases de l’architecture cloud AWS, notamment la segmentation réseau, la sécurité des flux et le rôle des composants réseau dans un environnement distribué.

Il représente une première étape vers des architectures cloud plus complexes et scalables utilisées en entreprise.