# Configuração de GitHub Actions para Build Java + Testes + SonarQube

## Exemplo de Workflow (`.github/workflows/build-java-sonar.yml`)

```yaml
name: Build Java 17 + Testes + SonarQube

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  build:
    name: Build e Teste
    runs-on: ubuntu-latest

    steps:
      - name: Checkout código
        uses: actions/checkout@v3

      - name: Set up Java 17
        uses: actions/setup-java@v3
        with:
          distribution: 'temurin'
          java-version: '17'

      - name: Build com Maven
        run: mvn clean install --batch-mode --update-snapshots

      - name: Executar Testes
        run: mvn test

  sonar:
    name: Análise SonarQube
    runs-on: ubuntu-latest
    needs: build

    steps:
      - name: Checkout código
        uses: actions/checkout@v3

      - name: Set up Java 17
        uses: actions/setup-java@v3
        with:
          distribution: 'temurin'
          java-version: '17'

      - name: Analisar com SonarQube
        run: mvn sonar:sonar -Dsonar.projectKey=${{ secrets.SONAR_PROJECT_KEY }} -Dsonar.organization=${{ secrets.SONAR_ORGANIZATION }} -Dsonar.host.url=${{ secrets.SONAR_HOST_URL }} -Dsonar.login=${{ secrets.SONAR_TOKEN }}
```

## 🔑 Secrets necessários:
- `SONAR_PROJECT_KEY`: Chave do projeto no SonarQube.
- `SONAR_ORGANIZATION`: Organização do SonarCloud (se usar).
- `SONAR_HOST_URL`: URL do servidor SonarQube (ex: https://sonarcloud.io ou seu self-hosted).
- `SONAR_TOKEN`: Token de autenticação.

---

