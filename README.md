# Terraform Jenkins Aws Project

Este projeto utiliza Terraform para provisionar e gerenciar a infraestrutura numa Cloud através do processo de CI/CD do Jenkins.

## Pré-requisitos

- [Terraform](https://www.terraform.io/downloads.html) v1.0.0 ou superior;
- [Jenkins](https://www.jenkins.io/download/) v2.0 ou superior;
- [Cloud] (AWS) configurado -> Esse projeto pode ser replicado nas demais Clouds, basta realizar as alterações básicas necessárias.

## Estrutura do Projeto

- `main.tf`: Arquivo principal do Terraform que define os recursos da infraestrutura;
- `variables.tf`: Define as variáveis utilizadas no projeto;
- `outputs.tf`: Define as saídas do Terraform após a execução;
- `Jenkisfile`: Declaração dos estágios da pipeline;
- `README.md`: Documentação do projeto.

## Como Usar

1. Clone o repositório:
    ```sh
    git clone https://github.com/hedgaralves/terraform-jenkins-aws
    cd terraform-jenkins
    ```

2. Inicialize o Terraform:
    ```sh
    terraform init
    ```

3. Defina as variáveis necessárias no arquivo `variables.tf`.

4. Aplique a configuração do Terraform:
    ```sh
    terraform apply
    ```

5. Após a conclusão, o Jenkins estará disponível no endereço de saída especificado.

## Contribuição

1. Faça um fork do projeto.
2. Crie uma branch para sua feature (`git checkout -b feature/nova-feature`).
3. Commit suas alterações (`git commit -am 'Adiciona nova feature'`).
4. Faça o push para a branch (`git push origin feature/nova-feature`).
5. Abra um Pull Request.


## Contato

Para mais informações, entre em contato pelo email: [hed.consultor@hotmail.com].
