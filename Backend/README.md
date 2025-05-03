# 🔙 Backend - Projet Fil Rouge

Ce projet est développé avec **Django** et **Django REST Framework**.

Il permet l'authentification via JWT et offre une API pour modifier le profil utilisateur.

---

## 🚀 Installation complète (copier/coller ce bloc dans votre terminal)

```bash
# Cloner le projet
git clone https://github.com/AWS-ODC-P4-C1/Backend.git
cd Backend

# Créer un environnement virtuel
python -m venv venv
source venv/bin/activate  # Linux/Mac
# venv\Scripts\activate    # Windows

# Installer les dépendances
pip install -r requirements.txt

# Appliquer les migrations
python manage.py migrate

# Lancer le serveur
python manage.py runserver

🔐 API d’authentification (JWT)
🔸 Login
Méthode : POST

URL : /api/login/

Exemple de requête JSON dans Postman :
{
  "username": "votre_username",
  "password": "votre_mot_de_passe"
}

Réponse attendue :

{
  "access": "token_access",
  "refresh": "token_refresh",
  "user": {
    "id": 1,
    "username": "mor",
    "email": "mor@example.com",
    "first_name": "Mor",
    "last_name": "Mbathie"
  }
}

🔸 Modifier son profil
Méthode : PUT

URL : /api/update-profile/

Header requis : Authorization: Bearer <access_token>

Exemple de corps JSON à envoyer dans Postman :

{
  "first_name": "Mor",
  "last_name": "Mbathie",
  "email": "mor@odc.sn"
}
👨‍💻 Contribuer au projet

# Créer une branche
git checkout -b feature/ma-fonctionnalite

# Ajouter vos modifications
git add .
git commit -m "feat: ajout de ma fonctionnalité"
git push origin feature/ma-fonctionnalite
🛎 Signalez-vous dans le groupe pour qu’on vous donne les droits de push.