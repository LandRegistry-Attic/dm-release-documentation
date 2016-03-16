## Release 0.1.4 (2016-02-12)

### Application versions:

    dm-deed-api:                            0.1.4
    dm-borrower-frontend                    0.1.3
    dm-esec-client                          0.1.3

### Environment variables

    The following environment variable should be set on the external test environments.

#### dm-deed-api

    ** NEW **
    AKUMA_BASE_HOST             - location of Akuma
    ESEC_CLIENT_URI             - location of dm-esec-client
    ACCOUNT_SID                 - Account Sign-on ID for Twillio
    AUTH_TOKEN                  - Twillio 2 factor authentication token to allow API calls
    TWILIO_PHONE_NUMBER         - Contact number the 2 factor text will be sent from

### Databases

    deed_api                    - version_num in alembic_version table should be 33280da2569
