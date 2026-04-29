# Trabalho — Apache Spark, Delta Lake e Apache Iceberg

Repositório alvo: **[github.com/Theordep/trabalho-arquitetura-de-dados](https://github.com/Theordep/trabalho-arquitetura-de-dados)**

Projeto acadêmico (Engenharia de Dados) com **PySpark**, **Delta Lake** e **Apache Iceberg**, notebooks **Jupyter** e documentação **MkDocs**.

## Pré-requisitos

- **Python 3.12 ou 3.13** (recomendado 3.12; ver `.python-version`).
- **Java 8+** (JRE ou JDK). O Spark precisa de **`JAVA_HOME`** e do **`java`** no `PATH` (reinicie o terminal após configurar). Para menos surpresas no ecossistema Spark 3.5, prefira **JDK 11 ou 17** ([Eclipse Temurin](https://adoptium.net/)).
- **[uv](https://docs.astral.sh/uv/)** (opcional: `pip install uv` e use `python -m uv`).

### Windows (Hadoop “fake” + Delta)

No Windows, o Spark/HDFS local costuma exigir **`winutils.exe`** e **`hadoop.dll`** compatíveis com o Hadoop embutido no PySpark (~3.3.x). Este repositório inclui `tools/hadoop/bin/` (fonte comum da comunidade: [cdarlint/winutils](https://github.com/cdarlint/winutils)).

Os notebooks **ajustam sozinhos** `HADOOP_HOME` e o `PATH` se essa pasta existir. Opcionalmente você pode definir no sistema:

- `HADOOP_HOME` = caminho absoluto até `...\tools\hadoop`
- No `Path` do usuário: `%HADOOP_HOME%\bin` **antes** de outros Java antigos.

Ao encerrar o Spark, o Windows às vezes mostra aviso ao apagar JARs em `%TEMP%` — costuma ser inofensivo.

## Clonar e instalar

```bash
git clone https://github.com/Theordep/trabalho-arquitetura-de-dados.git
cd trabalho-arquitetura-de-dados
python -m uv sync --frozen
```

O ambiente virtual fica em `.venv/`.

## Executar os notebooks

1. Abra a pasta `notebooks/`.
2. Use o kernel **Python do `.venv`** (VS Code / Jupyter Lab).
3. Execute `delta_lake.ipynb` e `iceberg.ipynb` na ordem das células.

Na **primeira** execução do Iceberg, o Spark baixa o JAR do Iceberg pelo Maven (pode demorar).

## Documentação (MkDocs)

Com o ambiente ativado:

```bash
.\.venv\Scripts\python.exe -m mkdocs serve
```

Publicar no GitHub Pages (após configurar `remote` e branch `gh-pages`):

```bash
.\.venv\Scripts\python.exe -m mkdocs gh-deploy
```

## Referências sugeridas na disciplina

- [jlsilva01/spark-delta](https://github.com/jlsilva01/spark-delta)
- [jlsilva01/spark-iceberg](https://github.com/jlsilva01/spark-iceberg)
- Canal **DataWay BR** (YouTube)

## Primeiro push deste clone

```bash
git init
git branch -M main
git remote add origin https://github.com/Theordep/trabalho-arquitetura-de-dados.git
git add .
git commit -m "chore: estrutura inicial PySpark, Delta, Iceberg e MkDocs"
git push -u origin main
```

*(Se o remoto já existir com histórico, use `git pull` com estratégia adequada ou alinhe com o professor.)*

## Versões principais

| Pacote      | Versão  |
|------------|---------|
| PySpark    | 3.5.3   |
| Delta Lake | 3.2.0   |
| Iceberg runtime (JAR) | 1.6.1 (Spark 3.5, Scala 2.12) |

---

Veja **`CHECKLIST.md`** para o status dos itens do enunciado em relação a este repositório.
