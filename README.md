# Search Engine Distribuída

Backend de uma **engine de busca distribuída**, inspirada conceitualmente em mecanismos como o Google, com foco na aplicação de conceitos de **Recuperação de Informação**, arquitetura de microserviços, processamento assíncrono e escalabilidade.

O sistema será responsável por realizar crawling de páginas, processar e indexar documentos, executar consultas e ranquear resultados utilizando técnicas como **BM25**, podendo evoluir para **PageRank, busca vetorial e busca híbrida**.

---

## Status do projeto

![Último commit](https://img.shields.io/github/last-commit/RaphaelMun1z/Spring-Microservices-Kafka-SearchEngine?style=flat-square)
![Tamanho do repositório](https://img.shields.io/github/repo-size/RaphaelMun1z/Spring-Microservices-Kafka-SearchEngine?style=flat-square)
![Issues](https://img.shields.io/github/issues/RaphaelMun1z/Spring-Microservices-Kafka-SearchEngine?style=flat-square)

---

## Stack

![Java](https://img.shields.io/badge/Java-25-E76F00?style=flat-square&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-4.x-6DB33F?style=flat-square&logo=springboot&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![OpenSearch](https://img.shields.io/badge/OpenSearch-005EB8?style=flat-square&logo=opensearch&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white)
![Apache Kafka](https://img.shields.io/badge/Apache_Kafka-231F20?style=flat-square&logo=apachekafka&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat-square&logo=kubernetes&logoColor=white)

---

## Arquitetura

A arquitetura separa dois fluxos principais:

- **Ingestion Plane:** crawling, processamento e indexação dos documentos.
- **Query Plane:** consulta, recuperação, ranking e entrega dos resultados.

A comunicação entre os componentes de ingestão será predominantemente **assíncrona e orientada a eventos através do Apache Kafka**.

---

## Microserviços

| Status | Serviço | Porta local | Papel |
|:------:|---------|:-----------:|-------|
| ⚪ | API Gateway | `8000` | Entrada principal, roteamento e proteção das APIs |
| ⚪ | Crawl Coordinator | `8100` | Coordenação do crawling e gerenciamento do URL Frontier |
| ⚪ | Crawler Worker | `8200` | Download e coleta das páginas |
| ⚪ | Document Processor | `8300` | Extração, normalização e processamento dos documentos |
| ⚪ | Indexing Service | `8400` | Indexação dos documentos no OpenSearch |
| ⚪ | Search Service | `8500` | Pesquisa, recuperação, ranking e snippets |
| ⚪ | Link Analysis Service | `8600` | Análise do grafo de links e sinais como PageRank |

---

## Infraestrutura de apoio

| Status | Componente | Porta local | Papel |
|:------:|------------|:-----------:|-------|
| ⚪ | Apache Kafka | `29092` | Mensageria e comunicação orientada a eventos |
| ⚪ | Kafka UI | `8090` | Inspeção de tópicos, consumidores e mensagens |
| ⚪ | PostgreSQL | `5432` | Metadados e dados transacionais |
| ⚪ | OpenSearch | `9200` | Indexação, recuperação e ranking dos documentos |
| ⚪ | OpenSearch Dashboards | `5601` | Administração e inspeção dos índices |
| ⚪ | Redis | `6379` | Cache, URL Frontier e dados temporários |
| ⚪ | Object Storage | `9000` | Armazenamento de páginas e documentos brutos |
| ⚪ | Keycloak | `8080` | Autenticação e autorização administrativa |
| ⚪ | Prometheus | `9090` | Coleta de métricas |
| ⚪ | Grafana | `3000` | Dashboards e observabilidade |

### Status

| Símbolo | Significado |
|:---:|---|
| ✅ | Implementado |
| 🟡 | Em desenvolvimento |
| ⚪ | Planejado |
| 🔴 | Com problema |

---

## Recuperação de Informação

Entre os conceitos que serão explorados pelo projeto estão:

- índice invertido;
- tokenização e normalização;
- TF-IDF;
- modelo vetorial;
- similaridade de cosseno;
- BM25;
- PageRank;
- Precision, Recall, MRR e nDCG;
- busca vetorial;
- busca híbrida.

---

## Infraestrutura

O ambiente local será inicialmente executado com **Docker Compose**.

A arquitetura poderá evoluir posteriormente para **Kubernetes**, permitindo escalabilidade horizontal independente dos principais serviços.

```text
Internet
   │
   ▼
API Gateway
   │
   ▼
Search Service ──────► Redis
   │
   └─────────────────► OpenSearch


Crawl Coordinator
   │
   ▼
Kafka
   │
   ▼
Crawler Workers
   │
   ▼
Document Processor
   │
   ▼
Kafka
   │
   ▼
Indexing Service
   │
   ▼
OpenSearch
