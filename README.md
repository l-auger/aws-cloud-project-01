# ☁️ Cloud-Projet-01 — Architecture Cloud AWS sécurisée

![AWS](https://img.shields.io/badge/AWS-Cloud-orange?style=for-the-badge&logo=amazon-aws)
![VPC](https://img.shields.io/badge/Network-VPC-blue?style=for-the-badge)
![EC2](https://img.shields.io/badge/Compute-EC2-yellow?style=for-the-badge)
![Security](https://img.shields.io/badge/Security-Best_Practices-green?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)

---

## 🏗️ Architecture globale

Ce projet simule une infrastructure cloud sécurisée sur AWS, inspirée d’un environnement d’entreprise.

L’objectif est de comprendre concrètement les bases de l’architecture cloud moderne.

![Architecture](./screenshots/aws-architecture.png)

---

## 🎯 Objectif du projet

Ce projet a pour objectif de pratiquer et renforcer mes compétences en Cloud Computing à travers la mise en place d’une architecture AWS complète et sécurisée.

Il s’inscrit dans une démarche de préparation aux certifications :
- AZ-900 (Microsoft Azure Fundamentals)
- AZ-104 (Azure Administrator Associate)

Même si l’infrastructure est réalisée sur AWS, les concepts abordés sont transverses aux principaux providers cloud (AWS / Azure / GCP), notamment :

- virtualisation des réseaux (VPC / VNet)
- segmentation réseau (subnets / VLAN logiques)
- gestion des machines virtuelles
- contrôle des flux réseau
- sécurisation des accès (Security Groups / NSG)
- administration d’infrastructures cloud

---

## 🧠 Compétences démontrées

Ce projet met en avant mes compétences en :

- Conception d’architecture cloud sur AWS
- Administration d’un VPC et de sous-réseaux
- Gestion d’instances EC2 (public / privé)
- Configuration de Security Groups (firewall cloud)
- Mise en place d’un Bastion Host
- Analyse et résolution de problèmes de connectivité réseau (SSH)
- Compréhension des flux réseau en environnement cloud

---

## 🌐 Architecture technique

L’infrastructure est composée de :

- Un **VPC (10.0.0.0/16)** isolé
- Un **subnet public (10.0.1.0/24)** pour les services exposés
- Un **subnet privé (10.0.2.0/24)** pour les services internes
- Un **Internet Gateway** pour l’accès Internet du subnet public
- Un **Bastion Host** comme point d’accès sécurisé
- Des **instances EC2** réparties selon leur rôle

---

## 🔄 Flux réseau

- 🌍 Internet → Web Server (HTTP/HTTPS)
- 👨‍💻 Administrateur → Bastion Host (SSH)
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
- Accès aux instances privées uniquement via règles explicites
- Principe du moindre privilège appliqué

---

## 🖥️ Fonctionnement de l’architecture

- Le serveur web est accessible publiquement via HTTP
- Le Bastion Host permet un accès sécurisé aux machines internes
- L’instance privée n’est pas exposée à Internet
- Les communications internes sont strictement contrôlées via Security Groups

---

## 🔐 Sécurité mise en place

- Isolation complète via VPC
- Segmentation réseau public / privé
- Application du principe du moindre privilège
- Bastion Host comme point d’entrée unique d’administration
- Absence d’IP publique sur les ressources sensibles

---

## 🧩 Problème rencontré

Une tentative d’accès SSH direct entre une instance publique et une instance privée a échoué.

### 🔍 Cause :
- mauvaise compréhension initiale du modèle de sécurité AWS
- absence de règle explicite dans les Security Groups
- isolation volontaire du subnet privé (architecture correcte)

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
✔ Architecture conforme aux bonnes pratiques cloud  
✔ Sécurité et segmentation réseau respectées  

---

## 🚀 Améliorations possibles

- Ajout d’un NAT Gateway pour permettre les mises à jour des instances privées
- Automatisation de l’infrastructure avec Terraform (IaC)
- Ajout d’un Load Balancer pour la haute disponibilité
- Mise en place de monitoring avec AWS CloudWatch
- Amélioration de la sécurité via IAM Roles

---

## 📚 Conclusion

Ce projet m’a permis de comprendre concrètement les bases de l’architecture cloud AWS et les bonnes pratiques de sécurité réseau.

La mise en place d’un Bastion Host permet de reproduire une architecture réaliste utilisée en entreprise pour sécuriser les accès aux environnements sensibles tout en conservant une administration centralisée.