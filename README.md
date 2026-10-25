# Google Cloud Setup

This demo uses terraform to manage gcp resource.

## Initial Setup

1. Create an account with your Google email address.
2. Create a [Google Cloud project](https://console.cloud.google.com/) if you don't already have one. For example, name it `Terraform Demo` and note its **Project ID**; you'll need it when deploying infrastructure with Terraform.
3. Set up a [service account and authentication](https://docs.cloud.google.com/docs/authentication/use-service-account-impersonation) for the project. Grant it the `Viewer` role to start, then download its service-account JSON key if you plan to authenticate with that key.
4. Install the [Google Cloud SDK](https://cloud.google.com/sdk/docs/quickstart).
5. To authenticate with the downloaded key, set `GOOGLE_APPLICATION_CREDENTIALS` to its path:

   ```sh
   export GOOGLE_APPLICATION_CREDENTIALS="<path/to/your/service-account-authkeys>.json"
   ```

## Terraform Execution

Terraform was used to create a Google Cloud Storage bucket and destroy it after the demo. Authenticate with Application Default Credentials, initialize Terraform, and review the planned changes:

```sh
terraform init
terraform plan -var="project=<your-gcp-project-id>"
```

Create the bucket and other resources defined in the Terraform configuration:

```sh
terraform apply -var="project=<your-gcp-project-id>"
```

When finished, destroy the resources to avoid ongoing charges:

```sh
terraform destroy
```

   Alternatively, use Application Default Credentials for local development:

   ```sh
   gcloud auth application-default login
   ```

   Keep service-account keys private and never commit them to the repository.

## Setup for Access

1. Add the following [IAM roles](https://cloud.google.com/storage/docs/access-control/iam-roles) to the service account:
   - `Storage Admin`
   - `Storage Object Admin`
   - `BigQuery Admin`


2. Enable these APIs for the project:
   - [Identity and Access Management (IAM) API](https://console.cloud.google.com/apis/library/iam.googleapis.com)
   - [IAM Service Account Credentials API](https://console.cloud.google.com/apis/library/iamcredentials.googleapis.com)
3. Ensure `GOOGLE_APPLICATION_CREDENTIALS` is set when using the service-account key:

   ```sh
   export GOOGLE_APPLICATION_CREDENTIALS="<path/to/your/service-account-authkeys>.json"
   ```