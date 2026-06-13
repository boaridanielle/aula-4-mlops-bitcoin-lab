# Git, GitHub, Docker E Railway Com 3 Repositórios

Este guia usa **três repositórios Git**.

Essa separação deixa o projeto mais parecido com uma operação real de MLOps.

## Decisão Da Aula

| Repo | Pasta local | O que versiona | Por quê |
|---|---|---|---|
| `aula-4-mlops-bitcoin-lab` | raiz da pasta `4_Ciclo_Vida_MLOps_Bitcoin` | notebooks, roteiro e documentação | Material de aula e treino. |
| `aula-4-bitcoin-api` | `02_api_bitcoin/` | FastAPI, testes, `requirements.txt`, `Dockerfile` | Serviço de predição independente. |
| `aula-4-mlflow-railway` | `railway/mlflow_server/` | Dockerfile e docs do MLflow Server | Infraestrutura do MLflow no Railway. |

O kit local continua em uma pasta só para facilitar a aula.

No GitHub, os projetos ficam separados.

## Conceitos Essenciais

| Termo | Explicação |
|---|---|
| Git | Ferramenta que registra histórico de mudanças nos arquivos. |
| GitHub | Site que hospeda repositórios Git. |
| Commit | Registro de uma mudança. |
| Branch | Linha separada de trabalho. |
| Homologação | Ambiente usado para testar antes de produção. |
| Produção | Ambiente usado pelo usuário final. |
| Docker | Ferramenta que empacota aplicação e dependências. |
| Container | Execução isolada de uma imagem Docker. |
| Railway | Plataforma que faz deploy em nuvem. |
| Variável de ambiente | Configuração fora do código, como `API_KEY`. |
| Secret | Valor sensível. Não deve ser versionado. |

## O Que Não Versionar

Não envie para GitHub:

- `.env`;
- tokens;
- chaves reais;
- senhas;
- `runtime/`;
- `mlflow.db`;
- `mlruns/`;
- `__pycache__/`;
- `.pytest_cache/`;
- volumes locais;
- arquivos temporários.

Cada repo tem seu próprio `.gitignore`.

## Verificar Se Git Já Está Instalado

Rode:

```powershell
git --version
```

Se aparecer uma versão, o Git está instalado.

Se não aparecer, verifique se o Windows encontra o executável.

```powershell
where git
```

## Instalar Git — Opção 1: Site Oficial

Use esta opção se linha de comando estiver bloqueada.

Acesse:

```text
https://git-scm.com/install/windows
```

Passos:

1. Clique em **Download for Windows**.
2. Baixe o instalador `64-bit Git for Windows Setup`.
3. Execute o instalador.
4. Mantenha as opções padrão.
5. Confirme que **Git Credential Manager** está habilitado.
6. Feche e abra o PowerShell.
7. Rode `git --version`.

## Instalar Git — Opção 2: `winget`

Verifique se `winget` existe.

```powershell
winget --version
```

Instale o Git.

```powershell
winget install --id Git.Git -e --source winget
```

Feche e abra o PowerShell.

Confira:

```powershell
git --version
```

## Instalar Git — Opção 3: Chocolatey

Use apenas se o computador tiver Chocolatey.

Verifique:

```powershell
choco --version
```

Instale:

```powershell
choco install git -y
```

Feche e abra o PowerShell.

Confira:

```powershell
git --version
```

## Instalar Git — Opção 4: Scoop

Use apenas se o computador tiver Scoop.

Verifique:

```powershell
scoop --version
```

Instale:

```powershell
scoop install git
```

Feche e abra o PowerShell.

Confira:

```powershell
git --version
```

## Configurar Git

Configure o nome que aparecerá nos commits.

Troque `Seu Nome`.

```powershell
git config --global user.name "Seu Nome"
```

Configure o e-mail.

Use o e-mail da conta GitHub quando possível.

```powershell
git config --global user.email "seu-email@exemplo.com"
```

Configure `main` como branch padrão.

```powershell
git config --global init.defaultBranch main
```

Confira:

```powershell
git config --global --list
```

## Criar Os 3 Repositórios No GitHub

Acesse:

```text
https://github.com/
```

Crie três repositórios vazios:

```text
aula-4-mlops-bitcoin-lab
```

```text
aula-4-bitcoin-api
```

```text
aula-4-mlflow-railway
```

Para cada repo:

