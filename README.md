Creates an Azure ARM environment.

# Environment Variables

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

## Notes

* The `location` input is optional. If omitted, then the value of the `azure_default_location` Cloudify secret is used.
* If `template-file` is a URL, it must be reachable by Cloudify Manager.

# Example

```yaml
jobs:
  test_job:
    env:
      AZURE_SUBSCRIPTION_ID: ${{ secrets.AZURE_SUBSCRIPTION_ID }}
      AZURE_TENANT_ID: ${{ secrets.AZURE_TENANT_ID }}
      AZURE_CLIENT_ID: ${{ secrets. AZURE_CLIENT_ID }}
      AZURE_CLIENT_SECRET: ${{ secrets.AZURE_CLIENT_SECRET }}
    steps:
      - name: Checkout code
        uses: actions/checkout@v2
      - name: Create environment
        uses: cloudify-cosmo/arm-action@v1.0
        with:
          environment-name: "test-arm-$GITHUB_RUN_ID"
          resource-group: "githubarmrg$GITHUB_RUN_ID"
          location: centralus
          template-file: arm/environment.json
          parameters-file: arm/test-params/integration.yaml
          outputs-file: env-data.json
```

Note how the Azure credentials are set as environment variables, with the values being taken
from GitHub secrets.

The template file and parameters file are both taken from the repository that was checked out
during the "Checkout code" step.

# More Information

Refer to [Cloudify CI/CD Integration](https://docs.cloudify.co/latest/working_with/integration/) for additional information about
Cloudify's integration with CI/CD tools.
