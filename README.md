# SAMPLE DOCKER SETTINGS FOR .NET CORE WITH POSTGRESQL

This is an example project demonstrating the use of docker to run a .NET Core Web API with Postgresql
The Base TodoApi Sample Project was cloned from https://github.com/laxmansahni/TodoApi/

Settings was referenced from:

1. https://docs.microsoft.com/en-us/dotnet/core/docker/docker-basics-dotnet-core
2. https://docs.docker.com/develop/develop-images/dockerfile_best-practices/
3. https://github.com/rajvirtual/docker-aspnetcore-postgresql

## NOTES ON DOT NET DB MIGRATION

Ideally you want to run your migrations by yourself but i have modified the code in the base Todoapi project so that migrations are executed
at run time. The ugly copy and paste class can be found in `TodoApi/Startup.cs` called DataSeeder class. It is called in line 51 `app.SeedData();`.

## ACCESSING THE INDIVIDUAL CONTAINERS

You can ssh into individual containers to test commands while building build steps for dockerfiles,
Below are a list of docker commands you can use for your everyday docker tasks.

| Task                                                     | Command                                   | Notes                                                                          |
| -------------------------------------------------------- | ----------------------------------------- | ------------------------------------------------------------------------------ |
| show all containers                                      | `docker ps -a`                            | -                                                                              |
| ssh into container                                       | `docker exec -it <containerid/name>` bash | Use `winpty docker exec it <containerid/name> bash` if you are on windows bash |
| Builds docker image and removes it if faulty image build | `docker build -t --rm test-container .`   | Run at the same directory where the Dockerfile resides                         |
| stops a container                                        | `docker stop <containerid/name>`          | -                                                                              |
| run a stopped container                                  | `docker run <containerid/name>`           | -                                                                              |
| removes a stopped container                              | `docker rm <containerid/name>`            | -                                                                              |
| shows all available images                               | `docker images`                           | -                                                                              |
| removes an available image                               | `docker image rm <imageid/name>`          | -                                                                              |

## HOW TO RUN

1. `docker-compose up`.
2. You can test if the application works by visiting `http://localhost:7000/api/values` or `http://localhost:7000/api/todo`.
3. To stop, `ctrl`+`c` and run `docker-compose down` to ensure containers shut down properly.

## NOTES ON `docker-compose up`

- If you run docker-compose up , it will re-use an available built image if it exists, otherwise it will build it.
- If your code changes or docker file changes are not picked up by docker-compose, you may need to remove the image manually and build it manually.
