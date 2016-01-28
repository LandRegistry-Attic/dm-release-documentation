## Upgrade to version 0.1.0

* Need to import file: test_md.csv into mortgage_document table:
* The DEED_DATABASE_URI environment variable needs to have been defined

```
    python3 ./migrations/setup_initial_data/data_importer.py /data/mortgage_document/ $DEED_DATABASE_URI mortgage_document
```
