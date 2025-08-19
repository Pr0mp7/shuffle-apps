# Shuffle Apps Collection

This repository contains various Shuffle apps for workflow automation and security operations.

## Apps Overview

| App | Version | Description | Actions |
|-----|---------|-------------|---------|
| AWS S3 | 1.0.0 | AWS S3 and MinIO storage operations | 10 actions |
| HTTP | 1.4.0 | HTTP client for web requests | 8 actions |
| Test App | 1.0.0 | Testing app for SDK features | 2 actions |

### HTTP App Version History

| Version | Status | Changes |
|---------|--------|---------|
| 1.0.0 | Legacy | Initial HTTP client implementation |
| 1.1.0 | Legacy | Enhanced HTTP functionality |
| 1.2.0 | Legacy | Improved header handling |
| 1.3.0 | Legacy | Additional HTTP methods |
| 1.4.0 | Current | Complete REST API support |

## AWS S3 App

A comprehensive AWS S3 and MinIO compatible storage operations app for Shuffle.

### Features

- List all S3 buckets
- Create new S3 buckets
- Upload files to S3 buckets
- Download files from S3 buckets
- Delete files from S3 buckets
- Block IP access to buckets (AWS only)
- Get bucket logging configuration
- Get bucket policy status
- Get bucket replication configuration
- Get bucket request payment configuration

### MinIO Support

This app supports MinIO by using the `endpoint_url` parameter. For MinIO in Kubernetes, use:
- endpoint_url: `http://minio.minio-namespace.svc.cluster.local:9000`
- region: `us-east-1` (standard for MinIO)

## HTTP App

HTTP client app for making web requests and API calls.

### Features

- GET requests
- POST requests  
- PUT requests
- PATCH requests
- DELETE requests
- HEAD requests
- OPTIONS requests
- Custom curl command execution

### Parameters

All HTTP methods support:
- Custom headers
- Authentication (username/password)
- SSL certificate verification
- HTTP/HTTPS proxy support
- Request timeout configuration
- Response to file conversion

## Test App

Simple testing app using App SDK 0.0.25 for development and testing purposes.

### Features

- Hello world test function
- Execution isolation testing
- Datastore functionality testing

## Installation & Usage

### Build and Deploy

1. Build the Docker image for any app:
```bash
cd [app-name]
docker build -t your-registry.local:5000/shuffle/[app-name]:1.0.0 .
```

2. Push to your local registry:
```bash
docker push your-registry.local:5000/shuffle/[app-name]:1.0.0
```

3. Create a ZIP for Shuffle upload:
```bash
zip -r [app-name].zip . -x "*.git*"
```

4. Upload to Shuffle via UI or API

## Deployment Configuration Files

This repository also includes deployment and configuration files for Shuffle infrastructure:

### Included Configuration Files

- `pull_and_save_shuffle_images.sh` - Script to download and save Shuffle 2.0.0 Docker images for offline deployment
- `shuffle-values.yaml` - Helm values configuration for Shuffle deployment with Kubernetes
- `ingress-nginx.yaml` - Nginx ingress configuration
- `iris-values.yaml` - IRIS system configuration values
- `longhorn-ingress.yaml` - Longhorn storage ingress configuration  
- `longhorn-values.yaml` - Longhorn storage system values
- `longhron-ingress.yaml` - Additional Longhorn ingress config

### Deployment Features

- **Offline Deployment Ready**: Includes script to download all required Docker images
- **Kubernetes Native**: Configured for Kubernetes deployment with proper resource management
- **Storage Integration**: Longhorn distributed storage configuration
- **Ingress Management**: Complete ingress setup for web access
- **High Availability**: Production-ready configuration with proper scaling

### Directory Structure

```
shuffle-apps/
├── README.md
├── aws_s3/
│   ├── Dockerfile
│   ├── requirements.txt
│   ├── api.yaml
│   └── src/
│       └── app.py
├── http/
│   ├── Dockerfile
│   ├── requirements.txt
│   ├── api.yaml
│   └── src/
│       └── app.py
├── test-app/
│   ├── Dockerfile
│   ├── requirements.txt
│   ├── api.yaml
│   └── src/
│       ├── app.py
│       └── shuffle_sdk/
│           └── __init__.py
├── http-versions/
│   ├── 1.0.0/
│   ├── 1.1.0/
│   ├── 1.2.0/
│   └── 1.3.0/
└── deployment-configs/
    ├── pull_and_save_shuffle_images.sh
    ├── shuffle-values.yaml
    ├── ingress-nginx.yaml
    ├── iris-values.yaml
    ├── longhorn-ingress.yaml
    ├── longhorn-values.yaml
    └── longhron-ingress.yaml
```

## Requirements

- Docker for containerization
- Shuffle platform for deployment
- Python 3.x with shuffle_sdk

## Deployment Quick Start

### For Air-Gapped Environments

1. Run the image download script:
```bash
cd deployment-configs
./pull_and_save_shuffle_images.sh
```

2. Transfer the generated `shuffle-2.0.0-complete.tar.gz` to your target environment

3. Load images in target environment:
```bash
tar -xzf shuffle-2.0.0-complete.tar.gz
for image in shuffle-2.0.0-export/*.tar; do docker load -i $image; done
```

4. Deploy using Helm:
```bash
helm install shuffle -f deployment-configs/shuffle-values.yaml shuffle/shuffle
```

### For Kubernetes Deployment

The included configurations support:
- **Shuffle 2.0.0+** with all components
- **OpenSearch** for data storage and analytics
- **Longhorn** distributed storage
- **Nginx Ingress** for web access
- **Production scaling** with proper resource limits

## Contributing

Feel free to add more Shuffle apps to this collection. Each app should follow the standard Shuffle app structure with:
- `Dockerfile` for containerization
- `api.yaml` for app definition
- `requirements.txt` for Python dependencies  
- `src/app.py` for main application logic

### Version Management

When adding new versions:
1. Place them in `http-versions/` for version history
2. Update the current version in the main app directory
3. Document changes in the version history table