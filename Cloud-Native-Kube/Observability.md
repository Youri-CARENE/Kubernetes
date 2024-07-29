### Synthèse et Explication Concise sur l'Observabilité Cloud Native dans Kubernetes

---

#### 1. Observability Fundamentals

**Observability** est la capacité de mesurer l'état interne d'un système en observant ses sorties externes. Les trois piliers de l'observabilité sont :

- **Logs** : Capturent les événements discrets.
- **Metrics** : Capturent les mesures et comptages.
- **Traces** : Capturent le cheminement des requêtes à travers les services.

---

#### 2. SLO/SLA/SLI

- **SLO (Service Level Objective)** : Objectif de performance que le service doit atteindre.
- **SLA (Service Level Agreement)** : Contrat entre un fournisseur de service et un client définissant les niveaux de service attendus.
- **SLI (Service Level Indicator)** : Mesure spécifique d'un aspect de la performance du service.

---

#### 3. Prometheus Use Case

**Prometheus** est un outil de surveillance et d'alerte open-source conçu pour collecter des métriques de divers services. Il est largement utilisé pour la surveillance des applications cloud native.

---

#### 4. Prometheus Basics

- **Prometheus** collecte des métriques en scrappant des endpoints HTTP exposés par les applications.
- **Métriques** sont stockées dans une base de données temporelle et peuvent être interrogées à l'aide du langage de requête PromQL.

---

#### 5. Prometheus Architecture

L'architecture de Prometheus comprend :

- **Prometheus Server** : Scrappe et stocke les métriques.
- **Exporters** : Exposent les métriques des systèmes et applications.
- **Alertmanager** : Gère les alertes envoyées par Prometheus.
- **Pushgateway** : Accepte les métriques poussées par les services courts.

---

#### 6. Prometheus - Node Exporter

**Node Exporter** est un exporter Prometheus qui expose des métriques sur les ressources matérielles et le système d'exploitation d'un nœud.

**Exemple de commande pour démarrer Node Exporter** :
```bash
./node_exporter
```

---

#### 7. Prometheus Configuration

La configuration de Prometheus est définie dans un fichier YAML. Elle inclut les paramètres pour le scrapping des cibles, la gestion des règles d'alerte et les paramètres globaux.

**Exemple de configuration** :
```yaml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']
```

---

#### 8. Prometheus - Metrics

Les **métriques** dans Prometheus sont des données sur les performances et l'état des applications. Elles sont exposées via des endpoints HTTP et peuvent inclure des compteurs, des jauges, des résumés et des histogrammes.

**Exemple de métriques** :
```plaintext
# HELP http_requests_total Total number of HTTP requests
# TYPE http_requests_total counter
http_requests_total{method="post",code="200"} 1027
```

---

#### 9. Prometheus - Monitoring Containers

Prometheus peut surveiller les conteneurs en utilisant des exporters spécifiques comme **cAdvisor**, qui collecte les métriques des conteneurs Docker et les expose à Prometheus.

**Exemple de configuration pour surveiller des conteneurs** :
```yaml
scrape_configs:
  - job_name: 'cadvisor'
    static_configs:
      - targets: ['localhost:8080']
```

---

#### 10. Prometheus - Monitoring Kubernetes

Prometheus peut surveiller les clusters Kubernetes en utilisant des exporters comme **kube-state-metrics** et **node-exporter** pour collecter les métriques des ressources Kubernetes.

**Exemple de configuration pour surveiller Kubernetes** :
```yaml
scrape_configs:
  - job_name: 'kubernetes-apiservers'
    kubernetes_sd_configs:
      - role: endpoints
    relabel_configs:
      - source_labels: [__meta_kubernetes_namespace, __meta_kubernetes_service_name, __meta_kubernetes_endpoint_port_name]
        action: keep
        regex: default;kubernetes;https
```

---

#### 11. Cost Management

**Cost Management** implique de surveiller et d'optimiser les coûts associés à l'exécution des applications et des infrastructures cloud native. Les outils et pratiques de gestion des coûts aident à identifier les inefficacités et à réduire les dépenses.

---