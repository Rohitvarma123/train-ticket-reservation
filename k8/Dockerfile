FROM node:18-alpine AS backend
WORKDIR /backend
COPY backend/package*.json .
RUN npm install
COPY backend .
CMD ["npm", "start"]

FROM node:18-alpine AS frontend
WORKDIR /frontend
COPY frontend/package*.json .
RUN npm install
COPY frontend .
RUN npm run build

# final container
FROM nginx:alpine
COPY --from=frontend /frontend/build /usr/share/nginx/html
COPY --from=backend /backend /app/backend

