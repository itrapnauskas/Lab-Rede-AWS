# **Conte�do: Redes e Entrega de Conte�do**

## **Introdu��o aos Principais Conceitos de Redes**
Este m�dulo abrange conceitos fundamentais sobre redes e entrega de conte�do, destacando servi�os da AWS como **Amazon VPC**, **Amazon Route 53**, e **Amazon CloudFront**. Esses servi�os s�o essenciais para criar, gerenciar e otimizar redes na nuvem e entregar conte�do de forma eficiente e segura.

---

### **Se��o 1: No��es B�sicas de Redes**

## **O que � uma Rede de Computadores?**

Uma **rede de computadores** � uma conex�o entre dois ou mais dispositivos (computadores, servidores, impressoras, etc.) que permite o compartilhamento de recursos e a comunica��o entre eles. As redes podem ser divididas logicamente em **sub-redes** para otimizar a organiza��o, seguran�a e efici�ncia do tr�fego de dados.

- **Roteador**: Dispositivo que encaminha pacotes de dados entre redes, determinando o melhor caminho para o tr�fego.
- **Switch**: Dispositivo que conecta dispositivos dentro da mesma rede, permitindo a comunica��o direta entre eles.

**Exemplo de Rede com Sub-redes:**

```
               Roteador
              /         \
        Sub-rede 1    Sub-rede 2
```

---

### **Endere�os IP**

Cada dispositivo em uma rede possui um **endere�o IP (Internet Protocol)** exclusivo que o identifica. Esse endere�o � um r�tulo num�rico que segue padr�es espec�ficos para garantir a comunica��o correta entre dispositivos.

#### **Endere�os IPv4**

- **Formato Decimal**: Consiste em quatro n�meros separados por pontos, por exemplo, `192.0.2.0`.
- **Convers�o Bin�ria**: Cada n�mero decimal representa 8 bits (um octeto) no formato bin�rio.

**Exemplo de Convers�o:**

```
Decimal: 192.0.2.0
Bin�rio:
192 -> 11000000
0   -> 00000000
2   -> 00000010
0   -> 00000000
```

- O total combinado � um endere�o de 32 bits.

#### **Endere�os IPv6**

- Criados para expandir a capacidade de endere�amento devido � limita��o do IPv4.
- **Formato Hexadecimal**: Composto por oito grupos de quatro caracteres hexadecimais separados por dois pontos, por exemplo, `2600:1f18:22ba:8c00:ba86:a05e:a5ba:00FF`.
- Totalizam 128 bits, permitindo uma quantidade muito maior de endere�os.

---

### **Roteamento Sem Classe entre Dom�nios (CIDR)**

O **CIDR (Classless Inter-Domain Routing)** � um m�todo usado para alocar endere�os IP de maneira eficiente e especificar redes de diferentes tamanhos.

- **Nota��o CIDR**: Combina um endere�o IP com um sufixo que indica o n�mero de bits fixos (rede) no endere�o.
- **Exemplo**: `192.0.2.0/24`
  - `/24` indica que os primeiros 24 bits s�o fixos, representando o **identificador de rede**.
  - Os 8 bits restantes s�o flex�veis, permitindo varia��o nos endere�os dos hosts dentro da rede.

**C�lculo de Endere�os Dispon�veis:**

- Com `/24`, temos 2^8 = 256 endere�os IP poss�veis na rede, variando de `192.0.2.0` a `192.0.2.255`.

**Casos Especiais:**

- **Endere�o Individual**: `/32` fixa todos os 32 bits, representando um �nico endere�o IP.
- **Toda a Internet**: `0.0.0.0/0` representa todos os endere�os IP poss�veis.

---

### **Modelo de Interconex�o de Sistemas Abertos (OSI)**

O **Modelo OSI** � um modelo conceitual de sete camadas que descreve as fun��es de um sistema de rede, permitindo a interoperabilidade entre diferentes produtos e softwares.

#### **As Sete Camadas do Modelo OSI:**

1. **Camada F�sica (1):**
   - Transmiss�o de bits brutos atrav�s de um meio f�sico (cabos, sinais el�tricos, fibras �pticas).
   - Dispositivos: Hubs, repetidores.
   - Fun��o: Define as especifica��es el�tricas e mec�nicas dos dispositivos.