1. Clique em **New repository**.
2. Preencha o nome.
3. Escolha **Public** ou **Private**.
4. Não marque `Add a README file`.
5. Não adicione `.gitignore` pelo GitHub.
6. Clique em **Create repository**.

Copie a URL HTTPS de cada repo.

Exemplo:

```text
https://github.com/SEU_USUARIO/aula-4-bitcoin-api.git
```

## Repo 1 — Material Da Aula

Este repo fica na raiz da pasta `4_Ciclo_Vida_MLOps_Bitcoin`.

Ele **não** versiona a API nem o MLflow Server.

Essas duas pastas ficam ignoradas pelo `.gitignore` principal.

Entre na raiz da aula.

```powershell
cd CAMINHO_DA_PASTA\4_Ciclo_Vida_MLOps_Bitcoin
```

Inicialize o Git.

```powershell
git init
```

Veja os arquivos.

```powershell
git status
```

Adicione o material da aula.

```powershell
git add .
```

Confira se `02_api_bitcoin/`, `railway/mlflow_server/` e `runtime/` não entraram.

```powershell
git status
```

Crie o commit.

```powershell
git commit -m "Add Bitcoin MLOps lesson lab"
```

Conecte ao GitHub.

Troque `SEU_USUARIO`.

```powershell
git remote add origin https://github.com/SEU_USUARIO/aula-4-mlops-bitcoin-lab.git
```

Garanta a branch `main`.

```powershell
git branch -M main
```

Envie.

```powershell
git push -u origin main
```

## Repo 2 — API FastAPI

Este repo fica dentro de `02_api_bitcoin/`.

Entre na pasta da API.

```powershell
cd 02_api_bitcoin
```

Inicialize.

```powershell
git init
```

Veja os arquivos.

```powershell
git status
```

Adicione a API.

```powershell
git add .
```

Crie o commit.

```powershell
git commit -m "Add Bitcoin prediction API"
```

Conecte ao GitHub.

Troque `SEU_USUARIO`.

```powershell
git remote add origin https://github.com/SEU_USUARIO/aula-4-bitcoin-api.git
```

Garanta a branch `main`.

```powershell
git branch -M main
```

Envie.

```powershell
git push -u origin main
```

Crie a branch de homologação.

```powershell
git checkout -b homol
```

Envie `homol`.

```powershell
git push -u origin homol
```

Volte para `main`.

```powershell
git checkout main
```

Crie a branch de produção.

```powershell
git checkout -b prod
```

Envie `prod`.

```powershell
git push -u origin prod
```

Volte para `homol`.

```powershell
git checkout homol
```

Volte para a raiz da aula quando terminar.

```powershell
cd ..
```

## Repo 3 — MLflow Server Railway

Este repo fica dentro de `railway/mlflow_server/`.

Entre na pasta.

```powershell
cd railway/mlflow_server
```

Inicialize.

```powershell
git init
```

Veja os arquivos.

```powershell
git status
```

Adicione o serviço.

```powershell
git add .
```

Crie o commit.

```powershell
git commit -m "Add Railway MLflow server"
```

Conecte ao GitHub.

Troque `SEU_USUARIO`.

```powershell
git remote add origin https://github.com/SEU_USUARIO/aula-4-mlflow-railway.git
```

Garanta a branch `main`.

```powershell
git branch -M main
```

Envie.

```powershell
git push -u origin main
```

Volte para a raiz da aula.

```powershell
cd ..\..
```

## Docker Na Aula

Os alunos não precisam rodar Docker localmente.

O Docker será executado pelo Railway.

O papel do Docker é empacotar:

- Python;
- bibliotecas;
- código;
- comando de inicialização.

## Docker Local Opcional Para O Professor

Use apenas se Docker Desktop estiver instalado.

Entre na API.

```powershell
cd 02_api_bitcoin
```

Construa a imagem.

```powershell
docker build -t api-bitcoin-aula4 .
```

Rode em modo de teste.

```powershell
docker run --rm -p 8000:8000 `
  -e API_KEY="test-key" `
  -e MODEL_SOURCE="dummy" `
  -e MODEL_NAME="bitcoin_price_forecaster" `
  -e MODEL_ALIAS="homol" `
  api-bitcoin-aula4
