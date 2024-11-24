# **Aulas de Redes e AWS**

## **Sumário**
- [Seção 1: Noções Básicas de Redes](#seção-1-noções-básicas-de-redes)
- [Seção 2: Amazon VPC](#seção-2-amazon-vpc)
- [Seção 3: Amazon Route 53](#seção-3-amazon-route-53)
- [Seção 4: Amazon CloudFront](#seção-4-amazon-cloudfront)

---

## **Seção 1: Noções Básicas de Redes**

### **Conteúdo**
1. **Introdução às Redes de Computadores**
   - Definição de rede
   - Componentes principais: roteadores e switches
2. **Endereços IP**
   - IPv4: formato e conversão binária
   - IPv6: formato hexadecimal e ampliação de endereços
3. **CIDR (Classless Inter-Domain Routing)**
   - Notação, cálculo de endereços e casos especiais
4. **Modelo OSI**
   - As 7 camadas e suas funções
5. **Tipos de Redes**
   - LAN e WAN: características e aplicações
6. **Endereçamento IP e Máscaras de Sub-rede**
   - Divisão em sub-redes e endereços reservados

### **Principais Lições**
- Compreender como dispositivos se comunicam em uma rede.
- Entender endereços IP e a importância de mascaramento e roteamento.

### **Referências**
- [Conceitos de Sub-redes](https://www.techtudo.com.br/artigos/noticia/2016/08/entenda-o-que-e-sub-rede-e-para-que-serve.html)
- [Modelo OSI](https://www.redesdamais.com.br/as-sete-camadas-do-modelo-osi/)

---

## **Seção 2: Amazon VPC**

### **Conteúdo**
1. **Introdução ao Amazon VPC**
   - O que é uma VPC
   - Benefícios: controle, flexibilidade e segurança
2. **Componentes Principais**
   - VPCs e sub-redes
   - Endereçamento IP e blocos CIDR
   - Gateways: Internet Gateway e NAT Gateway
3. **Segurança**
   - Grupos de Segurança e Network ACLs
4. **Conectividade Avançada**
   - Peering de VPC
   - Site-to-Site VPN
   - AWS Direct Connect

### **Principais Lições**
- Criar redes virtuais isoladas.
- Configurar tabelas de rotas e políticas de segurança.

### **Referências**
- [O que é Amazon VPC?](https://docs.aws.amazon.com/pt_br/vpc/latest/userguide/what-is-amazon-vpc.html)
- [Criando sua primeira VPC](https://docs.aws.amazon.com/pt_br/vpc/latest/userguide/vpc-getting-started.html)

---

## **Seção 3: Amazon Route 53**

### **Conteúdo**
1. **Introdução ao Route 53**
   - Definição e características principais
2. **Funcionalidades**
   - Resolução DNS, registro de domínios, verificações de saúde
   - Políticas de roteamento: Simples, Ponderado, Geográfico, Failover
3. **Casos de Uso**
   - Failover DNS, balanceamento de carga e implementações incrementais
4. **Integração com Outros Serviços**
   - Elastic Load Balancing, Amazon S3, CloudFront

### **Principais Lições**
- Configurar e gerenciar DNS na AWS.
- Implementar failover e balanceamento de tráfego.

### **Referências**
- [Amazon Route 53 Developer Guide](https://docs.aws.amazon.com/route53/)
- [Melhores Práticas para Implementação de DNS Failover](https://aws.amazon.com/pt/blogs/architecture/best-practices-for-implementing-dns-failover-with-amazon-route-53/)

---

## **Seção 4: Amazon CloudFront**

### **Conteúdo**
1. **Introdução ao CloudFront**
   - O que é uma CDN
   - Rede global de Locais de Borda
2. **Funcionamento**
   - Cache de conteúdo e distribuição
   - Integração com S3, EC2, Lambda@Edge
3. **Recursos Avançados**
   - Suporte a HTTP/3, compressão Brotli, certificados SSL
4. **Casos de Uso**
   - Distribuição de sites, streaming de mídia, APIs
5. **Configuração**
   - Criação de distribuições e práticas recomendadas

### **Principais Lições**
- Acelerar a entrega de conteúdo com CloudFront.
- Configurar políticas de cache e segurança.

### **Referências**
- [Amazon CloudFront Developer Guide](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Introduction.html)
- [Boas Práticas para Otimização de Cache](https://aws.amazon.com/pt/blogs/networking-and-content-delivery/best-practices-for-cache-control-directives-with-amazon-cloudfront/)

---

