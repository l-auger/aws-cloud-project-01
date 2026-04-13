# ☁️ Cloud-Projet-01 — Architecture Cloud AWS sécurisée

![AWS](https://img.shields.io/badge/AWS-Cloud-orange?style=for-the-badge&logo=amazon-aws)
![VPC](https://img.shields.io/badge/Network-VPC-blue?style=for-the-badge)
![EC2](https://img.shields.io/badge/Compute-EC2-yellow?style=for-the-badge)
![Security](https://img.shields.io/badge/Security-Best_Practices-green?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)

---

## 🧭 Présentation du projet

Ce projet consiste en la conception et le déploiement d’une architecture cloud sécurisée sur AWS, inspirée d’un environnement d’entreprise.

L’objectif est de reproduire une infrastructure moderne en appliquant les bonnes pratiques de segmentation réseau, sécurisation des accès et isolation des services.

---

## 🎯 Objectifs pédagogiques et techniques

Ce projet m’a permis de renforcer mes compétences en Cloud Computing et administration d’infrastructure.

Il s’inscrit dans une logique de préparation aux certifications :
- AZ-900 (Azure Fundamentals)
- AZ-104 (Azure Administrator)

Concepts abordés (transverses cloud) :
- Virtualisation réseau (VPC / VNet)
- Segmentation public / privé
- Gestion d’instances cloud (EC2)
- Sécurisation des flux réseau
- Security Groups
- Architecture multi-couches

---

## 🧠 Compétences développées

- Conception d’architecture cloud sécurisée
- Administration d’un VPC AWS
- Gestion d’instances EC2 (public / privé)
- Configuration de Security Groups
- Mise en place d’un Bastion Host
- Reverse proxy NGINX
- API interne sur réseau privé
- Analyse réseau (SSH / HTTP / proxy)
- Résolution de problèmes d’infrastructure

---

## 🏗️ Architecture globale

- VPC : 10.0.0.0/16
- Subnet public : 10.0.1.0/24
  - Bastion Host
  - Web Server (NGINX)
- Subnet privé : 10.0.2.0/24
  - App Server (API 8080)
- Internet Gateway
- Security Groups segmentés

---

## 🔄 Flux réseau

### 🌍 Accès public
Client → Web Server (HTTP)

### 👨‍💻 Administration
Admin → Bastion (SSH)
Bastion → Web Server (SSH)
Bastion → App Server (SSH)

### 🔁 Application
Web Server → App Server (port 8080)

### 🔒 Sécurité
- Pas d’accès Internet direct au backend
- Pas de SSH direct vers les serveurs privés
- Accès uniquement via Bastion

---

## 🔐 Bastion Host

Rôle :
- Point d’entrée sécurisé
- Centralisation des accès SSH
- Réduction de la surface d’attaque

Sécurité :
- SSH limité à mon IP
- Accès aux serveurs privés uniquement via Bastion
- Principe du moindre privilège

---

## 🌐 Web Server (NGINX Reverse Proxy)

Serveur public servant de point d’entrée.

Rôles :
- Serveur web
- Reverse proxy vers API interne
- Isolation du backend

Configuration :
```nginx
location /api/ {
    proxy_pass http://10.0.2.252:8080/;
}
