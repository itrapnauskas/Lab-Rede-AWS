# **Conteúdo: Redes e Entrega de Conteúdo**

## **Introdução aos Principais Conceitos de Redes**
Este módulo abrange conceitos fundamentais sobre redes e entrega de conteúdo, destacando serviços da AWS como **Amazon VPC**, **Amazon Route 53**, e **Amazon CloudFront**. Esses serviços são essenciais para criar, gerenciar e otimizar redes na nuvem e entregar conteúdo de forma eficiente e segura.

---

### **Seção 1: Noções Básicas de Redes**

## **O que é uma Rede de Computadores?**

Uma **rede de computadores** é uma conexão entre dois ou mais dispositivos (computadores, servidores, impressoras, etc.) que permite o compartilhamento de recursos e a comunicação entre eles. As redes podem ser divididas logicamente em **sub-redes** para otimizar a organização, segurança e eficiência do tráfego de dados.

- **Roteador**: Dispositivo que encaminha pacotes de dados entre redes, determinando o melhor caminho para o tráfego.
- **Switch**: Dispositivo que conecta dispositivos dentro da mesma rede, permitindo a comunicação direta entre eles.

**Exemplo de Rede com Sub-redes:**

```
               Roteador
              /         \
        Sub-rede 1    Sub-rede 2
```

---

### **Endereços IP**

Cada dispositivo em uma rede possui um **endereço IP (Internet Protocol)** exclusivo que o identifica. Esse endereço é um rótulo numérico que segue padrões específicos para garantir a comunicação correta entre dispositivos.

#### **Endereços IPv4**

- **Formato Decimal**: Consiste em quatro números separados por pontos, por exemplo, `192.0.2.0`.
- **Conversão Binária**: Cada número decimal representa 8 bits (um octeto) no formato binário.

**Exemplo de Conversão:**

```
Decimal: 192.0.2.0
Binário:
192 -> 11000000
0   -> 00000000
2   -> 00000010
0   -> 00000000
```

- O total combinado é um endereço de 32 bits.

#### **Endereços IPv6**

- Criados para expandir a capacidade de endereçamento devido à limitação do IPv4.
- **Formato Hexadecimal**: Composto por oito grupos de quatro caracteres hexadecimais separados por dois pontos, por exemplo, `2600:1f18:22ba:8c00:ba86:a05e:a5ba:00FF`.
- Totalizam 128 bits, permitindo uma quantidade muito maior de endereços.

---

### **Roteamento Sem Classe entre Domínios (CIDR)**

O **CIDR (Classless Inter-Domain Routing)** é um método usado para alocar endereços IP de maneira eficiente e especificar redes de diferentes tamanhos.

- **Notação CIDR**: Combina um endereço IP com um sufixo que indica o número de bits fixos (rede) no endereço.
- **Exemplo**: `192.0.2.0/24`
  - `/24` indica que os primeiros 24 bits são fixos, representando o **identificador de rede**.
  - Os 8 bits restantes são flexíveis, permitindo variação nos endereços dos hosts dentro da rede.

**Cálculo de Endereços Disponíveis:**

- Com `/24`, temos 2^8 = 256 endereços IP possíveis na rede, variando de `192.0.2.0` a `192.0.2.255`.

**Casos Especiais:**

- **Endereço Individual**: `/32` fixa todos os 32 bits, representando um único endereço IP.
- **Toda a Internet**: `0.0.0.0/0` representa todos os endereços IP possíveis.

---

### **Modelo de Interconexão de Sistemas Abertos (OSI)**

O **Modelo OSI** é um modelo conceitual de sete camadas que descreve as funções de um sistema de rede, permitindo a interoperabilidade entre diferentes produtos e softwares.

#### **As Sete Camadas do Modelo OSI:**

1. **Camada Física (1):**
   - Transmissão de bits brutos através de um meio físico (cabos, sinais elétricos, fibras ópticas).
   - Dispositivos: Hubs, repetidores.
   - Função: Define as especificações elétricas e mecânicas dos dispositivos.

