# execution_environments
# Build:
```bash
ansible-builder build -t quay.io/patrisilva/paloalto:nov25-custom -v 3 --container-runtime docker 2>&1 | tee build.log
```
# Login:
```bash
docker login quay.io/patrisilva
```
# Push:
```bash
docker push quay.io/patrisilva/paloalto:nov25-custom
```
> [!NOTE]
> When pulling the image, make sure to include the tag.