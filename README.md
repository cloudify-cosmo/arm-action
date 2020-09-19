Creates an Azure ARM environment.

# Prerequisites

The Cloudify ARM Integration blueprint must be uploaded to Cloudify Manager, with the ID
`cloudify-azure-arm-1.0`.

## Environment Variables

This Action uses the Cloudify Profile environment variables described in the official
Cloudify documentation (see [More Information](#more-information) below).

In addition, the following environment variables are used, containing the authentication data
for Azure:

* `AZURE_SUBSCRIPTION_ID`
* `AZURE_TENANT_ID`
* `AZURE_CLIENT_ID`
* `AZURE_CLIENT_SECRET`

# Inputs

(Certain commonly-used inputs are documented in our official website; see [More Information](#more-information) below)

| Name | Description
|------|------------
| `resource-group` | Name of resource group to create
| `template-file` | URL/path to template file
| `parameters-file` | YAML/JSON file containing template parameters
| `location` | Azure location to create resource group in
| `outputs-file` | Path to JSON file to receive the Cloudify environment's outputs and capabilities

# Notes

* The `location` input is optional. If omitted, then the value of the `azure_default_location` Cloudify secret is used.
* If `template-file` is a URL, it must be reachable by Cloudify Manager.

# More Information

Refer to [Cloudify CI/CD Integration](https://docs.cloudify.co/latest/working_with/integration/) for additional information about
Cloudify's integration with CI/CD tools.
