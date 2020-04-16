# Celo ETL

[![Build Status](https://travis-ci.org/blockchain-etl/ethereum-etl.png)](https://travis-ci.org/blockchain-etl/ethereum-etl)
[![Discord](https://img.shields.io/badge/discord-join%20chat-blue.svg)](https://discord.gg/wukrezR)

Celo ETL lets you convert blockchain data into convenient formats like CSVs and relational databases.


## Quickstart

Install Celo ETL:

```bash
pip3 install celo-etl
```

Export blocks and transactions ([Schema](docs/schema.md#blockscsv), [Reference](docs/commands.md#export_blocks_and_transactions)):

```bash
> celoetl export_blocks_and_transactions --start-block 0 --end-block 500000 \
--provider-uri https://alfajores-forno.celo-testnet.org --blocks-output blocks.csv --transactions-output transactions.csv
```

Export ERC20 and ERC721 transfers ([Schema](docs/schema.md#token_transferscsv), [Reference](docs/commands.md##export_token_transfers)):

```bash
> celoetl export_token_transfers --start-block 0 --end-block 500000 \
--provider-uri file://$HOME/Library/Ethereum/geth.ipc --output token_transfers.csv
```

Export traces ([Schema](docs/schema.md#tracescsv), [Reference](docs/commands.md#export_traces)):

```bash
> celoetl export_traces --start-block 0 --end-block 500000 \
--provider-uri file://$HOME/Library/Ethereum/parity.ipc --output traces.csv
```

---

Stream blocks, transactions, logs, token_transfers continually to console ([Reference](docs/commands.md#stream)):

```bash
> pip3 install celo-etl[streaming]
> celoetl stream --start-block 500000 -e block,transaction,log,token_transfer --log-file log.txt
```

Find other commands [here](https://celo-etl.readthedocs.io/en/latest/commands/).

For the latest version, check out the repo and call 
```bash
> pip3 install -e . 
> python3 celoetl.py
```

## Useful Links

- [Schema](https://celo-etl.readthedocs.io/en/latest/schema/)
- [Command Reference](https://celo-etl.readthedocs.io/en/latest/commands/)
- [Documentation](https://celo-etl.readthedocs.io/)
- [Exporting the Blockchain](https://celo-etl.readthedocs.io/en/latest/exporting-the-blockchain/)
- [Querying in Amazon Athena](https://celo-etl.readthedocs.io/en/latest/amazon-athena/)
- [Querying in Google BigQuery](https://celo-etl.readthedocs.io/en/latest/google-bigquery/)
- [Querying in Kaggle](https://www.kaggle.com/bigquery/ethereum-blockchain)
- [Airflow DAGs](https://github.com/blockchain-etl/celo-etl-airflow)
- [Postgres ETL](https://github.com/blockchain-etl/celo-etl-postgresql)

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

        > docker run -v $HOME/output:/celo-etl/output celo-etl:latest export_all -s 0 -e 200000 -b 50000 -p https://alfajores-forno.celo-testnet.org
        > docker run -v $HOME/output:/celo-etl/output celo-etl:latest export_all -s 2018-01-01 -e 2018-01-01 -p https://alfajores-forno.celo-testnet.org

