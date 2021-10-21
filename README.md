# Project config
```
az config set --local defaults.group=<resource group> defaults.location=uksouth
```
Download some PSC data as provided by companies house into the .gitignored ./data folder.
It has the format of the file in [./sampledata](./sampledata)

# Spike 1: Loading data into cosmosdb with python SDK (including rate-limiting)
> Note: do this with adf instead - much faster (todo, add sample pipeline to this repo)

Create a conda environment from the provided environment.yml file:
```
conda update conda
conda env create -f environment.yml
``` 

Get details of a separately provisioned cosmosdb
```
ACCT_NAME=<cosmos-db-account-name>

export ACCOUNT_URI=$(az cosmosdb show --name $ACCT_NAME --query documentEndpoint --output tsv)
export ACCOUNT_KEY=$(az cosmosdb list-keys --name $ACCT_NAME --query primaryMasterKey --output tsv)
```

or create a .env file for working with different instances of CosmosDB
```
MODE={provisioned|serverless}
ACCT_NAME=<cosmos-db-account-name or serverless account name>
ACCOUNT_URI=https://<cosmos-db-account-name>.documents.azure.com:443/
ACCOUNT_KEY=******
```

Then review [./load_data_to_cosmos.ipynb](./load_data_to_cosmos.ipynb)

## Spike 2: Visualising data directly with graphistry

Create a .env_graphistry file for working with Graphistry
```
TOKEN=******
USER=<user>
PASS=<pass>
```

Then see [graphistry.ipynb](graphistry.ipynb)

# Aux
- [jsonlines](https://jsonlines.readthedocs.io/en/latest/)

