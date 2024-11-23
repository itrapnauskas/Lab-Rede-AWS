# **Introdução aos Principais Conceitos de Redes**

Antes de iniciar o plano de ação do laboratório, é fundamental entender os conceitos que serão trabalhados. Abaixo está um resumo completo sobre os principais elementos que compõem uma rede de computadores e como esses conceitos se aplicam na nuvem, especialmente da AWS.

---

## **Conceitos Principais**

### **1. Rede de Computadores**
- Uma rede de computadores conecta dispositivos para compartilhar recursos e se comunicar. 
- Dispositivos finais (hosts): Computadores, celulares, impressoras e servidores.
- Equipamentos intermediários: Switches e roteadores que conectam dispositivos e permitem o tráfego de dados.

### **2. Tipos de Redes**
- **LAN (Local Area Network):** Rede local limitada a uma área pequena, como um escritório ou casa.
- **WAN (Wide Area Network):** Rede que cobre áreas geográficas amplas, como a internet.
- **Sub-redes:** Divisão lógica de redes para organizar e otimizar o tráfego.

---

### **3. Endereços IP e Máscaras de Sub-rede**
- **IPv4:** Endereços numéricos (ex.: 192.168.0.1) usados para identificar dispositivos em uma rede.
- **Máscara de Sub-rede:** Define o tamanho e a divisão da rede. Exemplo: `/24` indica que 256 endereços estão disponíveis.
- **CIDR (Classless Inter-Domain Routing):** Método para definir intervalos de IP. Ex.: `10.0.0.0/16`.

---

### **4. Gateway**
- Dispositivo que conecta uma rede local à internet ou a outras redes.
- No AWS, é implementado como um **Internet Gateway** ou **NAT Gateway**.

---

### **5. Segurança em Redes**
- **Grupos de Segurança (Security Groups):** Controle de acesso em nível de instância, permitindo ou bloqueando tráfego com base em regras.
- **Network ACLs:** Controle de acesso em nível de sub-rede.

---

### **6. Amazon Virtual Private Cloud (VPC)**
- Rede virtual isolada criada na AWS.
- Permite configurar sub-redes públicas e privadas, tabelas de rotas e gateways para personalizar a comunicação e segurança da rede.

---

### **7. Sub-redes**
- **Sub-rede Pública:** Permite acesso direto à internet.
- **Sub-rede Privada:** Restrita à comunicação interna da rede, sem acesso direto à internet.

---

### **8. Amazon EC2 (Elastic Compute Cloud)**
- Serviço de computação que permite criar e executar máquinas virtuais.
- Usaremos o EC2 para lançar uma instância configurada como servidor web.

---

### **9. HTTP e Web Servers**
- Protocolo HTTP: Permite a comunicação entre o navegador e servidores web.
- Servidor Web: Software (como Apache) que disponibiliza páginas e recursos na internet.

---

## **Plano de Ação - Laboratório Prático**

Os alunos devem seguir as etapas abaixo para criar uma VPC personalizada, configurar sub-redes, grupos de segurança e lançar uma instância EC2 para hospedar um servidor web.

---

### **Etapa 1: Criar a VPC**

1. **Acessar o Console AWS**
   - Entre no console AWS e pesquise por **VPC**.
   - Certifique-se de que a região selecionada é **N. Virginia (us-east-1)**.

2. **Criar a VPC**
   - Clique em **Create VPC**.
   - Selecione **VPC and more**.
   - Configure:
     - **Nome:** `lab-vpc`
     - **CIDR IPv4:** `10.0.0.0/16`
     - Sub-rede pública: `10.0.0.0/24`
     - Sub-rede privada: `10.0.1.0/24`
     - NAT Gateway: Ativado.
     - DNS: Habilitado.

3. **Verificar os Recursos Criados**
   - Após criar a VPC, revise os recursos:
     - Sub-redes públicas e privadas.
     - Tabelas de rotas associadas.
     - Internet Gateway e NAT Gateway.

---

### **Etapa 2: Adicionar Sub-redes em Outra Zona de Disponibilidade**

1. **Criar Sub-rede Pública Secundária**
   - Nome: `lab-subnet-public2`.
   - CIDR: `10.0.2.0/24`.
   - Zona de Disponibilidade: `us-east-1b`.

2. **Criar Sub-rede Privada Secundária**
   - Nome: `lab-subnet-private2`.
   - CIDR: `10.0.3.0/24`.
   - Zona de Disponibilidade: `us-east-1b`.

3. **Atualizar as Tabelas de Rotas**
   - Associe a sub-rede privada secundária ao NAT Gateway.
   - Associe a sub-rede pública secundária ao Internet Gateway.

---

### **Etapa 3: Configurar Grupos de Segurança**

1. **Criar Grupo de Segurança**
   - Nome: `Web Security Group`.
   - Descrição: `Permitir acesso HTTP`.
   - Regras:
     - Tipo: HTTP.
     - Origem: Anywhere-IPv4.

---

### **Etapa 4: Lançar a Instância EC2**

1. **Configurar a Instância**
   - Nome: `Web Server 1`.
   - AMI: Amazon Linux 2023.
   - Tipo: `t2.micro`.
   - Sub-rede: `lab-subnet-public2`.
   - Grupo de Segurança: `Web Security Group`.

2. **Adicionar Script de Inicialização**
   - No campo **User Data**, insira o script abaixo para configurar o servidor web:
     ```bash
     #!/bin/bash
     dnf install -y httpd wget php mariadb105-server
     wget https://aws-tc-largeobjects.s3.us-west-2.amazonaws.com/CUR-TF-100-ACCLFO-2/2-lab2-vpc/s3/lab-app.zip
     unzip lab-app.zip -d /var/www/html/
     chkconfig httpd on
     service httpd start
     ```

3. **Lançar a Instância**
   - Clique em **Launch Instance**.
   - Espere o status **2/2 checks passed**.

---

### **Etapa 5: Testar o Servidor Web**

1. **Obter o DNS Público**
   - No console EC2, copie o **Public IPv4 DNS** da instância.

2. **Acessar o Servidor**
   - Abra um navegador e cole o DNS copiado.
   - Verifique se a página exibe o logotipo da AWS e as informações do servidor.

---

## **Avaliação do Sucesso**

### **Critérios de Avaliação**
- **Estrutura de Rede:** 
  - VPC configurada com sub-redes públicas e privadas corretamente.
  - Tabelas de rotas associadas aos gateways apropriados.
- **Segurança:**
  - Grupo de segurança configurado corretamente para permitir tráfego HTTP.
- **Servidor Web:**
  - Instância EC2 acessível via DNS público.
  - Página web carregando corretamente.

---