2. **Camada de Enlace de Dados (2):**
   - Fornece a transferência de dados entre dispositivos na mesma rede local (LAN).
   - Dispositivos: Switches, bridges.
   - Endereçamento: Endereços MAC (Media Access Control).

3. **Camada de Rede (3):**
   - Responsável pelo roteamento e encaminhamento de pacotes entre redes diferentes.
   - Dispositivos: Roteadores.
   - Protocolos: IP (Internet Protocol).

4. **Camada de Transporte (4):**
   - Garante a transferência confiável de dados entre hosts.
   - Protocolos: TCP (Transmission Control Protocol), UDP (User Datagram Protocol).

5. **Camada de Sessão (5):**
   - Estabelece, gerencia e termina sessões entre aplicações.
   - Protocolos: NetBIOS, RPC (Remote Procedure Call).

6. **Camada de Apresentação (6):**
   - Traduz os dados para o formato que a aplicação aceita.
   - Funções: Criptografia, compressão, conversão de dados.

7. **Camada de Aplicação (7):**
   - Interface direta com o usuário e fornece serviços de rede às aplicações.
   - Protocolos: HTTP(S), FTP, SMTP, DNS.

---

### **Tipos de Redes**

#### **LAN (Local Area Network)**

- Redes locais que cobrem pequenas áreas geográficas, como escritórios, residências ou pequenos edifícios.
- Características:
  - Alta velocidade de transmissão.
  - Controle centralizado.
  - Baixa latência.

#### **WAN (Wide Area Network)**

- Redes que cobrem áreas geográficas amplas, como cidades, países ou continentes.
- Características:
  - Interconexão de múltiplas LANs.
  - Utiliza meios de transmissão de longa distância.
  - Exemplo: A Internet.

---

### **Endereçamento IP e Máscaras de Sub-rede**

#### **Máscara de Sub-rede**

- Determina qual parte do endereço IP é o identificador de rede e qual parte é o identificador do host.
- **Exemplo**:
  - Endereço IP: `192.168.1.10`
  - Máscara de Sub-rede: `255.255.255.0` (ou `/24`)
  - Significa que os primeiros 24 bits são para a rede (`192.168.1`) e os últimos 8 bits para os hosts.

#### **Divisão de Redes em Sub-redes**

- Permite organizar melhor a rede, melhorar a segurança e o desempenho.
- Cada sub-rede pode ter políticas e controles específicos.

---

### **Endereços IP Reservados**

Em cada sub-rede, certos endereços IP são reservados e não podem ser usados para hosts.

- **Endereço de Rede**: Primeiro endereço do bloco (todos os bits de host em 0).
- **Endereço de Broadcast**: Último endereço do bloco (todos os bits de host em 1).
- **Endereços Reservados pela AWS**:
  - **Comunicação Interna**: `10.0.0.1`
  - **Serviços de DNS**: `10.0.0.2`
  - **Uso Futuro**: `10.0.0.3`

**Exemplo em uma Sub-rede `/24` (`10.0.0.0/24`):**

- **Endereços Reservados**:
  - `10.0.0.0`: Endereço de rede.
  - `10.0.0.255`: Endereço de broadcast.
- **Endereços Disponíveis para Hosts**:
  - De `10.0.0.4` a `10.0.0.254`.

---

### **Tipos de Endereços IP Públicos**

#### **Endereço IPv4 Público**

- **Atribuição Automática**: Configurada para que instâncias recebam um IP público ao serem iniciadas.
- **Atribuição Manual**: Através de **Endereços IP Elásticos**.

#### **Endereço IP Elástico (EIP)**

- Endereço IPv4 estático público associado à sua conta AWS.
- Pode ser associado e remapeado entre instâncias ou interfaces de rede.
- Útil para mascarar falhas de instâncias, remapeando rapidamente o endereço para uma instância em funcionamento.
- **Custos**:
  - Podem ocorrer cobranças se o EIP não estiver associado a uma instância em execução.

---

### **Interface de Rede Elástica**

Uma **Interface de Rede Elástica (ENI)** é uma interface de rede virtual que pode ser:

