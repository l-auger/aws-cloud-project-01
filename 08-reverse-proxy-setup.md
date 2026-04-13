# 🔁 NGINX Reverse Proxy Setup — Cloud-Projet-01

---

## 🎯 Objectif

Mettre en place un reverse proxy avec NGINX sur le Web Server afin de rediriger les requêtes HTTP vers le serveur applicatif interne (App Server).

---

## 🧱 Architecture concernée

- 🟢 Bastion Host → accès administration uniquement
- 🟡 Web Server → reverse proxy NGINX (public via architecture interne)
- 🔴 App Server → backend privé (non exposé directement)

👉 Le Web Server joue le rôle de passerelle HTTP vers l’App Server.

---

## ⚙️ Principe du reverse proxy

Le reverse proxy permet de :

- recevoir les requêtes HTTP côté Web Server
- les rediriger vers le serveur applicatif interne
- masquer complètement l’architecture backend

---

## 🔧 Configuration NGINX

### 📁 Fichier de configuration

Édition du fichier :

```bash
sudo nano /etc/nginx/sites-available/default
```
Configuration du reverse proxy pour l'api : 

![nginx](./screenshots/12-Ajout-confnginxAPI.png)
