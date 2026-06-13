# Aula 4 MLOps Bitcoin Lab

Este repositório contém o material principal da aula.

Ele inclui notebooks, roteiro e documentação.

## Repositórios Da Aula

Esta aula usa três repositórios Git:

| Repositório | Pasta local | Conteúdo |
|---|---|---|
| `aula-4-mlops-bitcoin-lab` | raiz da pasta da aula | notebooks, roteiro e docs. |
| `aula-4-bitcoin-api` | `02_api_bitcoin/` | FastAPI, testes e Dockerfile da API. |
| `aula-4-mlflow-railway` | `railway/mlflow_server/` | Dockerfile do MLflow Server no Railway. |

O `.gitignore` do repo principal ignora:

```text
02_api_bitcoin/
```

E:

```text
railway/mlflow_server/
```

Essas pastas devem ser versionadas nos seus próprios repositórios.

Se você estiver lendo o repo `aula-4-mlops-bitcoin-lab` no GitHub, essas pastas não aparecem nele.

Use os outros dois repositórios para ver a API e o MLflow Server.

## Saídas Geradas

Os notebooks salvam dados baixados, artefatos e MLflow local em:

```text
runtime/
```

Para limpar a execução local, apague somente essa pasta.

## Comece Por Aqui

Leia:

```text
00_roteiro_aula_4.md
```

Depois siga:

```text
03_git_github_railway.md
```

Esse guia mostra como criar os três repositórios.