2. **Camada de Enlace de Dados (2):**
   - Fornece a transfer�ncia de dados entre dispositivos na mesma rede local (LAN).
   - Dispositivos: Switches, bridges.
   - Endere�amento: Endere�os MAC (Media Access Control).

3. **Camada de Rede (3):**
   - Respons�vel pelo roteamento e encaminhamento de pacotes entre redes diferentes.
   - Dispositivos: Roteadores.
   - Protocolos: IP (Internet Protocol).

4. **Camada de Transporte (4):**
   - Garante a transfer�ncia confi�vel de dados entre hosts.
   - Protocolos: TCP (Transmission Control Protocol), UDP (User Datagram Protocol).

5. **Camada de Sess�o (5):**
   - Estabelece, gerencia e termina sess�es entre aplica��es.
   - Protocolos: NetBIOS, RPC (Remote Procedure Call).

6. **Camada de Apresenta��o (6):**
   - Traduz os dados para o formato que a aplica��o aceita.
   - Fun��es: Criptografia, compress�o, convers�o de dados.

7. **Camada de Aplica��o (7):**
   - Interface direta com o usu�rio e fornece servi�os de rede �s aplica��es.
   - Protocolos: HTTP(S), FTP, SMTP, DNS.

---

### **Tipos de Redes**

#### **LAN (Local Area Network)**

- Redes locais que cobrem pequenas �reas geogr�ficas, como escrit�rios, resid�ncias ou pequenos edif�cios.
- Caracter�sticas:
  - Alta velocidade de transmiss�o.
  - Controle centralizado.
  - Baixa lat�ncia.

#### **WAN (Wide Area Network)**

- Redes que cobrem �reas geogr�ficas amplas, como cidades, pa�ses ou continentes.
- Caracter�sticas:
  - Interconex�o de m�ltiplas LANs.
  - Utiliza meios de transmiss�o de longa dist�ncia.
  - Exemplo: A Internet.

---

### **Endere�amento IP e M�scaras de Sub-rede**

#### **M�scara de Sub-rede**

- Determina qual parte do endere�o IP � o identificador de rede e qual parte � o identificador do host.
- **Exemplo**:
  - Endere�o IP: `192.168.1.10`
  - M�scara de Sub-rede: `255.255.255.0` (ou `/24`)
  - Significa que os primeiros 24 bits s�o para a rede (`192.168.1`) e os �ltimos 8 bits para os hosts.

#### **Divis�o de Redes em Sub-redes**

- Permite organizar melhor a rede, melhorar a seguran�a e o desempenho.
- Cada sub-rede pode ter pol�ticas e controles espec�ficos.

---

### **Endere�os IP Reservados**

Em cada sub-rede, certos endere�os IP s�o reservados e n�o podem ser usados para hosts.

- **Endere�o de Rede**: Primeiro endere�o do bloco (todos os bits de host em 0).
- **Endere�o de Broadcast**: �ltimo endere�o do bloco (todos os bits de host em 1).
- **Endere�os Reservados pela AWS**:
  - **Comunica��o Interna**: `10.0.0.1`
  - **Servi�os de DNS**: `10.0.0.2`
  - **Uso Futuro**: `10.0.0.3`

**Exemplo em uma Sub-rede `/24` (`10.0.0.0/24`):**

- **Endere�os Reservados**:
  - `10.0.0.0`: Endere�o de rede.
  - `10.0.0.255`: Endere�o de broadcast.
- **Endere�os Dispon�veis para Hosts**:
  - De `10.0.0.4` a `10.0.0.254`.

---

### **Tipos de Endere�os IP P�blicos**

#### **Endere�o IPv4 P�blico**

- **Atribui��o Autom�tica**: Configurada para que inst�ncias recebam um IP p�blico ao serem iniciadas.
- **Atribui��o Manual**: Atrav�s de **Endere�os IP El�sticos**.

#### **Endere�o IP El�stico (EIP)**

- Endere�o IPv4 est�tico p�blico associado � sua conta AWS.
- Pode ser associado e remapeado entre inst�ncias ou interfaces de rede.
- �til para mascarar falhas de inst�ncias, remapeando rapidamente o endere�o para uma inst�ncia em funcionamento.
- **Custos**:
  - Podem ocorrer cobran�as se o EIP n�o estiver associado a uma inst�ncia em execu��o.

---

### **Interface de Rede El�stica**

Uma **Interface de Rede El�stica (ENI)** � uma interface de rede virtual que pode ser:

