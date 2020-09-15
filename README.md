Creates an Azure ARM environment.

Notes:

* The `location` input is optional. If it is omitted, then the value of
  the `azure_default_location` Cloudify secret is used.
* `template-file` may be a path to a file, or a publicly-available URL.
