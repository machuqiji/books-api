![books-api-logo](https://user-images.githubusercontent.com/11173328/147469184-91048518-e48a-47d7-b8f5-01a478c33f46.png)

<p align="center">
  <a href="https://github.com/Project-Books/books-api/actions/workflows/build.yml">
    <img src="https://github.com/Project-Books/books-api/actions/workflows/build.yml/badge.svg" alt="Build Status" />
  </a>
	
  <a href="https://sonarcloud.io/dashboard?id=Project-Books_books-api">
    <img src="https://sonarcloud.io/api/project_badges/measure?project=Project-Books_books-api&metric=coverage" alt="Code coverage" />
  </a>
	
  <a href="https://join.slack.com/t/teambookproject/shared_invite/zt-punc8os7-Iz9PTCAkYcO_0S~XwtO5_A">
    <img src="https://img.shields.io/badge/slack-teambookproject-4A154B?logo=slack" alt="Slack" />
  </a>
</p>

GraphQL books API made using Spring Boot and [DGS](https://netflix.github.io/dgs/). This is a sibling project of the [Book Project](https://github.com/Project-Books/book-project).


## Setup

Prerequisites: 
- JDK 11 or higher
- Configure [Lombok](https://github.com/Project-Books/book-project/wiki/Troubleshooting#cannot-find-log-statements-or-the-entities-do-not-have-constructors-lombok-errors)
- PostgreSQL 12 or (better) Docker
  - For Linux users, install docker-compose 
  - For macOS and Windows users, install Docker Desktop

Recommended IntelliJ plugin: [JS GraphQL](https://plugins.jetbrains.com/plugin/8097-js-graphql)


## Before running the app

### Buildkit

As this Dockerfile caches the projects maven dependencies, please ensure docker buildkit is supported (Docker v18.09+) and is enabled.

Use the following command to see if the environment variable is set.

```bash
echo $DOCKER_BUILDKIT
``` 

If the result returns a blank string or an 0 please use the following command to set it:

```bash
export DOCKER_BUILDKIT=1
``` 

## Running the app

1. Import as a Maven project into your favourite IDE
2. Run the docker-compose file (if using macOS or Windows, you'll need to first ensure Docker Desktop is running)
   - build the image with default values
      - `docker-compose build booksapi` 
      - or with a custom mvn goal(s) `docker-compose build --build-arg mvn_arg="clean package -DskipTests" booksapi`
   - use `docker-compose up -d`
   - if you wish to view the output use `docker logs -f booksapi`
   - alternatively use `docker-compose up db booksapi` to launch the containers interactively
3. Go to `http://localhost:8082/graphiql`

Sample query:
```graphql
{
    findAllBooks {
        title
        isbn13
        yearOfPublication
        blurb
        publishers {
            name
        }
        isbn10
        authors {
            fullName
        }
        lang {
            name
        }
        genre {
            name
        }
        covers {
            pathToSmall
            pathToMedium
            pathToLarge
        }
        publishingFormat {
            formatName
        }
    }
}
```

### Access database

To access the PostgreSQL database when docker-compose/Docker desktop is running, use the follow credentials in your favourite client:

- Host: `localhost`
- Port: `5432`
- User: `dbuser`
- Password: `dbpassword`
- Database: books_api
- URL: `jdbc:postgresql://localhost:5432/books_api`

For example, in IntelliJ ultimate or DataGrip:

![image](https://user-images.githubusercontent.com/11173328/133380226-6e96a805-bf13-42e5-bcc2-0e39a1ab16a3.png)

## Contributing

If you wish to contribute (thanks!), please first see the [contributing document](https://github.com/Project-Books/books-api/blob/main/CONTRIBUTING.md).
