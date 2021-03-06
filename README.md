# quickbooks-python
-------------------

A really simple, brute-force, Python class for accessing the Quickbooks API. 

Made much simpler with some major contributions from @HaPsantran. See HaPsantran's branch [here](https://github.com/HaPsantran/quickbooks-python). It's probably a much more reliable spot for keeping this up to date and evolving. I've cleaned the script up a bit for a semi-clean v0.1.0.

As HaPsantran says in their ReadMe:

>Generally when using this module (or any of the QBO v3 API wrappers out there), keep in mind that there are some glaring omissions in it's functionality that (AFAIK) no one is able to get around programmatically. For example, you can't access (or create, update, or delete, obvi) Deposits or Transfers.

## Running the script

Works like any Python script, but you'll need [rauth](http://rauth.readthedocs.org/en/latest/) for it to work. 

## Accessing the API

Once you've gotten a hold of your QuickBooks access tokens, you can create a QB object:

    qb = QuickBooks(consumer_key = QB_OAUTH_CONSUMER_KEY, 
            consumer_secret = QB_OAUTH_CONSUMER_SECRET,
            access_token = QB_ACCESS_TOKEN, 
            access_token_secret = QB_ACCESS_TOKEN_SECRET,
            company_id = QB_REALM_ID
            )

__Note:__ the functionality for connecting to the QB API is here as well, I've just not written up proper documentation yet. Have a look at the `get_authorize_url()`, `get_access_tokens()`, and `create_session` methods.


### New in v0.1.0

* Well, versioning :)
* Removed a lot of extraneous method calls that have essentially been replaced with query_object().

## Available methods

__Note:__ This is a work-in-progress. It was made public to help other developers access the QuickBooks API, it's not a guarantee that it will ever be finished.

you can access any object via the query_object method.

    qb.query_objects(business_object, params, query_tail)

The available business objects are:

    "Account","Attachable","Bill","BillPayment",
    "Class","CompanyInfo","CreditMemo","Customer",
    "Department","Employee","Estimate","Invoice",
    "Item","JournalEntry","Payment","PaymentMethod",
    "Preferences","Purchase","PurchaseOrder",
    "SalesReceipt","TaxCode","TaxRate","Term",
    "TimeActivity","Vendor","VendorCredit"

Example:

    qb.query_objects("Bill")
    > [{u'DocNumber': ... }]

## From HaPsantran's README
------------------

Update: As I try using the pnl function in report.py, I notice that not all of the activity is making it in. I have to assume it basically doesn't work then. Rather than rebuild it, though, I'm probably going to use other tools outside the  module to massage the ledger_lines I get out of massage.py (rather than build special reporting tools within the quickbooks package).

Intuit has promised reporting features, but who knows...

http://stackoverflow.com/questions/19455750/quickbooks-online-api-financial-data
