# Apache Spark e PySpark

## O que é o Apache Spark

Motor de processamento distribuído (e modo **local** para desenvolvimento), com APIs em SQL, **DataFrame** e streaming. Neste trabalho usamos o modo **`local[*]`** para rodar no seu computador.

## PySpark

**PySpark** expõe a `SparkSession`, `DataFrame` e **Spark SQL** (`spark.sql(...)`). Os notebooks usam SQL para **INSERT**, **UPDATE** e **DELETE** nas tabelas **Delta** e **Iceberg**.

### Sessões neste projeto

| Notebook        | Extensões / pacotes principais |
|-----------------|---------------------------------|
| `delta_lake.ipynb` | `DeltaSparkSessionExtension`, `DeltaCatalog` |
| `iceberg.ipynb`    | `IcebergSparkSessionExtensions`, JAR `iceberg-spark-runtime-3.5_2.12` |

Requisito de infraestrutura: **JDK 11 ou 17** instalado, com `java` no `PATH` e preferencialmente **`JAVA_HOME`** definido. Sem Java, o Spark não inicia.

## Referências

- [Documentação PySpark](https://spark.apache.org/docs/latest/api/python/)
- [Spark SQL](https://spark.apache.org/docs/latest/sql-programming-guide.html)
