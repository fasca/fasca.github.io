---
layout: post
title: Kubernetes
date: 2019-11-29
tags:
  - backend
  - devOps
  - orchestrateur
  - docker
  - script
description: Presentation de Kubernetes...
categories: DevOps
serie: Orchestrateur
published: true
---

# KUBERNETES

## Sommaire

- [KUBERNETES](#kubernetes)
  - [Sommaire](#sommaire)
  - [1- Introduction](#1--introduction)
    - [Architecture micro-services](#architecture-micro-services)
    - [Application Cloud Native](#application-cloud-native)
    - [Les ouils devops](#les-ouils-devops)
  - [2- La plateforme](#2--la-plateforme)
    - [Historique](#historique)
    - [Fonctionnalites](#fonctionnalites)
    - [Differentes categories de ressources](#differentes-categories-de-ressources)
    - [Specification des ressources](#specification-des-ressources)
    - [Labels et Annotations](#labels-et-annotations)
    - [Communication avec le cluster](#communication-avec-le-cluster)
    - [Les differents types de nodes](#les-differents-types-de-nodes)
    - [Les processus: API Server](#les-processus-api-server)
    - [Context d'utilisation](#context-dutilisation)
  - [3- Mise en place](#3--mise-en-place)
    - [Minikube](#minikube)
    - [Docker Desktop (macOS/Win)](#docker-desktop-macoswin)
    - [Exercice: Installation de Minikube](#exercice-installation-de-minikube)
    - [Cluster Kubernetes managé](#cluster-kubernetes-manag%c3%a9)
    - [Cluster Kubernetes managé: GKE](#cluster-kubernetes-manag%c3%a9-gke)
    - [Cluster Kubernetes managé: AKS](#cluster-kubernetes-manag%c3%a9-aks)
    - [Cluster Kubernetes managé: DigitalOcean](#cluster-kubernetes-manag%c3%a9-digitalocean)
    - [Cluster de production - d'autres outils](#cluster-de-production---dautres-outils)
    - [Installation avec kubeadm](#installation-avec-kubeadm)
  - [Creer et superviser un cluster Kubernetes avec Rancher](#creer-et-superviser-un-cluster-kubernetes-avec-rancher)
    - [Exercice: Installation sur DigitalOcean avec kubeadm (pour la creation de cluster)](#exercice-installation-sur-digitalocean-avec-kubeadm-pour-la-creation-de-cluster)
    - [Playground en ligne](#playground-en-ligne)
    - [Configuration](#configuration)
  - [4- Les objets: Pod](#4--les-objets-pod)
    - [Description des commandes](#description-des-commandes)
    - [Presentation des Pod](#presentation-des-pod)
  - [5- Les objets: Service](#5--les-objets-service)
  - [6- Les objets: Deployment](#6--les-objets-deployment)
  - [7- Les objets: Namespace](#7--les-objets-namespace)
  - [8- Application micro-services](#8--application-micro-services)
  - [9- Les objets: ConfigMap](#9--les-objets-configmap)
  - [10- Stack Elastic (ELK)](#10--stack-elastic-elk)
  - [11- Les objets: Secret](#11--les-objets-secret)
  - [12- Utilisateurs et droits d'acces RBAC](#12--utilisateurs-et-droits-dacces-rbac)
  - [13- DaemonSet](#13--daemonset)
  - [14- Les objets: Ingress](#14--les-objets-ingress)
  - [15- Application stateful](#15--application-stateful)
  - [16- Helm](#16--helm)
  - [17- Bonus](#17--bonus)

---

## 1- Introduction

blog kubernetes: https://blog.heptio.com/

### Architecture micro-services

- Decouplage de l'application en multiples services
- Processus independant ayant sa propre responsabilite metier
- Plus grande liberte de choix dans le langage
- Equipe dediee pour chaque service
- Un service peut etre mis a jour independamment des autres services
- Containers tres adaptes pour les micro-services
- Necessite des interfaces bien definies
- Deplace la complexite dans l'orchestration de l'application globale

### Application Cloud Native

- Application orientee microservices
- Packagee dans des containers
- Orchestration dynamique
- Nombreux projets portes par la CNCF (Kubernetes, Prometheus, Fluentd...)

### Les ouils devops
![differents outils devops](/assets/img/kubernetes/diff-outils.png)

---

## 2- La plateforme

### Historique

- Kubernetes / K8s / Kube
- "Homme de barre" / "Pilote" en grec
- Plateforme open source d'orchestration de containers
- Inspiree du systeme Borg de Google
- v1.0, juillet 2015
- v1.14.1, avril 2019

### Fonctionnalites

- Automatise le deploiement, la montee en charge et le management des applications microservices conteneurisees
- Boucle de reconciliation vers l'etat souhaite (self-healing)
- Gestion d'applications stateless(sans persistance de donne) et stateful(avec persistance de donne)
- Orchestration du stockage
- Gestion des Secrets et des Configurations
- Long-running et batch jobs
- RBAC (gestion des droits)

![concept de base 1](/assets/img/kubernetes/concept1.png)

- Un **Service** permet d'exposer un ensemble de **Pods** a l'interieur/exterieur du cluster

![concept de base 2](/assets/img/kubernetes/concept2.png)

La gestion du cluster est faite via le binaire **kubectl** ou l'interface web (et au fichier de conf kubeconfig)

### Differentes categories de ressources

 - gestion des applications (deployment, deamonset, statefulset, job, pod, ...)
 - discovery et load balancing (service, ...)
 - configuration des applications (ConfigMap, secret)
 - Stockage (PersistentVolume, PersistentVolumeClaim, StorageClass, ...)
 - Configuration du cluster et metadata (Role, ClusterRole, Namespace, ...)
 - Des objets supplementaires pour ajouter des fonctionnalites (CRD)

### Specification des ressources

- Fichier `yaml` ou `json`
- Une structure commune
  - apiVersion, Kind, m
  - etadata

Exemple de specification d'un Pod:
```yml
apiVersion: v1
kind: Pod
metadata:
    name: www
    labels:
        app: w3
spec:
    containers:
    - name: www
      image: nginx:1.16
```

Exemple de specification d'un Service:
```yml
apiVersion: v1
kind: Service
metadata:
    name: www
spec:
    selector:
        app: w3
    ports:
    - port: 80
      targetPort: 80
```

Exemple de specification d'un Deployment:
```yml
apiVersion: apps/v1
kind: Deployment
metadata:
    name: www
spec:
    replicas: 3
    selector:
        matchLabels:
            app: w3
        template:
            metadata:
                labels:
                    app: vote
            spec:
                containers:
                - name: vote
                  image: instavote/vote
```

### Labels et Annotations

- information attachees aux ressources
- format: key/value
- labels
  - utilises pour la selection d'objets
  - recuperation de collections
- annotations
  - ne sert pas a selectionner des objets
  - non interne a kubernetes
  - utilisees par des outils et librairies clientes

```yml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
    name: www
    annotations:
        ingress.kubernetes.io/rewrite-target: /
    labels:
        app: www
```

### Communication avec le cluster

En utilisant le binaire `kibectl` ou l'interface web.

```
$ kubectl get nodes
$ kubectl get pods
$ kubectl apply -f pod.yaml
```



### Les differents types de nodes

**Master**:

- responsable de la gestion du cluster ("control plane")
- expose l'API server
- schedule les Pods sur les nodes du cluster

**Worker / Node**:

- node sur lequel sont lances les Pods applicatifs
- communique avec le Master
- fournit les ressources aux Pods

```bash
$ kubectl get nodes
NAME        STATUS      ROLES       AGE     VERSION
kube-01     Ready       master      32m     v1.13.4
kube-02     Ready       <none>      24m     v1.13.4
kube-03     Ready       <none>      24m     v1.13.4
```

![vision d'ensemble](/assets/img/kubernetes/processus1.png)

![vision d'ensemble suite](/assets/img/kubernetes/processus2.png)

![vision d'ensemble suite2](/assets/img/kubernetes/processus3.png)

Pour lister les differents Pods il suffit de faire `kubectl get pod -n kube-system`

![vision d'ensemble suite2](/assets/img/kubernetes/processus4.png)

### Les processus: API Server

- API Rest / specification OpenAPI
  - https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.14
- Clients: kubectl, interface web, application tournant dans le cluster
- Chaque requete passe dans un pipeline
  - authentification
  - autorisation
  - admission controleurs

![workflow de creation d'un pod](/assets/img/kubernetes/workflow-creation-pod.png)

### Context d'utilisation

- definie le cluster auquel on s'adresse et avec quel utilisateur
- kubectx + kubens: Power tools for kubectl: [https://github.com/ahmetb/kubectx](https://github.com/ahmetb/kubectx)

On peut utiliser plusieurs clusters Kubernetes, par exemple un en local (minikube, docker desktop), un cluster manage, pre prod, prod... Le contexte permet de definire le cluster (de staging, de production..) auquel on s'adresse et avec quel utilisateur on le fait. Par defaut il est defini dans un fichier `${HOME}/.kube/config` ou `$KUBECONFIG` ou encore `--kubeconfig`.

---

## 3- Mise en place

### Minikube

- Tous les composants de Kubernetes dans une seule VM locale
- Un hyperviseur
  - plusieurs hyperviseurs supportes (VirtualBox, VMWare, HyperKit...)
  - https://virtualbox.org/
- Le binaire Minikube
  - https://github.com/kubernetes/minikube
- Le binaire kubectl
  - client pour commmuniquer avec le cluster via l'API server
  - https://kubernetes.io/docs/tasks/tools/install-kubectl/

### Docker Desktop (macOS/Win)

- Integration de la version upstream de Kubernetes
- Deploiement sur Swarm ou Kubernetes pendant le developpement

### Exercice: Installation de Minikube

- [PDF : Exercice installation de Minikube](/assets/img/kubernetes/minikube-installation.pdf)

**Pour lancer minikube:**

```sh
$ minikube start
$ kubectl get pods
$ kubectl get nodes
$ kubectl get version
$ kubectl get services #verifier @IP et Port d'un service
```

Exemple demarrer 2 instances du serveur web Nginx puis verifiez que les 2 instances sont disponibles:

```sh
$ kubectl run my-nginx --image=nginx --replicas=2 --port=80
deployment "my-nginx" created

$ kubectl get deploy
NAME    DESORED     CURRENT     UP-TO-DATE      AVAILABLE   AGE
my-nginx 2          2           2               1           12s

$ kubectl get pod
NAME                READY       STATUS      RESTARTS    AGE
my-nginx-ldkdjfgh   1/1         Running     0           16s
my-nginx-rotieuee   1/1         Running     0           16s
```

Nginx s’exécute dans deux conteneurs Docker **mais n'est pas accessible hors du cluster Kubernetes. La façon la plus simple d'exposer le déploiement et de le rendre accessible de l'extérieur est d'utiliser l'adresse IP standard `192.168.99.100` (de la Minikube VM) et d'exposer un NodePort**. Le système convertit l'adresse pour le port TCP de cette adresse IP vers l'adresse IP interne du conteneur.

```sh
$ kubectl expose deployment my-nginx --port=80 --type=NodePort
service "my-nginx" exposed
```

Pour s'assurer que Nginx est actif, ouvrez un navigateur Web, et entrez `http://192.168.99.100:<port>` soit `30709`, où le port est celui indiqué dans la commande kubectl get services

```
$ kubectl get services
NAME        TYPE        CLUSTER-IP      EXTERNAL-IP     PORT(S)         AGE
kubernetes  ClusterIP   10.96.0.1       <none>          443/TCP         8m
my-nginx    NodePort    10.101.62.218   <none>          80:30709/TCP    2s
```

**Interface graphique:**

Un serveur web est maintenant déployé sur Kubernetes.

Jusqu'à présent, nous avons utilisé des outils en ligne de commande pour gérer Kubernetes, ce qui est une excellente pratique pour l'automatisation. Cependant, une interface graphique facilite grandement l'exploration de ce qui se passe dans ce labo Kubernetes. Utilisez la commande `minikube dashboard` pour lancer un navigateur Web et ouvrir le tableau de bord.

Le tableau de bord affiche des informations sur les déploiements actifs, l'exécution de Pods (là où se trouvent les containers) et plusieurs autres éléments.

**Fermer, supprimer:**

Pour fermer Minikube, exécutez la commande `minikube stop` pour arrêter la VM. Minikube conservera les déploiements ainsi que les services définis au démarrage. Pour empêcher le déploiement de reprendre, supprimez l'installation avec `kubectl delete po,svc,deploy my-nginx` avant de fermer Minikube.

Un cluster Kubernetes en production aura certes plus d'un hôte. Ce laboratoire n'est utile que pour des tests à petite échelle.

### Cluster Kubernetes managé

- GKE - Google Kubernetes Engine
- AKS - Azure Container Service
- EKS - Amazon Elastic Container Service
- DigitalOcean
- OVH
- https://kubernetes.io/docs/setup/pick-right-solution/#hosted-solutions

### Cluster Kubernetes managé: GKE

Creation depuis l'interface https://console.cloud.google.com ou le binaire `gcloud`

```bash
$ gcloud init
$ gcloud container clusters create kube-demo --cluster-version=lastest --num-nodes 3
```

- https://cloud.google.com/sdk/install

### Cluster Kubernetes managé: AKS

Creation depuis l'inteface web https://portal.azure.com ou le binaire `az`

```bash
# Creation d'un groupe
$ az group create --name kube-group --location westeurope

# Creation du cluster
$ az aks create --name kube-demo --resource-group kubegroup --node-count 3 --generate-ssh-keys

# Mise a jour de la configuration de kubectl
$ az aks get-credentials --resource-group kubegroup --name kube-demo
```

- https://docks.microsoft.com/fr-fr/cli/azure/install-azure-cli

### Cluster Kubernetes managé: DigitalOcean

Creation depuis l'interface web https://digitalocean.com ou le binaire `doctl`

```bash
$ doctl k8s cluster create mykube --region lon1 --version 1.14.1-do.2 --node-pool="name=workers;size=s-2vcpu-4gb;count=5" --update-kubeconfig=true
```

- https://github.com/digitalocean/doctl

(recuperer le `kubeconfig.yaml` permet de faire la liaison entre sa machine et le cluster cloud `export KUBECONFIG=~/[PATH_kubeconfig.yml]`)

### Cluster de production - d'autres outils

**De nombreuses solutions pour creer et superviser**

- kubeadm -(pour la creation de cluster) https://kubernetes.io/docs/reference/setup-tools/kubeadm/kubeadm/
- kops - https://github.com/kubernetes/kops
- kubespray - https://www.github.com/kubernetes-sigs/kubespray
- Rancher - https://rancher.com/
- Pharos - https://www.kontena.io/pharos
- Docker EE (deploy Swarm et Kubernetes)
- Terraform + Ansible

### Installation avec kubeadm

- https://kubernetes.io/docs/setup/independent/install-kubeadm/
- Necessite que les nodes aient ete prealablement provisionnes
- Single master ou HA cluster
- Los de la mise en place d'un cluster avec kubeadm, il n'y a pas de solution de reseau par defaut, il faut en installer une comme "Weave Net"

```bash
# Initialisation du Master
$ kubeadm init

# Mise en place du reseau pour la communication entre les Pods
$ export kubever=$(kubectl version | base64 | tr -d '\n')
$ kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$kubever"

# Ajout de node supplementaires
$ kubeadm join --token <token> <master-ip>:<master-port>
```

## Creer et superviser un cluster Kubernetes avec Rancher

```bash
$ docker run -d --restart=unless-stopped -p 80:80 -p 443:443 rancher/rancher:latest
```

### Exercice: Installation sur DigitalOcean avec kubeadm (pour la creation de cluster)

- [PDF : Exercice installation sur DigitalOcean avec kubeadm](/assets/img/kubernetes/kubeadm-DigitalOcean.pdf)

Installation des prerequis sur les vm (voir pdf ci-dessus):
- un runetime de container (docker)
- le binaire `kubeadm` pour la creation du cluster
- le binaire `kubelet` pour la supervision des containers

### Playground en ligne

**labs.play-with-k8s.com**

- Online playground aka PWK
- Cree par Marcos Lilljedahl et Jonathan Leibiusky
- [labs.play-with-k8s.com](https://labs.play-with-k8s.com/)
- Mise en place d'un cluster en 1 min avec le binaire `kubeadm`
- 5 instances utilisables pendant 4h
- (tapez sur google "kubernetes playground" il y a plusieurs sites qui en proposent)

Quelques commandes:
- `kubectl get deploy, pod` : permet de voir les deploiement et les pod
- `kubectl get svc` : permet de voir les services (permet d'exposer le service a l'exterieur du cluster)

### Configuration

- Plusieurs facon pour fournir la configuration a `kubectl`
- Utilisation d'un ou plusieurs fichiers de configuration (fichiers kubeconfig)
- Flag `--kubeconfig`
  - specification d'un fichier kubeconfig
- Variable d'environnement `$KUBECONFIG`
  - liste de fichiers kubeconfig
  - merge des differents fichiers
- `${HOME}/.kube/config`
  - fichier utilise par defaut

![context 1](/assets/img/kubernetes/context1.png)
![context 2](/assets/img/kubernetes/context2.png)
![context 3](/assets/img/kubernetes/context3.png)
![context 4](/assets/img/kubernetes/context4.png)
![context 5](/assets/img/kubernetes/context5.png)
![exemple play with k8s](/assets/img/kubernetes/exemple-pwk.png)

## 4- Les objets: Pod

### Description des commandes

- [PDF : DESCRIPTION DES COMMANDES POUR LES DIFFERENTS OBJETS](/assets/img/kubernetes/summary.pdf)

**Differentes categories:**

- Gestion des applications lancees sur le cluster (Deployment, Pod...)
- Discovery et load balancing (Service...)
- Configuration des applications (ConfigMap, Secret...)
- Stockage (PersistentVolume, PersistentVolumeClaim...)
- Configuration du cluster et metadata (Namespace...)

**Une meme structure de base:**

- `apiVersion`: depend la maturite du composant (v1, apps/v1, apps/v1beta1...)
- `kind`: Pod, Deployment, Service...
- `metadata`: ajout de nom, labels, annotations, timestamp...
- `spec`: specification / description du composant

```yml
apiVersion: v1
kind: Pod
metadata:
    name: nginx
spec:
    containers:
    - name: www
      image: nginx:1.12.2
```

```yml
apiVersion: v1
kind: Service
metadata:
    name: votre-service
spec:
    selector:
        app: vote.
    ports:
    - port: 80
      targetPort: 80
```

```yml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
    name: www-domain
spec:
    rules:
        - host: www.example.com
          http:
            paths:
                - backend:
                    serviceName: www
                    servicePort: 80
```

### Presentation des Pod

- Groupe de containers tournant dans un meme context d'isolation
  - Linux namespaces: network, IPC, UTS...
- Partagent la stack reseau et le stockage (volumes)
- Adresse IP dediee, pas de NAT pour la communication entre les Pods
- Application decoupee en plusieurs specifications de Pods
- - Chaque specification correspond a un service metier (microservice)
- Scaling horizontal via le nombre de replica d'un Pod
  - creation de nouveaux Pod base sur la meme specification


**Exemple - server http**

- Spécification dans un fichier texte yaml (souvent préféré au format json)
- Spécification d’un Pod dans lequel est lancé un container basé sur l’image nginx

```yml
$ cat nginx-pod.yaml
apiVersion: v1
kind: Pod
metadata:
 name: nginx
spec:
 containers:
 - name: www
 image: nginx:1.12.2
Spécification d’un Pod dans lequel est lancé un container basé sur l’image nginx
```

VIDEO 17















---

## 5- Les objets: Service

---

## 6- Les objets: Deployment

---

## 7- Les objets: Namespace

---

## 8- Application micro-services

---

## 9- Les objets: ConfigMap

---

## 10- Stack Elastic (ELK)

---

## 11- Les objets: Secret

---

## 12- Utilisateurs et droits d'acces RBAC

---

## 13- DaemonSet

---

## 14- Les objets: Ingress

---

## 15- Application stateful

---

## 16- Helm

---

## 17- Bonus