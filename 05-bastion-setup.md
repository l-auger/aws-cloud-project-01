# 🟢 Bastion Host — Setup

---

## 🎯 Objectif

Le Bastion Host sert de point d’entrée sécurisé pour administrer les instances privées de l’infrastructure AWS.  
Il agit comme une passerelle SSH contrôlée entre Internet et le réseau interne.

---

## 🧱 Configuration EC2

- **Nom** : bastion-host  
- **AMI** : Ubuntu Server 22.04  
- **Subnet** : public-subnet  
- **IP publique** : activée  
- **Security Group** : SG-bastion  
- **Key Pair** : bastion-key.pem  
- **Rôle** : accès SSH d’administration

---

## 🔐 Security Group (SG-bastion)

### Inbound Rules

- SSH (22) → **mon IP uniquement**

### Outbound Rules

- All traffic → autorisé

---

## 🔑 Connexion SSH

Depuis ta machine locale :

```bash
ssh -i bastion-key.pem ubuntu@IP_BASTION
```
## 🧠 Rôle dans l’architecture

Le Bastion Host joue un rôle central dans la sécurisation de l’infrastructure AWS :

- 🚫 Évite l’exposition directe des instances privées
- 🎯 Centralise les accès SSH
- 🔐 Renforce la sécurité globale de l’infrastructure
- 🧱 Met en place une architecture en **“zero direct access”**

---

## 🔄 Flux autorisés

- 🌍 Internet → 🟢 Bastion *(SSH uniquement)*
- 🟢 Bastion → 🟡 Web Server *(SSH)*
- 🟢 Bastion → 🔴 App Server *(SSH)*

---

## 🚀 Résultat

- 🎯 Point d’entrée unique pour l’administration
- 🛡️ Réduction de la surface d’attaque
- 🧩 Séparation claire entre environnements public et privé