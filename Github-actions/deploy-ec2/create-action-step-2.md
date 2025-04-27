# Configuração de GitHub Actions para Deploy em EC2

## Exemplo de Workflow (`.github/workflows/deploy.yml`)

```yaml
name: Deploy API no EC2

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout código
        uses: actions/checkout@v3

      - name: Build imagem Docker
        run: |
          docker build -t SEU_USUARIO_DOCKERHUB/seu-app:latest .
          echo "${{ secrets.DOCKER_PASSWORD }}" | docker login -u "${{ secrets.DOCKER_USERNAME }}" --password-stdin
          docker push SEU_USUARIO_DOCKERHUB/seu-app:latest

  deploy:
    needs: build
    runs-on: self-hosted
    steps:
      - name: Pull nova imagem Docker
        run: docker pull SEU_USUARIO_DOCKERHUB/seu-app:latest

      - name: Remover container antigo
        run: docker rm -f seu-app || true

      - name: Rodar novo container
        run: |
          docker run -d \
            --name seu-app \
            -p 8080:8080 \
            -e DATABASE_URL=${{ secrets.DATABASE_URL }} \
            -e DATABASE_USERNAME=${{ secrets.DATABASE_USERNAME }} \
            -e DATABASE_PASSWORD='${{ secrets.DATABASE_PASSWORD }}' \
            SEU_USUARIO_DOCKERHUB/seu-app:latest
```

