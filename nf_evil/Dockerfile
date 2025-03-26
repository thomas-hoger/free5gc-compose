# Utiliser une image de base avec Python préinstallé
FROM python:3.9-slim

# Mettre à jour les index des paquets et installer git
RUN apt-get update && apt-get install -y git

# Définir le répertoire de travail
WORKDIR /app

# Copier le contenu du dépôt GitHub dans le conteneur
RUN git clone https://github.com/HeineKayn/5G-dataset-generation.git /app

# Installer les dépendances Python
RUN pip install --no-cache-dir -r requirements.txt

# Définir la commande par défaut
CMD ["sh", "-c", "while true; do nc -l -p 8080; done"]
