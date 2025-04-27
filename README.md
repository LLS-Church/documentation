#  Projeto Documentation

Documentação completa de infraestrutura, CI/CD, análise de qualidade e deploy em produção.

## Índice
- [Configuração de Nginx + SSL Let's Encrypt](https://github.com/LLS-Church/documentation/blob/main/Nginx/config.md)
- [Configuração de GitHub Actions para deploy](https://github.com/LLS-Church/documentation/tree/main/Github-actions/deploy-ec2)
  - [Runner Self-hosted - Passo 1](https://github.com/LLS-Church/documentation/blob/main/Github-actions/deploy-ec2/create-runner-step-1.md)
  - [Deploy com Actions - Passo 2](https://github.com/LLS-Church/documentation/blob/main/Github-actions/deploy-ec2/create-action-step-2.md)
- [Configuração de GitHub Actions para Build Java + Testes + SonarQube + JaCoCo](https://github.com/LLS-Church/documentation/tree/main/Github-actions/java)
- [Instalação e configuração do Docker na EC2](https://github.com/LLS-Church/documentation/blob/main/EC2/docker-config.md)

## Requisitos
- AWS EC2 (Ubuntu Server)
- Docker + Docker Compose
- GitHub Actions configurado
- SonarQube ou SonarCloud
- Maven 3.8+
- Java 17
- Nginx

## Estrutura do Repositório

```bash
documentation/
 ├── EC2/
 │    └── docker-config.md
 ├── Github-actions/
 │    └── deploy-ec2/
 │         ├── create-runner-step-1.md
 │         ├── create-action-step-2.md
 │         └── java/
 │              └── java-action.md
 ├── Nginx/
 │    └── config.md
 └── README.md
```



# Como Contribuir

Contribuições são bem-vindas! Sinta-se livre para abrir issues ou enviar pull requests.

1. Faça um fork do projeto
2. Crie uma branch com sua feature/ajuste (`git checkout -b minha-feature`)
3. Commit suas mudanças (`git commit -m 'feat: Minha nova feature'`)
4. Push para a branch (`git push origin minha-feature`)
5. Abra um Pull Request

# 📄 Licença

Este projeto está licenciado sob a licença MIT.
