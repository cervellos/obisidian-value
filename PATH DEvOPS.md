

interpretacion de minifiesto

apiVersion: apps/v1

kind: Deployment

metadata:

name: nginx-deployment

labels:

app: web

spec:

selector:

matchLabels:

app: web

replicas: 5

strategy:

type: RollingUpdate

template:

metadata:

labels:

app: web

spec:

containers:

—name: nginx

image: nginx

resources:

limits:

memory: 200Mi

requests:

[[cpu: 100m]]

[[memory: 200Mi]]

ports:

—containerPort: 80





## 12 Factor App  

codebase

dependencies

concurrency

processes

backing services

config

build

release and run

port binding

disposability

dev prod parity

logs

admin processes

## DevOps Prerequisite course


linux basics

virtual box networking

vagrant

networking basics

programming basics

database basics

Git

Apache web server

IPs and ports

SSL & TLS basics

YAML


## Linux for Beginners

Linux Shell

Kernel

RunLevels

FileTypes

RPM

YUM

DPKG

APG

vi editor

networking

dns

ssh

scp

iptables

systemd

nfs

lvm

Master Containerization

## Docker for Absolute Beginners  


containers

images

volumes

container

orchestration

networking


## Kubernetes for Beginners  


pods

replicasets

deployments

services

setting up local environment

## Helm for Beginners  



helm components

helm charts

pipelines

conditionals

with blocks

ranges

named templates

chart hooks

packaging and signing charts

## Istio Service Mesh  


sidecars

envoy

monoliths & microservices

service mesh

istio kiali

gateways

virtual services

destination rules

fault injection

timeouts

retries

circuit breaking

authentication

certificate management

distributed tracing with jaeger

## Kustomize  



kustomize vs helm

kustomize output

managing directories

image transformers

patches

overlays

generators

imperative commands


## Prometheus Certified Associate (PCA)  


observability fundamentals

prometheus fundamentals

PromQL

dashboarding & visualization

application instrumentation

service discovery

push gateway

alerting

monitoring kubernetes

mock exam

