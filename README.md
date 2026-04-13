☁️ Cloud-Projet-01 — Architecture Cloud AWS sécurisée
https://img.shields.io/badge/AWS-Cloud-orange?style=for-the-badge&logo=amazon-aws https://img.shields.io/badge/Network-VPC-blue?style=for-the-badge https://img.shields.io/badge/Compute-EC2-yellow?style=for-the-badge https://img.shields.io/badge/Security-Best_Practices-green?style=for-the-badge https://img.shields.io/badge/Status-Completed-success?style=for-the-badge

🏗️ Architecture globale
Ce projet simule une infrastructure cloud sécurisée sur AWS, inspirée d’un environnement d’entreprise.
L’objectif : comprendre et maîtriser les bases d’une architecture cloud moderne, avec segmentation réseau, bastion, reverse proxy et API interne.
[Il semble que le résultat n’était pas sûr à afficher. Changeons un peu et essayons autre chose !]

🎯 Objectif du projet
Ce projet m’a permis de pratiquer et renforcer mes compétences en Cloud Computing à travers la mise en place d’une architecture AWS complète et sécurisée.
Il s’inscrit dans une démarche de préparation aux certifications :
- AZ‑900 (Azure Fundamentals)
- AZ‑104 (Azure Administrator)
Même si l’infrastructure est réalisée sur AWS, les concepts sont transverses :
- virtualisation réseau (VPC / VNet)
- segmentation logique (subnets publics / privés)
- gestion d’instances virtuelles
- contrôle des flux réseau
- sécurisation des accès (Security Groups / NSG)
- administration d’infrastructures cloud

🧠 Compétences démontrées
- Conception d’architecture cloud sécurisée
- Administration d’un VPC et de sous-réseaux
- Gestion d’instances EC2 (public / privé)
- Configuration avancée de Security Groups
- Mise en place d’un Bastion Host
- Mise en place d’un reverse proxy NGINX
- Déploiement d’une API interne dans un subnet privé
- Analyse et résolution de problèmes réseau (SSH, HTTP, proxy)
- Compréhension des flux réseau en environnement cloud

🌐 Architecture technique
L’infrastructure est composée de :
- VPC 10.0.0.0/16
- Subnet public 10.0.1.0/24
- Bastion Host
- Web Server (NGINX + reverse proxy)
- Subnet privé 10.0.2.0/24
- App Server (API interne sur port 8080)
- Internet Gateway pour l’accès public
- Security Groups en chaîne
- SG‑Bastion
- SG‑Public
- SG‑Private

🔄 Flux réseau détaillé
🌍 Accès public
- Client → Web Server (HTTP)
👨‍💻 Administration
- Admin → Bastion Host (SSH)
- Bastion → Web Server (SSH)
- Bastion → App Server (SSH)
🔁 Flux applicatif interne
- Web Server → App Server (port 8080)
🔒 Isolation
- ❌ Aucun accès Internet → App Server
- ❌ Aucun SSH direct → Web Server ou App Server
- ✔ Accès strictement contrôlé via Security Groups

🔐 Bastion Host
Le Bastion Host est le point d’entrée sécurisé vers le réseau privé.
Rôle :
- Accès SSH centralisé
- Réduction de la surface d’attaque
- Administration des instances privées
Sécurité :
- SSH autorisé uniquement depuis mon IP
- Accès aux instances privées uniquement via SG‑Bastion
- Principe du moindre privilège

🌍 Web Server (NGINX + Reverse Proxy)
Le Web Server est accessible publiquement et sert de reverse proxy vers l’API interne.
Fonctionnalités :
- Serveur web public
- Reverse proxy vers l’App Server
- Isolation du backend
- Aucune logique métier exposée
Configuration du reverse proxy :
location /api/ {
    proxy_pass http://10.0.2.252:8080/;
}



🧩 App Server (API interne)
L’App Server est totalement privé et héberge une API simple répondant sur le port 8080.
Caractéristiques :
- Pas d’IP publique
- Accessible uniquement depuis SG‑Public
- API interne simulée via un script Bash + netcat

🔐 Sécurité mise en place
- Isolation complète via VPC
- Subnet public / privé
- Bastion Host obligatoire pour l’administration
- Reverse proxy pour protéger l’API
- Security Groups en chaîne :
- SG‑Public → SG‑Private (port 8080)
- SG‑Bastion → SSH interne
- Principe du moindre privilège appliqué partout

🧪 Tests réalisés
✔ Administration
- SSH → Bastion
- SSH Bastion → Web Server
- SSH Bastion → App Server
✔ Application
- HTTP → Web Server
- Web Server → App Server (8080)
- Test reverse proxy :
curl http://localhost/api/


✔ Sécurité
- Impossible d’accéder à l’App Server depuis Internet
- Impossible d’accéder au Web Server en SSH depuis Internet

🖥️ Stack technique
- AWS VPC
- AWS EC2
- Internet Gateway
- Security Groups
- Bastion Host
- Ubuntu Server 22.04
- NGINX (reverse proxy)
- API interne (Bash + netcat)
- SSH

📈 Résultat final
✔ Serveur web accessible depuis Internet
✔ API interne accessible uniquement via reverse proxy
✔ Instance privée totalement isolée
✔ Accès sécurisé via Bastion Host
✔ Architecture conforme aux bonnes pratiques cloud
✔ Flux réseau maîtrisé et documenté

🚀 Améliorations possibles
- NAT Gateway pour mises à jour des instances privées
- Automatisation via Terraform (IaC)
- Load Balancer (ALB) pour la haute disponibilité
- Monitoring via CloudWatch
- IAM Roles pour sécuriser les accès aux services AWS
- HTTPS via Let’s Encrypt

📚 Conclusion
Ce projet m’a permis de construire une architecture cloud AWS réaliste, sécurisée et conforme aux bonnes pratiques d’entreprise.
Il démontre ma capacité à :
- concevoir une architecture cloud
- sécuriser les accès
- comprendre les flux réseau
- diagnostiquer et résoudre des problèmes réels
- mettre en place un reverse proxy et une API interne
