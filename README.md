# umd-fcrepo-docker

Docker images for the Fedora (fcrepo) applications.

## External Requirements

* [umd-fcrepo-webapp] Docker image

## Quick Start

```bash
git clone git@github.com:umd-lib/umd-fcrepo-docker.git
cd umd-fcrepo-docker
```

Build images:

```bash
docker build -t docker.lib.umd.edu/fcrepo-postgres postgres
docker build -t docker.lib.umd.edu/fcrepo-activemq activemq
docker build -t docker.lib.umd.edu/fcrepo-solr-fedora4 solr-fedora4
docker build -t docker.lib.umd.edu/fcrepo-fuseki fuseki
```

Export environment variables (for the repository container):

```bash
export MODESHAPE_DB_PASSWORD=...  # default in the umd-fcrepo-docker stack is "fcrepo"
export LDAP_BIND_PASSWORD=...     # see the SSDR "Identities" document for this
export JWT_SECRET=...             # can be anything, but must be sufficiently long
                                  # one method to generate a random secret is:
                                  #   uuidgen | shasum -a256 | cut -d' ' -f1
```

Deploy the stack:

```bash
docker stack deploy --with-registry-auth -c umd-fcrepo.yml umd-fcrepo
```

### Application URLs

* ActiveMQ admin console: <http://localhost:8161/admin>
* Solr admin console: <http://localhost:8983/solr/#/>
* Fuseki admin console: <http://localhost:3030/>
* Fedora repository REST API: <http://localhost:8080/rest/>
* Fedora repository login/user profile page: <http://localhost:8080/user/>

## Individual Images

Each of the images may also be built and run individually. See the README
files for each image for more information:

* [PostgreSQL](postgres/README.md)
* [ActiveMQ](activemq/README.md)
* [Solr (fedora4 Core)](solr-fedora4/README.md)
* [Fuseki](fuseki/README.md)

[umd-fcrepo-webapp]: https://github.com/umd-lib/umd-fcrepo-webapp