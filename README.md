# Shuffle Apps Collection

This repository contains various Shuffle apps for workflow automation and security operations.

## Apps Overview

| App | Version | Description | Actions |
|-----|---------|-------------|---------|
| AWS S3 | 1.0.0 | AWS S3 and MinIO storage operations | 10 actions |
| HTTP | 1.4.0 | HTTP client for web requests | 8 actions |
| Test App | 1.0.0 | Testing app for SDK features | 2 actions |

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
└── test-app/
    ├── Dockerfile
    ├── requirements.txt
    ├── api.yaml
    └── src/
        ├── app.py
        └── shuffle_sdk/
            └── __init__.py
```

## Requirements

- Docker for containerization
- Shuffle platform for deployment
- Python 3.x with shuffle_sdk

## Contributing

Feel free to add more Shuffle apps to this collection. Each app should follow the standard Shuffle app structure with:
- `Dockerfile` for containerization
- `api.yaml` for app definition
- `requirements.txt` for Python dependencies  
- `src/app.py` for main application logic