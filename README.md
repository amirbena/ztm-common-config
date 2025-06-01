# 🛠️ Shared Configuration for the Project

This repository contains the **shared environment configuration** used across our backend services, including:

- 🔧 Kafka topics and settings
- 🔴 Redis configuration
- 🧠 Neo4j graph database setup
- 🌐 Environment-specific values (dev, staging, prod)

## 📂 Structure

```
infra-config/
├── helm/
│   └── values/
│       ├── dev.yaml
│       ├── staging.yaml
│       └── prod.yaml
└── docker/
    └── neo4j.sh
```

## 🚀 Neo4j – Local Development Setup

To spin up a local Neo4j instance with the default credentials:

```bash
docker run \
  --name neo4j \
  -p 7474:7474 -p 7687:7687 \
  -v $HOME/neo4j/data:/data \
  -v $HOME/neo4j/logs:/logs \
  -v $HOME/neo4j/import:/import \
  -d \
  -e NEO4J_AUTH=neo4j/test \
  neo4j:5
```

- 🌐 Web interface: http://localhost:7474
- 🔑 Credentials:  
  - **Username**: `neo4j`  
  - **Password**: `test`

## 📦 How to Use in Other Services

Clone this repository as a Git submodule inside each service, or mount the `values/` directory during deployment to load environment-specific configurations.

```bash
helm upgrade --install my-service ./chart \
  -f ../infra-config/helm/values/dev.yaml
```

## 🧪 Notes

- All sensitive secrets (e.g. credentials) should be passed via Kubernetes secrets or external secret managers.
- Make sure to keep this configuration synchronized across environments.

---

Want to contribute or request changes? Feel free to open an issue or pull request 🙂
