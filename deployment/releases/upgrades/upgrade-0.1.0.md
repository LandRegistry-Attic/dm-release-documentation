## Upgrade to version 0.1.0

* Deploy dm-borrower-frontend.
* Deploy dm-deed-api.
* Deploy dm-esec-client


* New app.routes:

Deed-API
```
    /deed/<deed_reference>/                         GET
    /deed/                                          POST
    /deed/borrowers/delete/<borrower_id>            DELETE
```

Borrower-Frontend
```
    /                                               GET
    /identity-verified                              GET
    /searchdeed/                                    GET
    /searchdeed/enter-dob                           GET
    /searchdeed/search/                             POST
```

DM-Esec-Client
```
    /esec/add_borrower_signature/<borrower_pos>     GET
    /esec/sign_document_with_authority              POST
```
