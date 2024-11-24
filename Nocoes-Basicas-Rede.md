# **Conteúdo: Redes e Entrega de Conteúdo**

## **Introdução aos Principais Conceitos de Redes**
Este módulo abrange conceitos fundamentais sobre redes e entrega de conteúdo, destacando serviços da AWS como **Amazon VPC**, **Amazon Route 53**, e **Amazon CloudFront**. Esses serviços são essenciais para criar, gerenciar e otimizar redes na nuvem e entregar conteúdo de forma eficiente e segura.

---

### **Noções Básicas de Redes**

#### **1. O que é uma Rede de Computadores?**
Uma rede de computadores conecta dois ou mais dispositivos para compartilhar recursos e permitir comunicação. Ela pode ser segmentada em **sub-redes**, sendo que cada sub-rede pode ter regras e características próprias. Elementos essenciais incluem:
- **Roteadores e switches**: Dispositivos que permitem a comunicação entre máquinas.
- **Sub-redes**: Segmentos da rede criados para otimizar a organização e segurança.

#### **2. Endereços IP e CIDR**
- **IPv4 e IPv6**: Identificadores únicos que permitem que dispositivos na rede se comuniquem.
  - **IPv4**: Endereço de 32 bits (exemplo: 192.0.2.0).
  - **IPv6**: Endereço de 128 bits (exemplo: 2600:1f18:22ba:8c00:ba86:a05e:a5ba:00FF).
- **CIDR (Classless Inter-Domain Routing)**: Define o tamanho da rede. Por exemplo:
  - `10.0.0.0/16`: Rede com 65.536 endereços IP disponíveis.
  - `10.0.0.0/24`: Rede com 256 endereços IP disponíveis.

#### **3. Modelo OSI**
Modelo de referência com 7 camadas que explica como os dados trafegam entre dispositivos:
1. **Física**: Sinais elétricos, fibras ópticas.
2. **Enlace**: Switches e MAC addresses.
3. **Rede**: Roteamento, endereços IP.
4. **Transporte**: TCP/UDP.
5. **Sessão**: Gerencia conexões.
6. **Apresentação**: Criptografia e compressão.
7. **Aplicação**: HTTP, FTP.

---

### **Seção 2: Amazon VPC**

#### **1. O que é Amazon VPC?**
Amazon Virtual Private Cloud permite criar redes isoladas na nuvem, oferecendo controle completo sobre endereços IP, sub-redes, tabelas de rotas e gateways.

#### **2. Componentes Fundamentais da Amazon VPC**
- **Sub-redes**: 
  - **Pública**: Acesso direto à internet.
  - **Privada**: Isolada da internet.
- **Tabelas de Rota**: Regras que direcionam o tráfego da rede.
- **Gateways**:
  - **Internet Gateway**: Conecta a sub-rede pública à internet.
  - **NAT Gateway**: Permite que sub-redes privadas acessem a internet sem serem acessíveis por ela.

#### **3. Segurança na VPC**
- **Grupos de Segurança (Security Groups)**: Controlam o tráfego em nível de instância.
- **Listas de Controle de Acesso à Rede (Network ACLs)**: Controlam o tráfego em nível de sub-rede.

---

### **Seção 3: Amazon Route 53**

#### **1. O que é Amazon Route 53?**
Serviço de DNS gerenciado pela AWS que traduz nomes de domínio em endereços IP. Suporta:
- **Roteamento geográfico**: Direciona usuários ao servidor mais próximo.
- **Failover DNS**: Redireciona usuários a servidores de backup em caso de falhas.

---

### **Seção 4: Amazon CloudFront**

#### **1. O que é Amazon CloudFront?**
Serviço de Rede de Entrega de Conteúdo (CDN) que usa pontos de presença globais para:
- Melhorar a velocidade de entrega de conteúdo.
- Reduzir a latência para usuários finais.
- Aumentar a segurança e a escalabilidade de aplicações.

#### **2. Benefícios**
- Baixa latência.
- Segurança integrada (AWS Shield, SSL).
- Integração com outros serviços AWS.

---
