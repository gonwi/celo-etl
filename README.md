# Celo ETL

[![Build Status](https://travis-ci.org/codabl/celo-etl.png)](https://travis-ci.org/github/codabl/celo-etl)
[![Discord](https://img.shields.io/badge/discord-join%20chat-blue.svg)](https://discord.gg/6yWMkgM)

Celo ETL lets you convert blockchain data into convenient formats like CSVs and relational databases.

Celo ETL is a fork of 
## Quickstart

Install Celo ETL:

```bash
pip3 install celo-etl
```

Export blocks and transactions ([Schema](docs/schema.md#blockscsv), [Reference](docs/commands.md#export_blocks_and_transactions)):

```bash
> celoetl export_blocks_and_transactions --start-block 0 --end-block 100000 \
--provider-uri https://alfajores-forno.celo-testnet.org --blocks-output blocks.csv --transactions-output transactions.csv
```


For the latest version, check out the repo and call 
```bash
> pip3 install -e . 
> python3 celoetl.py
```

## Running Tests

```bash
> pip3 install -e .[dev,streaming]
> export ETHEREUM_ETL_RUN_SLOW_TESTS=True
> pytest -vv
```

### Running Tox Tests

```bash
> pip3 install tox
> tox
```

## Running in Docker

1. Install Docker https://docs.docker.com/install/

2. Build a docker image
        
        > docker build -t celo-etl:latest .
        > docker image ls
        
3. Run a container out of the image

        > docker run -v $HOME/output:/celo-etl/output celo-etl:latest export_all -s 0 -e 100000 -b 50000 -p https://alfajores-forno.celo-testnet.org

