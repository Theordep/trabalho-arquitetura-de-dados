# Trabalho — Apache Spark com Delta Lake e Apache Iceberg

> Disciplina: **Arquitetura de Dados** · SATC — Engenharia de Software · 5ª Fase

[![Documentação](https://img.shields.io/badge/docs-GitHub%20Pages-blue)](https://Theordep.github.io/trabalho-arquitetura-de-dados/)
[![Python](https://img.shields.io/badge/python-3.12-blue)](https://www.python.org/)
[![PySpark](https://img.shields.io/badge/PySpark-3.5.3-orange)](https://spark.apache.org/)
[![Delta Lake](https://img.shields.io/badge/Delta%20Lake-3.2.0-blue)](https://delta.io/)
[![Apache Iceberg](https://img.shields.io/badge/Apache%20Iceberg-1.6.1-brightgreen)](https://iceberg.apache.org/)
[![uv](https://img.shields.io/badge/gerenciador-uv-purple)](https://docs.astral.sh/uv/)

---

## Descrição

Projeto acadêmico que demonstra o uso do **Apache Spark (PySpark)** integrado com dois formatos de tabela aberta:

- **Delta Lake** — camada ACID sobre Parquet, com suporte a *time travel* e evolução de esquema.
- **Apache Iceberg** — formato de tabela aberta para analítica em larga escala, com catálogo e *snapshots*.

Cada formato possui um notebook Jupyter dedicado com cenário real, modelagem ER, DDL e operações DML completas (`INSERT`, `UPDATE`, `DELETE`). A documentação conceitual está publicada via **MkDocs** no GitHub Pages.

**Equipe:** Pedro Ernesto · Carlos Eduardo · Axel Filastro

**Repositório:** [github.com/Theordep/trabalho-arquitetura-de-dados](https://github.com/Theordep/trabalho-arquitetura-de-dados)

**Documentação:** [theordep.github.io/trabalho-arquitetura-de-dados](https://Theordep.github.io/trabalho-arquitetura-de-dados/)

---

## Estrutura do projeto

```
trabalho-arquitetura-de-dados/
│
├── README.md                  # Este arquivo — guia de instalação e uso
├── .python-version            # Versão do Python utilizada (3.12)
├── .gitignore                 # Arquivos ignorados pelo Git
├── pyproject.toml             # Dependências e metadados do projeto (uv)
├── uv.lock                    # Lock file com versões exatas resolvidas
│
├── docs/                      # Documentação MkDocs
│   ├── index.md               # Contexto e objetivo do trabalho
│   ├── pyspark.md             # Explicação do Apache Spark / PySpark
│   ├── delta.md               # Explicação do Delta Lake + exemplos DML
│   └── iceberg.md             # Explicação do Apache Iceberg + exemplos DML
│
├── notebooks/                 # Notebooks Jupyter com código PySpark
│   ├── delta_lake.ipynb       # Cenário, DDL, INSERT/UPDATE/DELETE com Delta
│   └── iceberg.ipynb          # Cenário, DDL, INSERT/UPDATE/DELETE com Iceberg
│
└── tools/
    └── hadoop/
        └── bin/               # Binários necessários para Spark no Windows
            ├── winutils.exe
            └── hadoop.dll
```

---

## Pré-requisitos

Antes de instalar, garanta que você possui os itens abaixo:

### 1. Python 3.12

Verifique a versão instalada:

```bash
python --version
# Python 3.12.x
```

> Caso não tenha, instale via [python.org](https://www.python.org/downloads/) ou com **pyenv**: `pyenv install 3.12.13`

---

### 2. Java (JDK 11, 17 ou 21)

O Apache Spark **exige** Java instalado e configurado. Recomendamos o [Eclipse Temurin](https://adoptium.net/).

Verifique:

```bash
java -version
# openjdk version "21.x.x" ...
```

Configure as variáveis de ambiente (Windows):

| Variável | Exemplo de valor |
|---|---|
| `JAVA_HOME` | `C:\Program Files\Eclipse Adoptium\jdk-21.0.7.6-hotspot` |
| `PATH` | adicionar `%JAVA_HOME%\bin` |

> Reinicie o terminal após configurar.

---

### 3. uv (gerenciador de pacotes)

```bash
pip install uv
```

Verifique:

```bash
uv --version
# uv 0.x.x
```

> Documentação oficial: [docs.astral.sh/uv](https://docs.astral.sh/uv/)

---

### 4. Git

```bash
git --version
# git version 2.x.x
```

> Download: [git-scm.com](https://git-scm.com/)

---

## Instalação

### Passo 1 — Clonar o repositório

```bash
git clone https://github.com/Theordep/trabalho-arquitetura-de-dados.git
cd trabalho-arquitetura-de-dados
```

---

### Passo 2 — Criar o ambiente virtual e instalar dependências

```bash
uv sync --frozen
```

O `uv` lê o `pyproject.toml` e o `uv.lock`, cria o ambiente virtual em `.venv/` e instala todas as dependências com versões exatas. A primeira execução pode demorar pois baixa o PySpark (~300 MB).

> **Sem o `uv` instalado globalmente?** Use: `python -m uv sync --frozen`

---

### Passo 3 — Verificar a instalação

```bash
uv run python -c "import pyspark; print(pyspark.__version__)"
# 3.5.3
```

---

## Como usar

### Executar os notebooks

#### Opção A — VS Code

1. Abra a pasta do projeto no VS Code.
2. Abra `notebooks/delta_lake.ipynb` ou `notebooks/iceberg.ipynb`.
3. Selecione o kernel: **Python — `.venv`** (aparece no canto superior direito).
4. Execute todas as células com **Run All** (`Ctrl+F9`).

#### Opção B — Jupyter Lab no navegador

```bash
uv run jupyter lab
```

Acesse [http://localhost:8888](http://localhost:8888), abra a pasta `notebooks/` e execute os notebooks.

---

### Notebook Delta Lake (`delta_lake.ipynb`)

Demonstra o uso do **Delta Lake** no Spark:

1. Criação da `SparkSession` com extensões Delta (`DeltaSparkSessionExtension`, `DeltaCatalog`).
2. DDL — criação do banco `trabalho` e da tabela `pedidos_delta` com `USING DELTA`.
3. **INSERT** — inserção de 3 registros.
4. **UPDATE** — alteração do total do pedido de id=1.
5. **DELETE** — remoção do pedido de id=2.

> Na primeira execução, o Spark baixa os JARs do Delta via Maven (~6 MB).

---

### Notebook Iceberg (`iceberg.ipynb`)

Demonstra o uso do **Apache Iceberg** no Spark:

1. Criação da `SparkSession` com catálogo `local` (tipo `hadoop`, warehouse local).
2. DDL — criação de `local.pedidos_iceberg` com `USING iceberg`.
3. **INSERT**, **UPDATE** e **DELETE** via Spark SQL.

> Na primeira execução, o Spark baixa o runtime JAR do Iceberg via Maven (~40 MB). É necessário ter acesso à internet.

---

## Versões das dependências

| Pacote | Versão |
|---|---|
| Python | 3.12.13 |
| PySpark | 3.5.3 |
| delta-spark | 3.2.0 |
| Iceberg runtime JAR | `iceberg-spark-runtime-3.5_2.12:1.6.1` |
| JupyterLab | 4.2.x |
| ipykernel | 6.29.x |
| MkDocs | 1.6.x |
| mkdocs-material | 9.5.x |

> Versões exatas de todos os pacotes transitivos estão fixadas no [`uv.lock`](./uv.lock).

---

## Documentação

A documentação conceitual completa está publicada no GitHub Pages:

**[theordep.github.io/trabalho-arquitetura-de-dados](https://Theordep.github.io/trabalho-arquitetura-de-dados/)**

Para visualizar localmente:

```bash
uv run mkdocs serve
```

Acesse [http://127.0.0.1:8000](http://127.0.0.1:8000).

Para publicar no GitHub Pages:

```bash
uv run mkdocs gh-deploy --force
```

---

## Referências

- [jlsilva01/spark-delta](https://github.com/jlsilva01/spark-delta) — repositório de referência do professor
- [jlsilva01/spark-iceberg](https://github.com/jlsilva01/spark-iceberg) — repositório de referência do professor
- Canal [DataWay BR](https://www.youtube.com/@DataWayBR) no YouTube
- [Documentação oficial Delta Lake](https://docs.delta.io/latest/index.html)
- [Documentação oficial Apache Iceberg](https://iceberg.apache.org/docs/latest/)
- [Documentação PySpark](https://spark.apache.org/docs/latest/api/python/)
