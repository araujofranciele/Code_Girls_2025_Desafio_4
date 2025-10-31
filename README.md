# Laboratório AWS CloudFormation – Infraestrutura Automatizada

## 📌 Objetivo

O objetivo deste laboratório é **implementar uma infraestrutura automatizada usando AWS CloudFormation**, praticando **Infraestrutura como Código (IaC)** e criando um ambiente totalmente provisionado de forma automática.

Nesta Stack, criamos:

* **Duas instâncias EC2** com Amazon Linux 2
* **Security Group** para permitir acesso SSH (22) e HTTP (80)
* **Apache Web Server** instalado automaticamente via **User Data**
* **Elastic Load Balancer (ALB)** para distribuir tráfego entre as instâncias
* **Outputs** úteis como IPs das instâncias, DNS do ALB e ID do Security Group

---

## 📚 Conceitos Aprendidos

* **Stack e Template**: organização de recursos AWS em um único arquivo YAML.
* **Resources**: EC2, Security Groups e Load Balancer provisionados automaticamente.
* **Parameters**: valores dinâmicos para customizar infraestrutura (tipo de instância, chave SSH).
* **User Data**: scripts que configuram automaticamente as instâncias EC2.
* **Outputs**: informações importantes sobre os recursos criados.
* **Dependências e orquestração**: controle da ordem de criação automática de recursos.

---

## 🛠️ Serviços e Ferramentas Utilizadas

* **AWS CloudFormation** – Criação, atualização e exclusão da Stack
* **Amazon EC2** – Instâncias de máquinas virtuais
* **Security Group** – Controle de acesso às instâncias
* **Elastic Load Balancer (ALB)** – Distribuição de tráfego entre instâncias
* **AWS CLI** – Validação e deploy da Stack via terminal (opcional)

---

## 📝 Passo a Passo da Implementação

1. **Criação do Template YAML**

   * Salvar o arquivo como `infra-automatizada.yaml` (template fornecido no repositório).
   * Ajustar IDs de **subnets** e **VPC**, **KeyName** e **ImageId (AMI)** conforme sua região.

2. **Validação do Template**

   ```bash
   aws cloudformation validate-template --template-body file://infra-automatizada.yaml
   ```

3. **Criação da Stack**

   ```bash
   aws cloudformation create-stack \
   --stack-name InfraestruturaAutomatizada \
   --template-body file://infra-automatizada.yaml \
   --parameters ParameterKey=KeyName,ParameterValue=minha-chave-ec2
   ```

4. **Monitoramento da Stack**

   * Acompanhar status pelo console ou via CLI:

   ```bash
   aws cloudformation describe-stacks --stack-name InfraestruturaAutomatizada
   ```

5. **Acesso e Testes**

   * Usar os **Outputs** para acessar as instâncias EC2 e o ALB.
   * Verificar se os scripts de User Data instalaram corretamente o Apache e criaram a página HTML.

6. **Atualização da Stack**

   * Modificar o template e atualizar a Stack:

   ```bash
   aws cloudformation update-stack \
   --stack-name InfraestruturaAutomatizada \
   --template-body file://infra-automatizada.yaml
   ```

7. **Exclusão da Stack**

   ```bash
   aws cloudformation delete-stack --stack-name InfraestruturaAutomatizada
   ```

---

## 💡 Insights e Dicas

* **Automatização completa:** facilita replicar ambientes rapidamente.
* **Parâmetros tornam a Stack flexível:** permite mudanças sem alterar o YAML.
* **User Data automatiza configuração de servidores.**
* **Outputs são úteis para integração e testes rápidos.**
* **Segurança:** limitar IPs no Security Group em ambientes de produção.
* **Tags ajudam na organização e rastreabilidade de recursos.**

---

## 📂 Estrutura do Repositório

```
aws-cloudformation-lab-2/
│
├── infra-automatizada.yaml    # Template CloudFormation
├── README.md                  # Este arquivo
└── notas-de-estudo.md         # Anotações e insights do laboratório

Quer que eu faça isso?

