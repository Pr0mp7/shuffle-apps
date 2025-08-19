# Shuffle Apps Collection

This repository contains various Shuffle apps for workflow automation and security operations.

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

### Usage

1. Build the Docker image:
```bash
cd aws_s3
docker build -t your-registry.local:5000/shuffle/aws_s3:1.0.0 .
```

2. Push to your local registry:
```bash
docker push your-registry.local:5000/shuffle/aws_s3:1.0.0
```

3. Create a ZIP for Shuffle upload:
```bash
zip -r aws_s3.zip . -x "*.git*"
```

4. Upload to Shuffle via UI or API

### MinIO Support

This app supports MinIO by using the `endpoint_url` parameter. For MinIO in Kubernetes, use:
- endpoint_url: `http://minio.minio-namespace.svc.cluster.local:9000`
- region: `us-east-1` (standard for MinIO)

### Directory Structure

```
aws_s3/
├── Dockerfile
├── requirements.txt
├── api.yaml
└── src/
    └── app.py
```