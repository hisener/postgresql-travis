# The newer versions of PostgreSQL + PostGIS on Travis CI

[![Build Status](https://travis-ci.org/hisener/postgresql-travis.svg?branch=master)](https://travis-ci.org/hisener/postgresql-travis)

## Versions

- [PostgreSQL 10 with PostGIS 2.4](#postgresql-10-with-postgis-24)
- [PostgreSQL 10 with PostGIS 2.5](#postgresql-10-with-postgis-25)
- [PostgreSQL 11 with PostGIS 2.5](#postgresql-11-with-postgis-25)

### PostgreSQL 10 with PostGIS 2.4

```yaml
addons:
  apt:
    packages:
      - postgresql-10-postgis-2.4
  postgresql: '10'
services:
  - postgresql
```

```
psql --version
psql (PostgreSQL) 10.7 (Ubuntu 10.7-1.pgdg16.04+1)

psql -c 'SELECT version()'
PostgreSQL 10.7 (Ubuntu 10.7-1.pgdg16.04+1) on x86_64-pc-linux-gnu, compiled by gcc (Ubuntu 5.4.0-6ubuntu1~16.04.11) 5.4.0 20160609, 64-bit

psql -c 'CREATE DATABASE travis_ci_test;' -U postgres
CREATE DATABASE
psql -c 'CREATE EXTENSION IF NOT EXISTS postgis' -U postgres
CREATE EXTENSION

psql -c 'SELECT PostGIS_full_version()' -U postgres
POSTGIS="2.4.4 r16526" PGSQL="100" GEOS="3.5.0-CAPI-1.9.0 r4084" PROJ="Rel. 4.9.2, 08 September 2015" GDAL="GDAL 1.11.3, released 2015/09/16" LIBXML="2.9.3" LIBJSON="0.11.99" LIBPROTOBUF="1.2.1" RASTER
```

### PostgreSQL 10 with PostGIS 2.5

```yaml
addons:
  apt:
    packages:
      - postgresql-10-postgis-2.5
      - postgresql-10-postgis-2.5-scripts
  postgresql: '10'

services:
  - postgresql
```

```
psql --version
psql (PostgreSQL) 10.7 (Ubuntu 10.7-1.pgdg16.04+1)

psql -c 'SELECT version()'
PostgreSQL 10.7 (Ubuntu 10.7-1.pgdg16.04+1) on x86_64-pc-linux-gnu, compiled by gcc (Ubuntu 5.4.0-6ubuntu1~16.04.11) 5.4.0 20160609, 64-bit

psql -c 'CREATE DATABASE travis_ci_test;' -U postgres
CREATE DATABASE
psql -c 'CREATE EXTENSION IF NOT EXISTS postgis' -U postgres
CREATE EXTENSION

psql -c 'SELECT PostGIS_full_version()' -U postgres
POSTGIS="2.5.2 r17328" [EXTENSION] PGSQL="100" GEOS="3.5.0-CAPI-1.9.0 r4084" PROJ="Rel. 4.9.2, 08 September 2015" GDAL="GDAL 1.11.3, released 2015/09/16" LIBXML="2.9.3" LIBJSON="0.11.99" LIBPROTOBUF="1.2.1" RASTER
```


### PostgreSQL 11 with PostGIS 2.5
```yaml
addons:
  apt:
    packages:
      - postgresql-11
      - postgresql-11-postgis-2.5
      - postgresql-11-postgis-2.5-scripts
  postgresql: '11'

before_install:
  - sudo sed -i 's/port = 5433/port = 5432/' /etc/postgresql/11/main/postgresql.conf
  - sudo cp /etc/postgresql/{10,11}/main/pg_hba.conf
  - sudo service postgresql stop
  - sudo service postgresql start 11

services:
  - postgresql
```

```
psql --version
psql (PostgreSQL) 11.2 (Ubuntu 11.2-1.pgdg16.04+1)

psql -c 'SELECT version()'
PostgreSQL 11.2 (Ubuntu 11.2-1.pgdg16.04+1) on x86_64-pc-linux-gnu, compiled by gcc (Ubuntu 5.4.0-6ubuntu1~16.04.11) 5.4.0 20160609, 64-bit

psql -c 'CREATE DATABASE travis_ci_test;' -U postgres
CREATE DATABASE
psql -c 'CREATE EXTENSION IF NOT EXISTS postgis' -U postgres
CREATE EXTENSION

psql -c 'SELECT PostGIS_full_version()' -U postgres
POSTGIS="2.5.2 r17328" [EXTENSION] PGSQL="110" GEOS="3.5.0-CAPI-1.9.0 r4084" PROJ="Rel. 4.9.2, 08 September 2015" GDAL="GDAL 1.11.3, released 2015/09/16" LIBXML="2.9.3" LIBJSON="0.11.99" LIBPROTOBUF="1.2.1" RASTER
```
