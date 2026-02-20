es-kluster

es-1                     ssh hunter@172.16.80.10
es-2                     ssh hunter@172.16.80.11
es-3                     ssh hunter@172.16.80.12
kibana                   ssh hunter@172.16.80.13


# Elasticsearch 3-node Cluster + Kibana + NFS Snapshots (SLM)

## Topology
| Host | Role | IP | Ports |
|---|---|---:|---|
| es-1 | ES (master/data/ingest) | 172.16.80.10 | 9200, 9300 |
| es-2 | ES (master/data/ingest) | 172.16.80.11 | 9200, 9300 |
| es-3 | ES (master/data/ingest) | 172.16.80.12 | 9200, 9300 |
| kibana | Kibana                | 172.16.80.13 | 5601 |

## Versions
- Elasticsearch: 8.19.11
- Kibana: 8.19.11

## Config files in this repo
- `es-1/elasticsearch.yml`
- `es-2/elasticsearch.yml`
- `es-3/elasticsearch.yml`
- `kibana/kibana.yml`

> Note: certs (`certs/http.p12`, `certs/transport.p12`) are auto-generated on each node by Elastic security auto-config.
> We do NOT store certs or passwords in Git.

---

## Cluster checks

### Nodes / health
```bash
PASS='YOUR_ELASTIC_PASSWORD'
curl -k -u "elastic:$PASS" "https://172.16.80.10:9200/_cat/nodes?v"
curl -k -u "elastic:$PASS" "https://172.16.80.10:9200/_cluster/health?pretty"
curl -k -u "elastic:$PASS" "https://172.16.80.10:9200/_cat/master?v"
