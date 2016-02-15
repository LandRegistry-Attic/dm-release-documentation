## Release 0.1.3 (2016-02-12)

### Application versions:

    dm-deed-api:                            0.1.3

### Environment variables

    The following environment variable should be set on the external test environments.

    WEBSEAL_AUTHENTICATION      - determines if Webseal_authentication is turned on
                                  Default True. Only set to false on the public test environment
#### dm-deed-api

    SETTINGS                    - environment identifier (dev/prod/...)
    DEBUG                       - debug indicator
    DEED_DATABASE_URI           - name of the deed database to connect to (deed_api)

### Databases

    deed_api                    - version_num in alembic_version table should be 2ef609ed309
