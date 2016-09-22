# Automated urban remote sensing with Python

## Setup

### Python environment

Using [Anaconda distribution](https://www.continuum.io/downloads):

``` bash
# Create a new virtual environment
conda create --name remotesensing python

# Install packages
conda install numpy scipy scikit-learn matplotlib \
              pandas psycopg2 rasterio fiona \
              jupyter
```

### Run the notebook

``` bash
# Clone the repository
git clone https://github.com/yannforget/foss4g.git your_directory
cd your_directory

# Change environment
source activate remotesensing

# Start jupyter notebook
jupyter notebook
```

### Populate a local PostGIS database with OSM data

Using [`osm2pgsql`](https://github.com/openstreetmap/osm2pgsql):

``` bash
# Start postgres if needed
sudo systemctl start postgres.service

# Login using psql
psql -U postgres
```

``` sql
CREATE DATABASE your_database;
\connect your_database;
CREATE EXTENSION postgis
```

``` bash
# Populate the database
osqm2pgsql --slim --create --multi-geometry --prefix osm \
  --database your_database --proj 32630 data/ouagadougou.xml
```
