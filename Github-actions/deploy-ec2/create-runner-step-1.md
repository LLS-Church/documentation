## 🏃 Como Deixar o Runner rodando em Background

1. Instale o runner no seu EC2.

2. Acesse a pasta do runner:

```bash
cd actions-runner
```

3. Instale o serviço:

```bash
sudo ./svc.sh install
```

4. Inicie o serviço:

```bash
sudo ./svc.sh start
```

5. Valide que o serviço está rodando:

```bash
sudo ./svc.sh status
```

Você verá uma resposta parecida com:

```
Service "actions.runner.SEU_REPO" is running
```

Isso garante que o runner se inicia automaticamente no boot e fica ativo em background.

## Observações:
- Configure `DOCKER_USERNAME`, `DOCKER_PASSWORD`, `DATABASE_URL`, `DATABASE_USERNAME` e `DATABASE_PASSWORD` nos **Secrets** do GitHub.
- O runner `self-hosted` deve estar rodando na sua EC2 para o deploy automático funcionar.
