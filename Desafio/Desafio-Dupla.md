```markdown
# **Desafio: Configure Sua Própria VPC e Inicie um Servidor Web**

Neste desafio, você irá criar uma infraestrutura personalizada na **AWS**, configurando uma **Amazon VPC** e adicionando componentes essenciais como sub-redes, tabelas de rotas, e um grupo de segurança. Ao final, você irá lançar uma instância EC2 configurada como um servidor web. O objetivo é proporcionar uma experiência prática no uso da AWS para construir uma rede segura e funcional.

---

## **Cenário**

Você foi contratado para configurar a infraestrutura de uma pequena empresa que precisa de uma rede virtual com os seguintes requisitos:

- **VPC personalizada:** com sub-redes públicas e privadas.
- **Alta disponibilidade:** sub-redes distribuídas em múltiplas Zonas de Disponibilidade (AZs).
- **Servidor Web Público:** acessível pela internet.
- **Segurança:** regras que permitam apenas tráfego HTTP para o servidor web.
- **Conectividade Privada:** recursos na sub-rede privada acessam a internet através de um NAT Gateway.

Ao concluir este desafio, sua arquitetura incluirá:

- **VPC:** `10.0.0.0/16`
- **Sub-redes públicas:** `10.0.0.0/24` e `10.0.2.0/24`
- **Sub-redes privadas:** `10.0.1.0/24` e `10.0.3.0/24`
- **Internet Gateway e NAT Gateway:** conectividade segura entre as sub-redes e a internet.
- **Servidor Web:** instância EC2 em uma sub-rede pública.

---

## **Instruções Detalhadas**

### **Passo 1: Criação da VPC e Sub-redes**

1. **Acesse o Console da AWS**:
   - No canto superior direito, selecione a região **N. Virginia (us-east-1)**.
   - No menu de serviços, procure e acesse o **VPC Console**.

2. **Configure a VPC**:
   - Clique em **Create VPC**.
   - Selecione **VPC and more**.
   - Configure os parâmetros:
     - **Name tag auto-generation:** `lab-vpc`.
     - **IPv4 CIDR block:** `10.0.0.0/16`.
     - **Number of Availability Zones:** `1`.
     - **Number of public subnets:** `1` (`10.0.0.0/24`).
     - **Number of private subnets:** `1` (`10.0.1.0/24`).
     - **NAT Gateway:** `In 1 AZ`.
     - **VPC Endpoints:** `None`.

3. **Adicione Sub-redes Adicionais**:
   - Crie mais duas sub-redes:
     - Sub-rede pública: `10.0.2.0/24` na **AZ us-east-1b**.
     - Sub-rede privada: `10.0.3.0/24` na **AZ us-east-1b**.

4. **Atualize as Tabelas de Rotas**:
   - Associe as sub-redes públicas ao **Internet Gateway**.
   - Associe as sub-redes privadas ao **NAT Gateway**.

---

### **Passo 2: Configuração de Segurança**

1. **Crie um Grupo de Segurança**:
   - Vá em **Security Groups** e clique em **Create Security Group**.
   - Configure:
     - **Name:** `Web Security Group`.
     - **Description:** `Enable HTTP access`.
     - **VPC:** `lab-vpc`.

2. **Adicione Regras de Entrada**:
   - **Type:** HTTP.
   - **Source:** Anywhere-IPv4.
   - **Description:** `Permit web requests`.

---

### **Passo 3: Lançamento do Servidor Web**

1. **Crie a Instância EC2**:
   - Vá ao serviço **EC2** e clique em **Launch Instance**.
   - Configure:
     - **Name:** `Web Server 1`.
     - **AMI:** Amazon Linux 2023 (padrão selecionado).
     - **Instance type:** `t2.micro`.
     - **Key pair:** selecione ou crie um par de chaves.
     - **Network settings:**
       - **Network:** `lab-vpc`.
       - **Subnet:** `lab-subnet-public2`.
       - **Auto-assign public IP:** Enable.
       - **Security group:** `Web Security Group`.

2. **Configure o Script de Inicialização**:
   - Em **Advanced details**, cole o seguinte script em **User data**:

     ```bash
     #!/bin/bash
     # Instalar servidor web e dependências
     dnf install -y httpd wget php mariadb105-server
     # Baixar arquivos da aplicação
     wget https://aws-tc-largeobjects.s3.us-west-2.amazonaws.com/CUR-TF-100-ACCLFO-2/2-lab2-vpc/s3/lab-app.zip
     unzip lab-app.zip -d /var/www/html/
     # Iniciar servidor web
     chkconfig httpd on
     service httpd start
     ```

3. **Lance a Instância**:
   - Clique em **Launch Instance** e aguarde até que a instância esteja com o status `2/2 checks passed`.

---

### **Passo 4: Teste e Validação**

1. **Acesse o Servidor Web**:
   - No console EC2, copie o valor **Public IPv4 DNS** da instância.
   - Cole o valor em um navegador e pressione **Enter**.
   - A página deve exibir o logotipo da AWS e valores de meta-dados da instância.

2. **Valide a Conectividade Privada**:
   - Verifique se as sub-redes privadas podem acessar a internet via NAT Gateway.

---

## **Resultados Esperados**

Ao final, você terá:
- Uma VPC com sub-redes públicas e privadas em múltiplas AZs.
- Um servidor web funcional acessível pela internet.
- Recursos privados conectados à internet via NAT Gateway.

---

