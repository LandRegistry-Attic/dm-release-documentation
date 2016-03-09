## Release 0.1.4 (2016-02-12)

### Application versions:

    dm-deed-api:                            0.1.4
    dm-borrower-frontend                    0.1.4

### Environment variables

    The following environment variable should be set on the external test environments.

    ACCOUNT_SID                 - Account Sign-on ID for Twillio 
                                  
    AUTH_TOKEN                  - Twillio 2 factor authentication token to allow API calls
    
    TWILIO_PHONE_NUMBER         - Contact number the 2 factor text will be sent from
   
#### dm-deed-api

    SETTINGS                    - environment identifier (dev/prod/...)
    DEBUG                       - debug indicator
    DEED_DATABASE_URI           - name of the deed database to connect to (deed_api)

### Databases

    deed_api                    - version_num in alembic_version table should be 384b88178a6
