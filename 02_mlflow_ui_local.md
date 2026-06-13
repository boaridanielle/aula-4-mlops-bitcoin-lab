# MLflow UI Local

A url `http://127.0.0.1:5000` é a interface visual do MLflow.


## O Que É

MLflow registra experimentos de Machine Learning.

Nesta aula, ele guarda:

- parâmetros de treino;
- métricas;
- artefatos;
- modelos registrados;
- aliases como `homol` e `prod`.

O endereço `127.0.0.1` significa que o site está rodando no seu próprio computador.

## Antes De Abrir

Execute primeiro o notebook:

```text
01_treinamento_pipeline_bitcoin_mlflow.ipynb
```

Ele cria:

```text
runtime/mlflow.db
```

E:

```text
runtime/mlruns/
```

Sem esses arquivos, a tela do MLflow pode abrir vazia.

## Abrir Na Porta Padrão

Rode este comando a partir da raiz da pasta `4_Ciclo_Vida_MLOps_Bitcoin`.

```powershell
mlflow ui --backend-store-uri sqlite:///runtime/mlflow.db
```

Abra no navegador:

```text
http://127.0.0.1:5000
```

## Se A Porta 5000 Estiver Ocupada

Pare o comando anterior com `CTRL+C`.

Depois rode o MLflow na porta `5001`.

```powershell
mlflow ui --backend-store-uri sqlite:///runtime/mlflow.db --port 5001
```

Abra no navegador:

```text
http://127.0.0.1:5001
```

Se a porta `5001` também estiver ocupada, tente `5002`.

```powershell
mlflow ui --backend-store-uri sqlite:///runtime/mlflow.db --port 5002
```

Abra:

```text
http://127.0.0.1:5002
```

## O Que Ver Na Tela

Na tela inicial, procure o experimento da aula.

O nome esperado é:

```text
aula_4_bitcoin_price_forecasting
```

Entre no experimento e abra a run mais recente.

### Metrics

Mostra os resultados do modelo.

Procure métricas como:

- `validation_rmse`;
- `validation_mae`;
- `test_rmse`;
- `test_mae`;
- `test_r2`;
- `baseline_test_rmse`.

Explique que métrica é evidência de comportamento, não garantia de valor financeiro.

### Parameters

Mostra configurações do treino.

Exemplos:

- nome do modelo;
- período de treino;
- quantidade de features;
- modelo escolhido.

### Artifacts

Mostra arquivos salvos pela run.

Nesta aula, artefatos úteis incluem:

- `feature_columns.json`;
- `metrics_initial.json`;
- `predictions_test.csv`;
- `sample_payload.json`;
- `model_metadata.json`.

### Models

Mostra o modelo registrado no Model Registry.

O nome esperado é:

```text
bitcoin_price_forecaster
```

### Aliases

Alias é um apelido para uma versão do modelo.

Nesta aula:

- `homol`: versão em homologação;
- `prod`: versão aprovada para produção.

A API carrega o modelo por alias.

Assim, a API não precisa mudar quando o modelo troca de versão.

## Avisos Que Podem Aparecer

### `Registry store URI not provided`

Não é erro para esta aula.

O MLflow está dizendo que vai usar o mesmo banco `sqlite:///runtime/mlflow.db` para tracking e registry.

### `localhost-only`

Não é erro.

O MLflow está protegido para aceitar acesso apenas do próprio computador.

Isso é adequado para aula local.

### `MLflow job backend does not support Windows`

Não é erro para esta aula.

Esse aviso fala sobre execução de MLflow Jobs no Windows.

Nós usamos tracking, artifacts e model registry. Esses recursos continuam funcionando.

## Como Parar

Volte ao terminal onde o MLflow está rodando.

Pressione:

```text
CTRL+C
```

O site local será encerrado.