- **Anexada** a uma inst�ncia.
- **Desanexada** e reanexada a outra inst�ncia, permitindo flexibilidade e redirecionamento de tr�fego.
- **Atributos Mantidos**:
  - Endere�os IP privados.
  - Endere�os IP el�sticos (se houver).
  - Grupos de seguran�a.
  - DNS.

Cada inst�ncia possui uma interface de rede prim�ria. � poss�vel criar interfaces adicionais e anex�-las conforme necess�rio, dependendo do tipo da inst�ncia.

---

### **Rotas e Tabelas de Rotas**

As **Tabelas de Rotas** definem como o tr�fego de rede � direcionado dentro da VPC.

- **Rota Local**:
  - Presente por padr�o.
  - Permite comunica��o dentro da VPC.
  - **N�o pode ser removida**.

- **Rotas Personalizadas**:
  - Podem ser adicionadas para direcionar tr�fego para fora da VPC, como para a internet ou outras redes.
  - **Destinos**: Especificam o bloco de endere�os IP de destino (por exemplo, `0.0.0.0/0` para toda a internet).
  - **Alvos**: Especificam para onde enviar o tr�fego (por exemplo, um **Internet Gateway** ou **NAT Gateway**).

**Associa��o de Tabelas de Rotas:**

- Cada sub-rede deve estar associada a uma tabela de rotas.
- Se uma sub-rede n�o for associada explicitamente a uma tabela de rotas, ela usar� a tabela de rotas principal da VPC.

---

## **Principais Li��es da Se��o 1**

- **Redes de Computadores**: Conectam dispositivos para comunica��o e compartilhamento de recursos.
- **Endere�os IP**: Identificadores �nicos para dispositivos na rede; podem ser IPv4 ou IPv6.
- **CIDR**: M�todo para definir blocos de endere�os IP e tamanhos de rede.
- **Modelo OSI**: Estrutura em camadas que descreve a comunica��o em redes.
- **Sub-redes**: Divis�es l�gicas dentro de uma rede para melhor gerenciamento e seguran�a.
- **Endere�os IP Reservados**: Certos endere�os em uma sub-rede s�o reservados e n�o podem ser usados por dispositivos.
- **Tipos de Endere�os IP P�blicos**: Incluem endere�os IP p�blicos atribu�dos automaticamente e Endere�os IP El�sticos.
- **Interface de Rede El�stica**: Permite flexibilidade na gest�o de interfaces de rede e endere�os IP.
- **Tabelas de Rotas**: Controlam o fluxo de tr�fego dentro e fora da VPC.

---

## **Refer�ncias para Estudo Adicional**

- **Documenta��o AWS sobre Amazon VPC**:
  - [O que � Amazon VPC?](https://docs.aws.amazon.com/pt_br/vpc/latest/userguide/what-is-amazon-vpc.html)
- **Conceitos de Redes**:
  - **Endere�amento IP e Sub-redes**:
    - [Conceitos B�sicos de Sub-redes](https://www.techtudo.com.br/artigos/noticia/2016/08/entenda-o-que-e-sub-rede-e-para-que-serve.html)
  - **Modelo OSI**:
    - [As Sete Camadas do Modelo OSI](https://www.redesdamais.com.br/as-sete-camadas-do-modelo-osi/)

---

## **Conclus�o**

Compreender os fundamentos de redes � crucial para projetar e implementar infraestruturas eficientes e seguras na nuvem. Os conceitos abordados nesta se��o servem como base para as pr�ximas etapas, onde aplicaremos esse conhecimento na configura��o de redes virtuais com o Amazon VPC, explorando suas funcionalidades e benef�cios.

---

# **Pr�ximos Passos**

- **Se��o 2: Amazon VPC**
  - Exploraremos como criar redes virtuais na nuvem usando o Amazon VPC.
  - Aprenderemos sobre sub-redes p�blicas e privadas, gateways e tabelas de rotas.
- **Se��o 3: Redes da VPC**
  - Veremos as diferentes op��es de conectividade e como expandir nossas redes.
- **Se��o 4: Seguran�a da VPC**
  - Entenderemos como proteger nossas redes usando grupos de seguran�a e ACLs de rede.

---

Aprofundar-se nesses conceitos permitir� que voc� projete arquiteturas de rede robustas e seguras, atendendo �s necessidades espec�ficas de aplica��es modernas e escal�veis.

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
