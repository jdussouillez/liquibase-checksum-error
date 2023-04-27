# liquibase-checksum-error

Projet to reproduce a bug in Liquibase v4.21+.

- https://github.com/liquibase/liquibase/issues/4168
- https://forum.liquibase.org/t/liquibase-4-21-x-introduces-changeset-validation-error/8081/

## How to reproduce

- Setup a local PostgreSQL database (`localhost:5432/test`, user `postgre`, password `mypassword`)
- Run `./mvnw liquibase:update` (using Liquibase v4.20.0) -> changesets are applied with success
- Run `./mvnw liquibase:update` -> "Database is up to date, no changesets to execute"
- Change the Liquibase version to 4.21.1
- Run `./mvnw liquibase:update` -> error

Maven error:

```
Starting Liquibase at 16:04:30 (version 4.21.1 #9070 built at 2023-04-13 20:56+0000)
[INFO] Set default schema name to public
[INFO] Executing on Database: jdbc:postgresql://localhost:5432/test
[INFO] Successfully acquired change log lock
[INFO] Reading from databasechangelog
[INFO] Change failed validation!
[INFO] Successfully released change log lock
[INFO] Command execution complete
[INFO] Command execution complete
[INFO] ------------------------------------------------------------------------
[INFO] BUILD FAILURE
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  1.489 s
[INFO] Finished at: 2023-04-27T16:04:31+02:00
[INFO] ------------------------------------------------------------------------
[ERROR] Failed to execute goal org.liquibase:liquibase-maven-plugin:4.21.1:update (default-cli) on project liquibase-checksum-error: 
[ERROR] Error setting up or running Liquibase:
[ERROR] liquibase.exception.ValidationFailedException: Validation Failed:
[ERROR]      1 changesets check sum
[ERROR]           changelogs/2023-04-27_init.xml::init:procedure::JR was: 8:e350d4815158265f13ef42a2b920c97a but is now: 8:bcb966fbe934329da77f2c259a3f8adf
[ERROR] 
[ERROR] -> [Help 1]
[ERROR] 
```
