# Utiliser une image de base légère, comme Node.js ou Nginx selon votre besoin
FROM node:16 AS build

# Définir le répertoire de travail
WORKDIR /app

# Copier le package.json et le package-lock.json
COPY package*.json ./

# Installer les dépendances
RUN npm install

# Copier le reste de l'application
COPY . .

# Construire l'application (si nécessaire)
RUN npm run build

# Étape de production
FROM nginx:alpine

# Copier les fichiers construits de l'étape précédente
COPY --from=build /app/build /usr/share/nginx/html

# Ajouter un fichier de configuration Nginx personnalisé si nécessaire
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Exposer le port 80
EXPOSE 80

# Commande pour démarrer Nginx
CMD ["nginx", "-g", "daemon off;"]

