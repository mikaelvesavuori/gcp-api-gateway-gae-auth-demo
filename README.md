# Demo: GCP API Gateway fronting an App Engine app secured with Identity-Aware Proxy

This demo is based on the [official Google quickstart for API Gateway fronting an App Engine instance](https://cloud.google.com/api-gateway/docs/get-started-app-engine). Lovingly repurposed from Google with <3 for the benefit of all.

The example app is a Node-based web server (Fastify) that responds to the root `/` and `hello`. Hello will be used in the API specification (`api-spec.yaml`).

## Prerequisites

- You have a GCP account
- You are logged in through your environment
- You have set your variables as needed in `setup.sh`

## Instructions

- Run `deploy-app.sh` to deploy your basic demo application to App Engine
- Set `x-google-backend.address` in `api-spec.yaml` to your App Engine URL (looks similar to `https://{PROJECT_ID}.ew.r.appspot.com`)
- Refer to [https://cloud.google.com/iap/docs/app-engine-quickstart#enabling_iap](https://cloud.google.com/iap/docs/app-engine-quickstart#enabling_iap) for how to enable IAP. Copy the IAP client ID and set it in `x-google-backend.address.jwt_audience` in `api-spec.yaml`.
- Go to [IAP](https://console.cloud.google.com/security/iap) and set up your consent screen if it's not done above. You will most likely use the "External" option. Add a few users (like yourself) that should be granted access. Enable IAP for the App Engine web service.
- Run `setup.sh` to login, update your `gcloud` CLI tool and enable required APIs
- Visit the application URL. Any requests from an accepted user should go through and the rest should be blocked.

## References

- [Getting started with API Gateway and App Engine](https://cloud.google.com/api-gateway/docs/get-started-app-engine?hl=en_GB)
- [Quickstart: Manage access with Google Accounts](https://cloud.google.com/iap/docs/app-engine-quickstart#enabling_iap)
- [gcloud services](https://cloud.google.com/sdk/gcloud/reference/services)
- [Swagger / OpenAPI Specification version 2](https://swagger.io/docs/specification/2-0/basic-structure/)