- **Anexada** a uma instância.
- **Desanexada** e reanexada a outra instância, permitindo flexibilidade e redirecionamento de tráfego.
- **Atributos Mantidos**:
  - Endereços IP privados.
  - Endereços IP elásticos (se houver).
  - Grupos de segurança.
  - DNS.

Cada instância possui uma interface de rede primária. É possível criar interfaces adicionais e anexá-las conforme necessário, dependendo do tipo da instância.

---

### **Rotas e Tabelas de Rotas**

As **Tabelas de Rotas** definem como o tráfego de rede é direcionado dentro da VPC.

- **Rota Local**:
  - Presente por padrão.
  - Permite comunicação dentro da VPC.
  - **Não pode ser removida**.

- **Rotas Personalizadas**:
  - Podem ser adicionadas para direcionar tráfego para fora da VPC, como para a internet ou outras redes.
  - **Destinos**: Especificam o bloco de endereços IP de destino (por exemplo, `0.0.0.0/0` para toda a internet).
  - **Alvos**: Especificam para onde enviar o tráfego (por exemplo, um **Internet Gateway** ou **NAT Gateway**).

**Associação de Tabelas de Rotas:**

- Cada sub-rede deve estar associada a uma tabela de rotas.
- Se uma sub-rede não for associada explicitamente a uma tabela de rotas, ela usará a tabela de rotas principal da VPC.

---

## **Principais Lições da Seção 1**

- **Redes de Computadores**: Conectam dispositivos para comunicação e compartilhamento de recursos.
- **Endereços IP**: Identificadores únicos para dispositivos na rede; podem ser IPv4 ou IPv6.
- **CIDR**: Método para definir blocos de endereços IP e tamanhos de rede.
- **Modelo OSI**: Estrutura em camadas que descreve a comunicação em redes.
- **Sub-redes**: Divisões lógicas dentro de uma rede para melhor gerenciamento e segurança.
- **Endereços IP Reservados**: Certos endereços em uma sub-rede são reservados e não podem ser usados por dispositivos.
- **Tipos de Endereços IP Públicos**: Incluem endereços IP públicos atribuídos automaticamente e Endereços IP Elásticos.
- **Interface de Rede Elástica**: Permite flexibilidade na gestão de interfaces de rede e endereços IP.
- **Tabelas de Rotas**: Controlam o fluxo de tráfego dentro e fora da VPC.

---

## **Referências para Estudo Adicional**

- **Documentação AWS sobre Amazon VPC**:
  - [O que é Amazon VPC?](https://docs.aws.amazon.com/pt_br/vpc/latest/userguide/what-is-amazon-vpc.html)
- **Conceitos de Redes**:
  - **Endereçamento IP e Sub-redes**:
    - [Conceitos Básicos de Sub-redes](https://www.techtudo.com.br/artigos/noticia/2016/08/entenda-o-que-e-sub-rede-e-para-que-serve.html)
  - **Modelo OSI**:
    - [As Sete Camadas do Modelo OSI](https://www.redesdamais.com.br/as-sete-camadas-do-modelo-osi/)

---

## **Conclusão**

Compreender os fundamentos de redes é crucial para projetar e implementar infraestruturas eficientes e seguras na nuvem. Os conceitos abordados nesta seção servem como base para as próximas etapas, onde aplicaremos esse conhecimento na configuração de redes virtuais com o Amazon VPC, explorando suas funcionalidades e benefícios.

---

# **Próximos Passos**

- **Seção 2: Amazon VPC**
  - Exploraremos como criar redes virtuais na nuvem usando o Amazon VPC.
  - Aprenderemos sobre sub-redes públicas e privadas, gateways e tabelas de rotas.
- **Seção 3: Redes da VPC**
  - Veremos as diferentes opções de conectividade e como expandir nossas redes.
- **Seção 4: Segurança da VPC**
  - Entenderemos como proteger nossas redes usando grupos de segurança e ACLs de rede.

---

Aprofundar-se nesses conceitos permitirá que você projete arquiteturas de rede robustas e seguras, atendendo às necessidades específicas de aplicações modernas e escaláveis.

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
