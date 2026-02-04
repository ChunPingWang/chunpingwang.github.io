---
layout: post
title: "Setting Up Harbor Container Registry with Self-Signed Certificates"
date: 2026-02-04 12:00:00 +0800
categories: [devops, containers]
tags: [harbor, docker, registry, kubernetes, certificates]
---

Harbor is an open-source container image registry that provides essential features like security scanning, image signing, and role-based access control. In this post, I'll share my notes on setting up Harbor with self-signed certificates.

## Why Harbor?

When working with Kubernetes in development or air-gapped environments, you need a private container registry. Harbor offers:

- **Security scanning** for vulnerabilities
- **Image replication** across registries
- **Role-based access control**
- **Audit logging**
- **Helm chart repository**

## Generating Self-Signed Certificates

First, create SSL certificates for Harbor:

```bash
# Generate CA certificate
openssl genrsa -out ca.key 4096
openssl req -x509 -new -nodes -sha512 -days 3650 \
  -subj "/CN=harbor-ca" \
  -key ca.key \
  -out ca.crt

# Generate server certificate
openssl genrsa -out harbor.key 4096
openssl req -sha512 -new \
  -subj "/CN=harbor.example.com" \
  -key harbor.key \
  -out harbor.csr

# Sign the certificate
openssl x509 -req -sha512 -days 3650 \
  -CA ca.crt -CAkey ca.key -CAcreateserial \
  -in harbor.csr \
  -out harbor.crt
```

## Configuring Docker to Trust the Certificate

### On Linux

```bash
sudo mkdir -p /etc/docker/certs.d/harbor.example.com
sudo cp ca.crt /etc/docker/certs.d/harbor.example.com/
sudo systemctl restart docker
```

### On macOS

```bash
sudo security add-trusted-cert -d -r trustRoot \
  -k /Library/Keychains/System.keychain ca.crt
# Restart Docker Desktop
```

### In Minikube

```bash
minikube start --insecure-registry="harbor.example.com"
# Or copy certificates to minikube
minikube cp ca.crt /etc/docker/certs.d/harbor.example.com/ca.crt
```

## Installing Harbor

1. Download from [Harbor releases](https://github.com/goharbor/harbor/releases)
2. Extract and configure `harbor.yml`:

```yaml
hostname: harbor.example.com
https:
  port: 443
  certificate: /path/to/harbor.crt
  private_key: /path/to/harbor.key
harbor_admin_password: YourSecurePassword
```

3. Run the installer:

```bash
./install.sh --with-trivy
```

## Learn More

Check out my detailed notes: [harbor-install-note](https://github.com/ChunPingWang/harbor-install-note)

Harbor is essential for any serious Kubernetes deployment. Take the time to set it up properly!
