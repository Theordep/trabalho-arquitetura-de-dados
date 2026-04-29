# Apache Iceberg

## Conceito

O **Apache Iceberg** é um formato de **tabela aberta** para analítica em larga escala, com **ACID**, *snapshots* e evolução de partição/esquema, integrado ao Spark via catálogo e *runtime* JVM.

## No trabalho

O notebook `notebooks/iceberg.ipynb` registra o catálogo **`local`** (tipo `hadoop`, *warehouse* em `spark-warehouse/iceberg`), cria **`local.pedidos_iceberg`** e executa DML em Spark SQL.

### Exemplos de DML (alinhados ao enunciado)

**INSERT**:

```sql
INSERT INTO local.pedidos_iceberg VALUES
  (1, 'Ana', 100.0),
  (2, 'Beto', 200.0),
  (3, 'Carla', 50.0);
```

**UPDATE**:

```sql
UPDATE local.pedidos_iceberg SET total = 120.0 WHERE id = 1;
```

**DELETE**:

```sql
DELETE FROM local.pedidos_iceberg WHERE id = 2;
```

Na primeira execução, o Spark resolve o pacote Maven `org.apache.iceberg:iceberg-spark-runtime-3.5_2.12:1.6.1` (pode demorar e exige rede).

## Links

- [Apache Iceberg](https://iceberg.apache.org/)
- [Iceberg + Spark](https://iceberg.apache.org/docs/latest/spark-getting-started/)
