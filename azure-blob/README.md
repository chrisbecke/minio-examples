# Minio Azure

Demonstrates deploying Minio to Azure ACI using Docker as a gateway in front of Azure Blob storage.

Prerequsites:

* You have an Azure account with a configured docker context.
* You have created an Azure Storage account.

## Quickstart

Create `.env` with the following contents

```ini
AZURE_STORAGE_ACCOUNT=your-storage-account-name
AZURE_STORAGE_KEY=your-storage-account-key-base64
```

Then run the following to deploy the compose to your azure context, and access the minio instance ip address.

```bash
docker context use my-azure
docker compose up
docker ps
```