```

Volte.

```powershell
cd ..
```

## Railway — Ordem Correta

No Railway, faça nesta ordem:

1. criar serviço `mlflow-server` pelo repo `aula-4-mlflow-railway`;
2. criar volume persistente para o MLflow;
3. gerar domínio do MLflow;
4. registrar modelos no MLflow remoto rodando notebooks localmente;
5. criar serviço `api-bitcoin` pelo repo `aula-4-bitcoin-api`;
6. configurar variáveis da API;
7. testar homologação;
8. promover para produção.

## Railway — MLflow Server

Siga o guia:

```text
railway/mlflow_server/README_MLFLOW_RAILWAY.md
```

No Railway:

1. Clique em **New Project**.
2. Escolha **Deploy from GitHub repo**.
3. Selecione `aula-4-mlflow-railway`.
4. Confirme que o `Dockerfile` está na raiz.
5. Adicione volume com mount path `/mlflow`.
6. Configure as variáveis do guia.
7. Gere domínio público.

## Popular O MLflow Remoto

Depois de criar o domínio do MLflow, copie a URL.

Exemplo:

```text
https://SEU_MLFLOW.up.railway.app
```

No PowerShell local, configure:

```powershell
$env:MLFLOW_TRACKING_URI="https://SEU_MLFLOW.up.railway.app"
```

Execute:

```text
01_treinamento_pipeline_bitcoin_mlflow.ipynb
```

Depois execute:

```text
05_monitoramento_drift_retreino_promocao.ipynb
```

Isso cria o modelo no MLflow remoto e aponta `homol`.

## Railway — API

No Railway:

1. Clique em **New**.
2. Escolha **GitHub Repo**.
3. Selecione `aula-4-bitcoin-api`.
4. Confirme que o `Dockerfile` está na raiz do repo.
5. Configure as variáveis.
6. Gere domínio público.

Como a API agora tem repo próprio, não configure subpasta como root.

O root do serviço é o próprio repositório.

## Variáveis Da API Em Homologação

No serviço `api-bitcoin`, abra **Variables**.

Adicione a chave de homologação.

```text
API_KEY=troque_por_uma_chave_de_homol
```

Adicione a URL do MLflow.

```text
MLFLOW_TRACKING_URI=https://SEU_MLFLOW.up.railway.app
```

Adicione o nome do modelo.

```text
MODEL_NAME=bitcoin_price_forecaster
```

Use alias de homologação.

```text
MODEL_ALIAS=homol
```

Use MLflow como fonte.

```text
MODEL_SOURCE=mlflow
```

## Testar API Em Homologação

Troque a URL pela URL real da API.

```powershell
Invoke-RestMethod -Method Get -Uri "https://SUA_API_HOMOL.up.railway.app/health"
```

Crie o cabeçalho.

Troque a chave pelo valor real.

```powershell
$headers = @{"X-API-Key" = "troque_por_uma_chave_de_homol"}
```

Teste `/model-info`.

```powershell
Invoke-RestMethod -Method Get `
  -Uri "https://SUA_API_HOMOL.up.railway.app/model-info" `
  -Headers $headers
```

Use também:

```text
04_consumo_api_homologacao.ipynb
```

Configure `API_BASE_URL` com a URL do Railway.

## Produção

Produção pode usar o mesmo repo da API com outra branch ou outro ambiente Railway.

Variáveis de produção:

```text
API_KEY=troque_por_uma_chave_de_prod
```

```text
MLFLOW_TRACKING_URI=https://SEU_MLFLOW.up.railway.app
```

```text
MODEL_NAME=bitcoin_price_forecaster
```

```text
MODEL_ALIAS=prod
```

```text
MODEL_SOURCE=mlflow
```

Para trocar o modelo em produção, atualize o alias `prod` no MLflow.

Não altere código da API.

## Checklist Antes De Produção

Confirme:

- MLflow remoto tem modelo `bitcoin_price_forecaster`;
- alias `homol` aponta para a versão validada;
- API homologação responde `/health`;
- API homologação responde `/model-info`;
- `/predict` exige `X-API-Key`;
- `/predict` retorna previsão;
- métricas novas foram revisadas;
- `prod` só aponta para versão aprovada;
- chave de produção é diferente da chave de homologação.

## Links Necessários

- Git para Windows: <https://git-scm.com/install/windows>
- GitHub: <https://github.com/>
- Railway: <https://railway.app/>
- Railway dashboard: <https://railway.app/dashboard>
