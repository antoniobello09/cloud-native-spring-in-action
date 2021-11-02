# Catalog Service

## REST API

| Endpoint	      | Method   | Req. body  | Status | Resp. body     | Description    		   	     |
|:---------------:|:--------:|:----------:|:------:|:--------------:|:-------------------------------|
| `/books`        | `GET`    |            | 200    | Book[]         | Get all the books in the catalog. |
| `/books`        | `POST`   | Book       | 201    | Book           | Add a new book to the catalog. |
|                 |          |            | 422    |                | A book with the same ISBN already exists. |
| `/books/{isbn}` | `GET`    |            | 200    | Book           | Get the book with the given ISBN. |
|                 |          |            | 404    |                | No book with the given ISBN exists. |
| `/books/{isbn}` | `PUT`    | Book       | 200    | Book           | Update the book with the given ISBN. |
|                 |          |            | 201    | Book           | Create a book with the given ISBN. |
| `/books/{isbn}` | `DELETE` |            | 204    |                | Delete the book with the given ISBN. |
|                 |          |            | 404    |                | No book with the given ISBN exists. |

## Useful Commands

| Gradle Command	         | Description                                   |
|:---------------------------|:----------------------------------------------|
| `./gradlew bootRun`        | Run the application.                          |
| `./gradlew build`          | Build the application.                        |
| `./gradlew test`           | Run tests.                                    |
| `./gradlew bootJar`        | Package the application as a JAR.             |
| `./gradlew bootBuildImage` | Package the application as a container image. |

After building the application, you can also run it from the Java CLI:

```bash
java -jar build/libs/catalog-service-0.0.1-SNAPSHOT.jar
```

## Running a PostgreSQL Database

Run PostgreSQL as a Docker container

```bash
docker run --name polar-postgres-catalog \
    -e POSTGRES_USER=user \
    -e POSTGRES_PASSWORD=password \
    -e POSTGRES_DB=polardb_catalog \
    -p 5432:5432 \
    -d postgres:13.4
```

### Container Commands

| Docker Command	              | Description       |
|:-------------------------------:|:-----------------:|
| `docker stop polar-postgres-catalog`   | Stop container.   |
| `docker start polar-postgres-catalog`  | Start container.  |
| `docker remove polar-postgres-catalog` | Remove container. |

### Database Commands

Start an interactive PSQL console:

```bash
docker exec -it polar-postgres-catalog psql -U user -d polardb_catalog
```

| PSQL Command	             | Description                    |
|:--------------------------:|:------------------------------:|
| `\list`                    | List all databases.            |
| `\connect polardb_catalog` | Connect to specific database.  |
| `\dt`                      | List all tables.               |
| `\quit`                    | Quit interactive psql console. |