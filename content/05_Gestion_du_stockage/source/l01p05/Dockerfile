# Étape 1 : Utiliser une image de base Node.js
FROM node:14 AS build

# Étape 2 : Définir le répertoire de travail
WORKDIR /app

# Étape 3 : Copier les fichiers nécessaires
COPY . .

# Étape 4 : Installer les dépendances (si nécessaire, sinon cette étape peut être omise)
# RUN npm install

# Étape 5 : Construire l'application (si nécessaire, sinon cette étape peut être omise)
# RUN npm run build

# Étape 6 : Créer une image de production
FROM node:14

# Étape 7 : Définir le répertoire de travail
WORKDIR /app

# Étape 8 : Copier les fichiers de construction de l'étape précédente
COPY --from=build /app .

# Étape 9 : Exposer le port
EXPOSE 3000

# Étape 10 : Ajouter le fichier de configuration de l'application
RUN echo "const http = require('http');\n\
const port = 3000;\n\
const htmlContent = \`<!DOCTYPE html>\n\
<html lang='fr'>\n\
<head>\n\
    <meta charset='UTF-8'>\n\
    <meta name='viewport' content='width=device-width, initial-scale=1.0'>\n\
    <title>Welcome App</title>\n\
    <style>\n\
        body {\n\
            display: flex;\n\
            justify-content: center;\n\
            align-items: center;\n\
            height: 100vh;\n\
            margin: 0;\n\
            background-color: #202cac;\n\
            color: #ff0454;\n\
            font-family: Arial, sans-serif;\n\
            text-align: center;\n\
        }\n\
        h1 {\n\
            font-size: 3rem;\n\
        }\n\
    </style>\n\
</head>\n\
<body>\n\
    <h1>Bienvenue chez Neutron IT!</h1>\n\
</body>\n\
</html>\`;\n\
http.createServer((req, res) => {\n\
    res.writeHead(200, { 'Content-Type': 'text/html' });\n\
    res.end(htmlContent);\n\
}).listen(port, () => {\n\
    console.log(\`Serveur en cours d'exécution sur le port \${port}\`);\n\
});" > server.js

# Étape 11 : Démarrer l'application
CMD ["node", "server.js"]

