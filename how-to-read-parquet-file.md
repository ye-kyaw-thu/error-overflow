## Installation

```
pip install parquet-cli
```

## View the Metadata

```
(base) C:\Users\ye\.spyder-py3\notebook\1019715464.parquet>parq 1019715464.parquet

 # Metadata
 <pyarrow._parquet.FileMetaData object at 0x000002AA78C429A0>
  created_by: parquet-cpp-arrow version 11.0.0
  num_columns: 1631
  num_rows: 161461
  num_row_groups: 1
  format_version: 2.6
  serialized_size: 770816

(base) C:\Users\ye\.spyder-py3\notebook\1019715464.parquet>
```

## check head 10

```
(base) C:\Users\ye\.spyder-py3\notebook\1019715464.parquet>parq 1019715464.parquet --head 10

## Check the schema

(base) C:\Users\ye\.spyder-py3\notebook\1019715464.parquet>parq 1019715464.parquet --schema
```

## Reference

1. https://stackoverflow.com/questions/36140264/inspect-parquet-from-command-line

