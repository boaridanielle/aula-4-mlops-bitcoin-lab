# Aula 4 — Ciclo De Vida MLOps Com Bitcoin

Este roteiro assume que o aluno abriu a pasta `4_Ciclo_Vida_MLOps_Bitcoin` como raiz do projeto.

Use os comandos no PowerShell ou no Anaconda Prompt.

## Ordem Da Aula

| Etapa | Arquivo | Objetivo |
|---|---|---|
| 1 | `01_treinamento_pipeline_bitcoin_mlflow.ipynb` | Treinar modelos e registrar no MLflow. |
| 2 | `02_mlflow_ui_local.md` | Abrir e explicar a interface local do MLflow. |
| 3 | `02_api_bitcoin/README_API.md` | Rodar e testar a API FastAPI. |
| 4 | `03_git_github_railway.md` | Criar 3 repositórios, preparar Docker e publicar no Railway. |
| 5 | `04_consumo_api_homologacao.ipynb` | Consumir a API com `X-API-Key`. |
| 6 | `05_monitoramento_drift_retreino_promocao.ipynb` | Medir drift, retreinar e atualizar alias. |
| 7 | `railway/mlflow_server/README_MLFLOW_RAILWAY.md` | Subir MLflow Server no Railway com volume. |

## 1. Criar O Ambiente

Crie um ambiente conda novo.

```powershell
conda create -n aula_4_mlops_bitcoin python=3.12 --no-default-packages -y
```

Ative o ambiente.

```powershell
conda activate aula_4_mlops_bitcoin
```

Instale o `pip` no ambiente.

```powershell
conda install pip -y
```

Atualize o `pip`.

```powershell
python -m pip install --upgrade pip
```

Instale as dependências da API e do MLflow.

```powershell
pip install -r 02_api_bitcoin/requirements.txt
```

Instale as dependências extras dos notebooks.

```powershell
pip install matplotlib==3.10.9 seaborn==0.13.2 scipy==1.17.1 ipykernel==7.2.0 jupyter==1.1.1
```

Registre o kernel no Jupyter.

```powershell
python -m ipykernel install --user --name aula_4_mlops_bitcoin --display-name "Python (aula_4_mlops_bitcoin)"
```

## 2. Rodar O Treino Inicial

Abra o notebook abaixo.

```text
01_treinamento_pipeline_bitcoin_mlflow.ipynb
```

Selecione o kernel:

```text
Python (aula_4_mlops_bitcoin)
```

Execute todas as células.

## 3. Artefatos Gerados Pelo Notebook De Treino

Depois que o notebook `01_treinamento_pipeline_bitcoin_mlflow.ipynb` termina, estes arquivos locais são criados ou atualizados:

| Caminho | Conteúdo |
|---|---|
| `runtime/data/btc.csv` | Cache local da base CoinMetrics BTC. |
| `runtime/artifacts/feature_columns.json` | Lista de colunas que a API exige no `/predict`. |
| `runtime/artifacts/metrics_initial.json` | Métricas de validação e teste do modelo escolhido. |
| `runtime/artifacts/model_metadata.json` | Metadados didáticos do modelo publicado. |
| `runtime/artifacts/predictions_test.csv` | Amostra de previsões no conjunto de teste. |
| `runtime/artifacts/sample_payload.json` | Exemplo pronto de payload para a API. |
| `runtime/artifacts/local_model.joblib` | Cópia local do pipeline para inspeção em aula. |
| `runtime/mlflow.db` | Banco local do MLflow Tracking e Model Registry. |
| `runtime/mlruns/` | Artefatos internos salvos pelo MLflow. |

Tudo que é gerado pela execução fica dentro de `runtime/`.

Para limpar o projeto, apague essa pasta.

```powershell
Remove-Item -Recurse -Force .\runtime -ErrorAction SilentlyContinue
```

`runtime/` não deve ser enviado para o GitHub. O `.gitignore` já protege essa pasta.

## 4. Validar Código Local

Compile apenas os arquivos da aula.

> Se rodar `python -m compileall -q` sem caminho, o Python pode tentar listar arquivos internos do ambiente conda, como `python312.zip`. Isso gera aviso desnecessário. Use o comando abaixo.

```powershell
python -m compileall -q 02_api_bitcoin
```

Rode os testes automatizados da API.

```powershell
python -m pytest 02_api_bitcoin/tests
```

Resultado esperado:

```text
4 passed
```

## 5. Abrir O MLflow Local

Abra o MLflow UI na porta padrão `5000`.

```powershell
mlflow ui --backend-store-uri sqlite:///runtime/mlflow.db
```

Abra no navegador:

```text
http://127.0.0.1:5000
```

Se a porta `5000` estiver ocupada, pare o comando com `CTRL+C` e use a porta `5001`.

```powershell
mlflow ui --backend-store-uri sqlite:///runtime/mlflow.db --port 5001
```

Abra:

```text
http://127.0.0.1:5001
```

Seguir no arquivo:

```text
02_mlflow_ui_local.md
```

## 6. Rodar A API Local

Leia e execute:

```text
02_api_bitcoin/README_API.md
```

A API usa o modelo registrado no MLflow local.

Ela também pode rodar em modo `dummy` para validar contrato sem depender do MLflow.

## 7. Consumir A API

Depois que a API estiver rodando, abra:

```text
04_consumo_api_homologacao.ipynb
```

Se a API estiver na porta `8000`, não precisa alterar nada.

Se estiver na porta `8001`, ajuste `API_BASE_URL` no notebook para:

```text
http://127.0.0.1:8001
```

## 8. Drift, Retreino E Promoção

Depois da API e do MLflow estarem explicados, execute:

```text
05_monitoramento_drift_retreino_promocao.ipynb
```

Esse notebook:

- compara dados de referência com dados de 2026;
- calcula drift;
- mede performance no período novo;
- retreina com dados até `2026-05-31`;
- registra nova versão no MLflow;
- aponta `homol` para a versão nova.

## 9. Deploy

O deploy real no GitHub e Railway não é feito automaticamente.

Nesta versão da aula, o GitHub fica separado em três repositórios:

| Repo | Conteúdo |
|---|---|
| `aula-4-mlops-bitcoin-lab` | notebooks, roteiro e docs. |
| `aula-4-bitcoin-api` | API FastAPI, testes e Dockerfile. |
| `aula-4-mlflow-railway` | MLflow Server para Railway. |

No kit local, as pastas da API e do MLflow Server continuam dentro da pasta da aula.

No GitHub, elas ficam em repositórios próprios.

Use:

```text
03_git_github_railway.md
```

E:

```text
railway/mlflow_server/README_MLFLOW_RAILWAY.md
```

Na faculdade, os alunos não precisam rodar Docker localmente.

O Docker será usado pelo Railway para construir a API em nuvem.

## Observação Didática

Este projeto prevê `PriceUSD` do próximo dia.

Ele é útil para ensinar ciclo de vida de ML, não para recomendar compra ou venda de Bitcoin.

Séries de preço têm autocorrelação forte. Por isso, métricas altas podem parecer melhores do que a utilidade prática do modelo.
