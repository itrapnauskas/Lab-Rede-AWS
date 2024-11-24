# **Conte�do: Redes e Entrega de Conte�do**

## **Introdu��o aos Principais Conceitos de Redes**
Este m�dulo abrange conceitos fundamentais sobre redes e entrega de conte�do, destacando servi�os da AWS como **Amazon VPC**, **Amazon Route 53**, e **Amazon CloudFront**. Esses servi�os s�o essenciais para criar, gerenciar e otimizar redes na nuvem e entregar conte�do de forma eficiente e segura.

---

### **No��es B�sicas de Redes**

#### **1. O que � uma Rede de Computadores?**
Uma rede de computadores conecta dois ou mais dispositivos para compartilhar recursos e permitir comunica��o. Ela pode ser segmentada em **sub-redes**, sendo que cada sub-rede pode ter regras e caracter�sticas pr�prias. Elementos essenciais incluem:
- **Roteadores e switches**: Dispositivos que permitem a comunica��o entre m�quinas.
- **Sub-redes**: Segmentos da rede criados para otimizar a organiza��o e seguran�a.

#### **2. Endere�os IP e CIDR**
- **IPv4 e IPv6**: Identificadores �nicos que permitem que dispositivos na rede se comuniquem.
  - **IPv4**: Endere�o de 32 bits (exemplo: 192.0.2.0).
  - **IPv6**: Endere�o de 128 bits (exemplo: 2600:1f18:22ba:8c00:ba86:a05e:a5ba:00FF).
- **CIDR (Classless Inter-Domain Routing)**: Define o tamanho da rede. Por exemplo:
  - `10.0.0.0/16`: Rede com 65.536 endere�os IP dispon�veis.
  - `10.0.0.0/24`: Rede com 256 endere�os IP dispon�veis.

#### **3. Modelo OSI**
Modelo de refer�ncia com 7 camadas que explica como os dados trafegam entre dispositivos:
1. **F�sica**: Sinais el�tricos, fibras �pticas.
2. **Enlace**: Switches e MAC addresses.
3. **Rede**: Roteamento, endere�os IP.
4. **Transporte**: TCP/UDP.
5. **Sess�o**: Gerencia conex�es.
6. **Apresenta��o**: Criptografia e compress�o.
7. **Aplica��o**: HTTP, FTP.

---

### **Se��o 2: Amazon VPC**

#### **1. O que � Amazon VPC?**
Amazon Virtual Private Cloud permite criar redes isoladas na nuvem, oferecendo controle completo sobre endere�os IP, sub-redes, tabelas de rotas e gateways.

#### **2. Componentes Fundamentais da Amazon VPC**
- **Sub-redes**: 
  - **P�blica**: Acesso direto � internet.
  - **Privada**: Isolada da internet.
- **Tabelas de Rota**: Regras que direcionam o tr�fego da rede.
- **Gateways**:
  - **Internet Gateway**: Conecta a sub-rede p�blica � internet.
  - **NAT Gateway**: Permite que sub-redes privadas acessem a internet sem serem acess�veis por ela.

#### **3. Seguran�a na VPC**
- **Grupos de Seguran�a (Security Groups)**: Controlam o tr�fego em n�vel de inst�ncia.
- **Listas de Controle de Acesso � Rede (Network ACLs)**: Controlam o tr�fego em n�vel de sub-rede.

---

### **Se��o 3: Amazon Route 53**

#### **1. O que � Amazon Route 53?**
Servi�o de DNS gerenciado pela AWS que traduz nomes de dom�nio em endere�os IP. Suporta:
- **Roteamento geogr�fico**: Direciona usu�rios ao servidor mais pr�ximo.
- **Failover DNS**: Redireciona usu�rios a servidores de backup em caso de falhas.

---

### **Se��o 4: Amazon CloudFront**

#### **1. O que � Amazon CloudFront?**
Servi�o de Rede de Entrega de Conte�do (CDN) que usa pontos de presen�a globais para:
- Melhorar a velocidade de entrega de conte�do.
- Reduzir a lat�ncia para usu�rios finais.
- Aumentar a seguran�a e a escalabilidade de aplica��es.

#### **2. Benef�cios**
- Baixa lat�ncia.
- Seguran�a integrada (AWS Shield, SSL).
- Integra��o com outros servi�os AWS.

---
