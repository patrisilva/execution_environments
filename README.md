# execution_environments

Base image: `registry.redhat.io/ansible-automation-platform-26/ee-minimal-rhel9:latest` (requires Red Hat registry login).

## Build (Docker)

```bash
docker login registry.redhat.io
docker login quay.io/patrisilva

ansible-builder build \
  -f execution-environment.yml \
  -t quay.io/patrisilva/paloalto:aap26-r1 \
  -v 3 \
  --container-runtime docker \
  2>&1 | tee build.log
```

On Apple Silicon, target the same architecture as your AAP execution nodes (usually `linux/amd64`):

```bash
DOCKER_DEFAULT_PLATFORM=linux/amd64 ansible-builder build \
  -f execution-environment.yml \
  -t quay.io/patrisilva/paloalto:aap26-r1 \
  -v 3 \
  --container-runtime docker \
  2>&1 | tee build.log
```

## Verify (Docker)

```bash
docker run --rm quay.io/patrisilva/paloalto:aap26-r1 \
  python3 -c "import ssl; print(ssl.OPENSSL_VERSION)"

docker run --rm quay.io/patrisilva/paloalto:aap26-r1 \
  python3 -c "import cryptography, paramiko, netmiko; print('ok')"
```

## Push

```bash
docker login quay.io/patrisilva
docker push quay.io/patrisilva/paloalto:aap26-r1
```

> [!NOTE]
> When pulling the image in AAP, use the full image path including the tag (e.g. `quay.io/patrisilva/paloalto:aap26-r1`).

> [!NOTE]
> If your organization mirrors `ee-minimal-rhel9` on private Automation Hub, set that URL in `execution-environment.yml` under `images.base_image.name` before building.
