# Minggu 12 
## Drupal 
1. buka docker 
2. membuat folder untuk drupal 
```
$ cd ndrupal
```
3. membuat file docker-compose.yml 
```
version: '3.3'

services:
  drupal:
    image: drupal:latest
    ports:
      - 9090:80
    volumes:
      - drupal_modules:/var/www/html/modules
      - drupal_profiles:/var/www/html/profiles
      - drupal_themes:/var/www/html/themes
      - drupal_sites:/var/www/html/sites
    restart: always

  postgres:
    image: postgres:10
    environment:
      POSTGRES_PASSWORD: 123456qq
    volumes:
        - db_data:/var/lib/postgresql/data
    restart: always

volumes:
  drupal_modules:
  drupal_profiles:
  drupal_themes:
  drupal_sites:
  db_data:
```
4. jalankan menggunakan docker compose up 
```
$ docker-compose up
Creating network "ndrupal_default" with the default driver
Creating volume "ndrupal_drupal_modules" with default driver
Creating volume "ndrupal_drupal_profiles" with default driver
Creating volume "ndrupal_drupal_themes" with default driver
Creating volume "ndrupal_drupal_sites" with default driver
Creating volume "ndrupal_db_data" with default driver
Pulling drupal (drupal:latest)...
latest: Pulling from library/drupal
d599a449871e: Pull complete
1a363f133ddd: Pull complete
dd6ffd5f60d7: Pull complete
515e48bcd87c: Pull complete
c6f3d43db193: Pull complete
f1c6f8e807f6: Pull complete
65d8fe3b5a08: Pull complete
2a46b5d1a618: Pull complete
80a23a71b657: Pull complete
ca8777914fba: Pull complete
d50334859dfc: Pull complete
e649e463bd1c: Pull complete
fbe597190285: Pull complete
ed0793760991: Pull complete
a4071a9a4e73: Pull complete
3a0c698e7383: Pull complete
Digest: sha256:add38184429bb4a089ae76eb6ea2bea4125c1c30813ce5e2a6b0ec25a846661a
Status: Downloaded newer image for drupal:latest
Pulling postgres (postgres:10)...
10: Pulling from library/postgres
804555ee0376: Pull complete
dc6ae8802d84: Pull complete
395ccdd34b05: Pull complete
a97aec38ba66: Pull complete
38ca37422b05: Pull complete
4f48902af5dd: Pull complete
f3aa2278d16c: Pull complete
babec8f73680: Pull complete
5786b6152d8c: Pull complete
930eb24af97d: Pull complete
62cb5d5e381f: Pull complete
ed354fd5634d: Pull complete
f3ee8456dd6c: Pull complete
04756c66ce5b: Pull complete
Digest: sha256:e77ca7cc0d744914ea5d0e5b214d4fdb04ba717dfab18659dcf148fe9640ab84
Status: Downloaded newer image for postgres:10
Creating ndrupal_drupal_1   ... done
Creating ndrupal_postgres_1 ... done
Attaching to ndrupal_postgres_1, ndrupal_drupal_1
postgres_1  | The files belonging to this database system will be owned by user "postgres".
postgres_1  | This user must also own the server process.
postgres_1  |
postgres_1  | The database cluster will be initialized with locale "en_US.utf8".
postgres_1  | The default database encoding has accordingly been set to "UTF8".
postgres_1  | The default text search configuration will be set to "english".
postgres_1  |
postgres_1  | Data page checksums are disabled.
postgres_1  |
postgres_1  | fixing permissions on existing directory /var/lib/postgresql/data ... ok
postgres_1  | creating subdirectories ... ok
postgres_1  | selecting default max_connections ... 100
postgres_1  | selecting default shared_buffers ... 128MB
postgres_1  | selecting default timezone ... Etc/UTC
postgres_1  | selecting dynamic shared memory implementation ... posix
postgres_1  | creating configuration files ... ok
postgres_1  | running bootstrap script ... ok
postgres_1  | performing post-bootstrap initialization ... ok
postgres_1  | syncing data to disk ... ok
postgres_1  |
postgres_1  | WARNING: enabling "trust" authentication for local connections
postgres_1  | You can change this by editing pg_hba.conf or using the option -A, or
postgres_1  | --auth-local and --auth-host, the next time you run initdb.
postgres_1  |
postgres_1  | Success. You can now start the database server using:
postgres_1  |
postgres_1  |     pg_ctl -D /var/lib/postgresql/data -l logfile start
postgres_1  |
postgres_1  | waiting for server to start....2019-12-29 07:43:19.868 UTC [43] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5432"
postgres_1  | 2019-12-29 07:43:19.990 UTC [44] LOG:  database system was shut down at 2019-12-29 07:43:18 UTC
postgres_1  | 2019-12-29 07:43:20.003 UTC [43] LOG:  database system is ready to accept connections
postgres_1  |  done
postgres_1  | server started
postgres_1  |
postgres_1  | /usr/local/bin/docker-entrypoint.sh: ignoring /docker-entrypoint-initdb.d/*
postgres_1  |
postgres_1  | 2019-12-29 07:43:20.116 UTC [43] LOG:  received fast shutdown request
postgres_1  | waiting for server to shut down....2019-12-29 07:43:20.142 UTC [43] LOG:  aborting any active transactions
postgres_1  | 2019-12-29 07:43:20.160 UTC [43] LOG:  worker process: logical replication launcher (PID 50) exited with exit code 1
postgres_1  | 2019-12-29 07:43:20.161 UTC [45] LOG:  shutting down
drupal_1    | AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 172.18.0.2. Set the 'ServerName' directive globally to suppress this message
postgres_1  | 2019-12-29 07:43:20.177 UTC [43] LOG:  database system is shut down
postgres_1  |  done
postgres_1  | server stopped
postgres_1  |
postgres_1  | PostgreSQL init process complete; ready for start up.
postgres_1  |
postgres_1  | 2019-12-29 07:43:20.257 UTC [1] LOG:  listening on IPv4 address "0.0.0.0", port 5432
postgres_1  | 2019-12-29 07:43:20.257 UTC [1] LOG:  listening on IPv6 address "::", port 5432
postgres_1  | 2019-12-29 07:43:20.272 UTC [1] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5432"
postgres_1  | 2019-12-29 07:43:20.340 UTC [52] LOG:  database system was shut down at 2019-12-29 07:43:20 UTC
drupal_1    | AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 172.18.0.2. Set the 'ServerName' directive globally to suppress this message
drupal_1    | [Sun Dec 29 07:43:20.639193 2019] [mpm_prefork:notice] [pid 1] AH00163: Apache/2.4.25 (Debian) PHP/7.3.13 configured -- resuming normal operations

```