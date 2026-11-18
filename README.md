# Greeting Service

Projet DevOps 2026 : un service web Java (Spring Boot) conteneurisé avec Docker et déployé sur Kubernetes (Minikube).

Réalisé par : Oumou CAMARA

## Description

Le service expose une route `/` qui renvoie un message de bienvenue : `Hello Oumou <3`.
Le projet de départ est celui du cours : https://github.com/charroux/kubernetes-minikube
Je l'ai adapté (message, nom de l'image, nom des ressources Kubernetes).

## Technologies

- Java 21, Spring Boot, Gradle
- Docker (build multi-étapes : Gradle puis JRE)
- Docker Hub : `oumou23/greeting-service`
- Kubernetes (Minikube)

## Structure

- `GreetingService/` : code source et Dockerfile
- `greeting-deployment.yml` : Deployment Kubernetes
- `greeting-service.yml` : Service Kubernetes (NodePort)
- `ingress.yml` : Ingress (prévu pour le palier 12)

## Lancer en local

```
cd GreetingService
./gradlew bootRun
```

Ouvrir http://localhost:8080

## Construire et publier l'image

```
cd GreetingService
docker build -t oumou23/greeting-service:1.0 .
docker login
docker push oumou23/greeting-service:1.0
```

## Déployer sur Kubernetes

```
minikube start
kubectl apply -f greeting-deployment.yml
kubectl apply -f greeting-service.yml
kubectl get pods
minikube service greeting-service
```

## Supprimer les ressources

```
kubectl delete -f greeting-service.yml
kubectl delete -f greeting-deployment.yml
```

## Suite prévue

- Gateway (Ingress)
- Deuxième service
- Base de données
- Sécurité