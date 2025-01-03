# ElasticNotebook

Welcome to ElasticNotebook! ElasticNotebook is a checkpoint/restore tool for Jupyter Notebook sessions, which uses a 
novel live migration mechanism that is reliable, efficient, and platform-independent.

## Getting Started

### カレントディレクトリにダウンロードせずライブラリとして使う方法
```bash
pip install elastic-notebook-slim
```


### ソースコードをローカルのカレントディレクトリにダウンロードして使う方法
```bash
git clone https://github.com/MRyutaro/elastic_notebook_slim.git
pip install ./elastic_notebook_slim
```

## Project Structure

```
elastic-notebook
│   ElasticNotebook.py                     ## top-level cell magic
│───algorithm
│   │───baseline.py                        ##  Migrate/recompute all baselines
│   │───optimizer_exact.py                 ##  Replication plan generation via min-cut reduction (Section 5.3)
│   └───selector.py                        ##  Optimizer base class
└───core
    │───common
    │   │───checkpoint_file.py             ## Struct of ElasticNotebook's checkpoint file
    │   │───profile_graph_size.py          ## Size estimator for ElasticNotebook's Application History Graph
    │   │───profile_migration_speed.py     ## Profiler for network bandwidth
    │   └───profile_variable_size.py       ## Profiler for variable size
    │───graph
    │   │───cell_execution.py              ## Data structure for Cell Executions
    │   │───graph.py                       ## ElasticNotebook's Application History Graph (Section 4.1)
    │   └───variable_snapshot.py           ## Data strcutre for Variable Snapshots
    │───io
    │   │───adapter.py                     ## File writer base class
    │   │───filesystem_adapter.py          ## Writer for writing checkpoint file to NFS
    │   │───migrate.py                     ## Helper for creating checkpoint file
    │   │───pickle.py                      ## Helper for variable serializability detection
    │   └───recover.py                     ## Helper for unpacking checkpoint file
    │───mutation
    │   │───fingerprint.py                 ## Helper for detecting variable modifications via ID graph and object hash
    │   │───id_graph.py                    ## ID graph construction and comparison (Section 4.2)
    │   └───object_hash.py                 ## Object hash construction and comparison (Section 4.2)
    └───notebook
        │───checkpoint.py                  ## Line magic for checkpointing notebook session (Section 3.2)
        │───find_input_vars.py             ## AST analysis module for finding input variables
        │───find_output_vars.py            ## Helper for finding created/deleted variables via namespace difference
        │───restore_notebook.py            ## Line magic for restoring notebook session (Section 3.2)
        └───update_graph.py                ## Helper for updating Application History Graph
```
