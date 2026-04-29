# Delta Lake

## Conceito

O **Delta Lake** é uma camada *open source* sobre armazenamento em arquivo (tipicamente **Parquet**) que adiciona **transações ACID**, histórico (*time travel*) e evolução de esquema ao ecossistema Spark.

## No trabalho

O notebook `notebooks/delta_lake.ipynb` cria o banco `trabalho`, a tabela **`pedidos_delta`** (`USING DELTA`) e executa DML em Spark SQL.

### Exemplos de DML (alinhados ao enunciado)

**INSERT** — incluir linhas:

```sql
INSERT INTO pedidos_delta VALUES
  (1, 'Ana', 100.0),
  (2, 'Beto', 200.0),
  (3, 'Carla', 50.0);
```

**UPDATE** — alterar colunas que satisfazem a condição:

```sql
UPDATE pedidos_delta SET total = 120.0 WHERE id = 1;
```

**DELETE** — remover linhas:

```sql
DELETE FROM pedidos_delta WHERE id = 2;
```

A extensão Delta é ativada na `SparkSession` com `io.delta.sql.DeltaSparkSessionExtension` e o catálogo `spark_catalog` apontando para `DeltaCatalog` (ver primeira célula de código do notebook).

## Links

- [Delta Lake](https://delta.io/)
- [Quickstart Delta + Spark](https://docs.delta.io/latest/quick-start.html)
