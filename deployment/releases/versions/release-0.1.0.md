## Release 0.1.0 (2016-01-28)

### Application versions:

    dm-deed-api:                            0.1.0
    dm-borrower-frontend                    0.1.0
    dm-esec-client                          0.1.0

### Environment variables

#### dm-deed-api

    SETTINGS                    - environment identifier (dev/prod/...)
    DEBUG                       - debug indicator
    DEED_DATABASE_URI           - name of the deed database to connect to (deed_api)

#### dm-borrower-frontend

    DEED_API_ADDRESS            - location of deed_api service

#### dm-esec-client

    DEBUG                       - debug indicator
    ESEC_LIVE                   - production indicator
    ESEC_HOST                   - location of eSecurity
    ESEC_REQUEST_ID             - user credentials accessing eSecurity
    ESEC_ORGANISATION           - organisation the user belongs to  
    ESEC_ORGANISATIONAL_UNIT    - the unit with the organisation the user belongs to
    ESEC_LOCATION               - Locale details
    ESEC_ROLES                  - account type that created users will be created as
    ESEC_USER_PASSWORD_PREFIX   -
    ESEC_INTEGRATION            - service endpoint description switch (different WSDL loaded)


### Databases

    deed_api                    - version_num in alembic_version table should be 2ef609ed309
