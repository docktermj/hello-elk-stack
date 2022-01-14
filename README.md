# hello-elk-stack

## Synopsis

An ELK Stack (ElasticSearch, LogStash, Kibana) with mock log generators.

## Clone repository

1. :pencil2: Locate git repository.
   Example:

    ```console
    export GIT_ACCOUNT=docktermj
    export GIT_REPOSITORY=hello-elk-stack
    export GIT_ACCOUNT_DIR=~/${GIT_ACCOUNT}.git
    export GIT_REPOSITORY_DIR="${GIT_ACCOUNT_DIR}/${GIT_REPOSITORY}"
    ```

### Determine URL of git repository

:thinking: Git repositories can be cloned via SSH or HTTPS.
For anonymous access, use HTTPS.
Perform one of the following commands to set `GIT_REPOSITORY_URL`.

#### URL for HTTPS

1. Use this example for anonymous access.

    ```console
    export GIT_REPOSITORY_URL="https://github.com/${GIT_ACCOUNT}/${GIT_REPOSITORY}.git"
    ```

#### URL for SSH

1. Use this example to log in with GitHub credentials.

    ```console
    export GIT_REPOSITORY_URL="git@github.com:${GIT_ACCOUNT}/${GIT_REPOSITORY}.git"
    ```

### Perform clone repository

1. :thinking: Create parent directories.
   Choose one method.
    1. Linux.
       Example:

        ```console
        mkdir --parents ${GIT_ACCOUNT_DIR}
        ```

    1. macOS.
       Example:

        ```console
        mkdir -p ${GIT_ACCOUNT_DIR}
        ```

1. Get repository.
   Example:

    ```console
    cd  ${GIT_ACCOUNT_DIR}
    git clone  --recurse-submodules ${GIT_REPOSITORY_URL}
    ```

## Demonstrate using docker-compose

1. Run command.
   Example:

    ```console
    cd ${GIT_REPOSITORY_DIR}
    docker-compose up
    ```

## Test

### Logstash

1. Test if messages are in logstash using
   [Node Stats API](https://www.elastic.co/guide/en/logstash/current/node-stats-api.html).

    ```console
    curl -X GET 'localhost:9600/_node/stats/events?pretty'
    ```

   Look at the `events.in` and `events.out` numbers.

### Elasticsearch

1. Test if messages are in elasticsearch using
   [cat indices API](https://www.elastic.co/guide/en/elasticsearch/reference/current/cat-indices.html).

    ```console
    curl -X GET localhost:9200/_cat/indices?v=true
    ```

    View `docs.count` column.

### Kibana

1. Test if messages are in Kibana using
   [Index Management](http://localhost:5601/app/management/data/index_management/indices).

    - View "Docs count" column.
