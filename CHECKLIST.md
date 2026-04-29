# Checklist — trabalho Spark / Delta / Iceberg (PDF)

**Repositório:** [Theordep/trabalho-arquitetura-de-dados](https://github.com/Theordep/trabalho-arquitetura-de-dados)  
**PDF do enunciado:** `PDFS-APOIO/Trabalho_Apache_Spark_-_Delta_Lake_e_Apache_Iceberg-69e022f947e74.pdf`

Legenda: `[x]` atendido no código/docs desta pasta · `[ ]` pendente ou validação na sua máquina / GitHub

---

## Conformidade com o PDF

| Requisito (PDF) | Status |
|-----------------|--------|
| Grupo (máx. 3), repo público GitHub | `[ ]` *você disse que já criou/enviou e-mail — manter repo atualizado com este código* |
| Um ambiente **PySpark** + **Jupyter** (Lab ou VS Code) | `[x]` deps `pyspark`, `jupyterlab`, `ipykernel`; instruções no README |
| **1 notebook Delta** + **1 notebook Iceberg** (`.ipynb`) | `[x]` `notebooks/delta_lake.ipynb`, `notebooks/iceberg.ipynb` |
| **README** com passo a passo, libs e **versões** | `[x]` README + tabela de versões + `uv.lock` |
| **Só Poetry ou só UV** | `[x]` **UV** (`pyproject.toml` + `uv.lock`) |
| Padrão de projeto Python da aula | `[x]` estrutura com `docs/`, `data/`, `notebooks/`, `pyproject.toml` |
| Fontes sugeridas (DataWay BR, repos jlsilva01) citadas | `[x]` README |
| Notebook: **cenário**, **ER**, **DDL**, **fonte de dados**, **INSERT/UPDATE/DELETE** Delta e Iceberg | `[x]` código e texto; `[ ]` **imagem** do ER (PDF pede imagens — hoje só Mermaid + nota para colocar PNG em `docs/assets/`) |
| **MkDocs**: 1 página contexto, 1 Spark, 1 Iceberg, 1 Delta + explicar DML com exemplos | `[x]` `docs/*.md` com SQL de exemplo nas páginas Delta e Iceberg |
| **`mkdocs gh-deploy`** → URL pública | `[ ]` rodar após push; colar URL no README e em `docs/index.md` |
| Apresentação ~10 min, projeto **funcionando** | `[ ]` ensaiar com Java instalado |

---

## Instalação e execução (validação técnica)

| Verificação | Resultado na revisão desta pasta |
|---------------|-----------------------------------|
| `python -m uv sync --frozen` | `[x]` resolve e instala dependências |
| `.\.venv\Scripts\python.exe -m mkdocs build` | `[x]` build OK |
| `java -version` / `JAVA_HOME` | `[ ]` **neste ambiente Java não está no PATH** — no seu PC é obrigatório para Spark; sem isso os notebooks **não rodam** |
| Executar células `delta_lake.ipynb` | `[ ]` depende do Java acima |
| Executar células `iceberg.ipynb` (1ª vez baixa JAR) | `[ ]` idem + rede |

---

## Git local

| Item | Status |
|------|--------|
| Repositório com histórico em `main` | `[x]` *(push já realizado anteriormente)* |
| Manter `main` atualizado com entregas finais | `[ ]` |

---

## Melhorias opcionais (nota / enunciado)

- `[ ]` Exportar diagrama ER (PNG/SVG) para `docs/assets/` e referenciar em `index.md` e no notebook.
- `[ ]` Ler dados reais de `data/*.csv` antes do INSERT, se quiser fortalecer “fonte de dados”.
- `[ ]` Link do **GitHub Pages** no topo do README após `gh-deploy`.

---

*Última revisão automática do conteúdo do projeto (notebooks, docs, README, deps).*
