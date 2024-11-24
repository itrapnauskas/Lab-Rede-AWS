# **Se��o 2: Amazon VPC**

## **Introdu��o**

Nesta se��o, varemos o **Amazon Virtual Private Cloud (Amazon VPC)**, servi�o essencial da AWS que permite criar redes virtuais isoladas logicamente na nuvem. Controle total sobre o ambiente de rede, incluindo a sele��o do intervalo de endere�os IP, cria��o de sub-redes, configura��o de tabelas de rotas e gateways de rede. 

---

### **O que � Amazon VPC?**

O **Amazon Virtual Private Cloud (Amazon VPC)** � um servi�o que permite provisionar uma se��o isolada logicamente da **Nuvem AWS**, onde voc� pode executar recursos da AWS em uma rede virtual definida por voc�. O Amazon VPC oferece controle completo sobre o ambiente de rede virtual, incluindo:

- **Sele��o do intervalo de endere�os IP**: Voc� define o bloco CIDR (Classless Inter-Domain Routing) da VPC.
- **Cria��o de sub-redes**: Segmenta��o da rede em sub-redes p�blicas e privadas.
- **Configura��o de tabelas de rotas e gateways**: Controle sobre o roteamento de tr�fego dentro e fora da VPC.
- **Seguran�a**: Utiliza��o de grupos de seguran�a e listas de controle de acesso � rede (ACLs de rede) para gerenciar o acesso aos recursos.

**Benef�cios do Amazon VPC**:

- **Isolamento L�gico**: As VPCs s�o isoladas umas das outras dentro da nuvem AWS.
- **Controle e Flexibilidade**: Personalize a configura��o de rede para atender �s necessidades espec�ficas da sua aplica��o.
- **Seguran�a**: Implementa��o de m�ltiplas camadas de seguran�a para proteger seus recursos.

---

### **Componentes Fundamentais da Amazon VPC**

#### **1. VPCs e Sub-redes**

- **VPC (Virtual Private Cloud)**:
  - Uma rede virtual isolada logicamente dentro da AWS.
  - Pertence a uma �nica **Regi�o AWS**.
  - Pode abranger m�ltiplas **Zonas de Disponibilidade (Availability Zones)**.

- **Sub-redes**:
  - Dividem a VPC em segmentos menores.
  - Cada sub-rede est� contida em uma �nica Zona de Disponibilidade.
  - Podem ser classificadas como **p�blicas** (com acesso � internet) ou **privadas** (sem acesso direto � internet).

**Exemplo de Arquitetura de VPC e Sub-redes**:

```
                Regi�o AWS
                 |
            -----------------
            |               |
      Zona de Disp. A  Zona de Disp. B
            |               |
        Sub-rede A       Sub-rede B
```

#### **2. Endere�amento IP na VPC**

Ao criar uma VPC, voc� deve definir um bloco CIDR IPv4, que especifica o intervalo de endere�os IP privados dispon�veis na rede. Alguns pontos importantes:

- **Tamanho do Bloco CIDR**:
  - **M�ximo**: `/16` (65.536 endere�os IP).
  - **M�nimo**: `/28` (16 endere�os IP).
- **Sub-redes**:
  - Cada sub-rede recebe um bloco CIDR que � um subconjunto do bloco CIDR da VPC.
  - Os blocos CIDR das sub-redes **n�o podem se sobrepor**.
- **IPv6**:
  - Opcionalmente, voc� pode associar um bloco CIDR IPv6 � VPC e �s sub-redes.

#### **3. Endere�os IP Reservados**

Em cada sub-rede, a AWS reserva cinco endere�os IP que n�o est�o dispon�veis para uso:

- **Endere�o de rede**: Primeiro endere�o do bloco (ex.: `10.0.0.0`).
- **Endere�o de roteador local**: Para comunica��o interna (ex.: `10.0.0.1`).
- **Endere�o para resolu��o DNS**: (ex.: `10.0.0.2`).
- **Endere�o reservado para uso futuro**: (ex.: `10.0.0.3`).
- **Endere�o de broadcast**: �ltimo endere�o do bloco (ex.: `10.0.0.255`).

**Exemplo**:

- Sub-rede: `10.0.0.0/24` (256 endere�os IP).
- Endere�os dispon�veis para inst�ncias: 251 (de `10.0.0.4` a `10.0.0.254`).

---

### **Tipos de Endere�os IP P�blicos**

#### **1. Endere�o IPv4 P�blico**

- **Atribu�do automaticamente**: Ao iniciar uma inst�ncia em uma sub-rede com atribui��o autom�tica de IP p�blico habilitada.
- **Utilizado para permitir que inst�ncias em sub-redes p�blicas se comuniquem com a internet**.

#### **2. Endere�o IP El�stico (Elastic IP)**

- **Endere�o IPv4 p�blico est�tico**.
- **Associado � sua conta AWS**.
- **Pode ser associado ou dissociado de inst�ncias ou interfaces de rede a qualquer momento**.
- **Uso t�pico**: Manter um endere�o IP p�blico fixo para uma inst�ncia, mesmo que a inst�ncia seja parada ou substitu�da.

**Considera��es**:

- **Custos**: Podem ser cobrados se o EIP estiver alocado, mas n�o associado a uma inst�ncia em execu��o.
- **Limites**: O n�mero de EIPs que voc� pode alocar � limitado por regi�o.

---

### **Interface de Rede El�stica (Elastic Network Interface - ENI)**

- **Defini��o**: Interface de rede virtual que pode ser anexada ou separada de uma inst�ncia em uma VPC.
- **Funcionalidades**:
  - **Flexibilidade**: Mover uma ENI entre inst�ncias para redirecionar o tr�fego de rede.
  - **Atributos Mantidos**: Endere�os IP privados, EIPs, grupos de seguran�a e configura��es de DNS.
- **Uso Comum**:
  - **Alta Disponibilidade**: Em caso de falha de uma inst�ncia, a ENI pode ser movida para outra inst�ncia de backup.
  - **Gerenciamento de Rede**: Segmentar fun��es de rede entre diferentes ENIs.

---

### **Tabelas de Rotas e Rotas**

#### **1. Tabelas de Rotas**

- **Defini��o**: Conjunto de regras que determinam para onde o tr�fego de rede � direcionado.
- **Composi��o**:
  - **Destinos**: Blocos CIDR que especificam o tr�fego de destino.
  - **Alvos**: O caminho ou dispositivo pelo qual o tr�fego deve ser roteado (ex.: internet gateway, NAT gateway).
- **Associa��es**:
  - Cada sub-rede deve estar associada a uma tabela de rotas (pode ser a tabela principal ou uma personalizada).
  - Uma tabela de rotas pode ser associada a m�ltiplas sub-redes.

#### **2. Rotas**

- **Rota Local**:
  - Presente por padr�o em todas as tabelas de rotas.
  - Permite comunica��o dentro da VPC (ex.: `10.0.0.0/16` alvo `local`).
- **Rotas Personalizadas**:
  - Definidas pelo usu�rio para direcionar tr�fego para fora da VPC.
  - **Exemplo**:
    - **Destino**: `0.0.0.0/0` (todo o tr�fego n�o local).
    - **Alvo**: `igw-id` (Internet Gateway) ou `nat-gw-id` (NAT Gateway).

---

### **Gateways na Amazon VPC**

#### **1. Internet Gateway**

- **Defini��o**: Componente da VPC que permite comunica��o entre inst�ncias na VPC e a internet.
- **Fun��es**:
  - **Ponto de entrada e sa�da**: Para tr�fego de internet.
  - **Convers�o de Endere�os de Rede (NAT)**: Para inst�ncias com endere�os IPv4 p�blicos.
- **Configura��o**:
  - Anexar o Internet Gateway � VPC.
  - Atualizar a tabela de rotas da sub-rede p�blica para direcionar o tr�fego n�o local (`0.0.0.0/0`) para o Internet Gateway.

#### **2. NAT Gateway**

- **Defini��o**: Servi�o gerenciado que permite que inst�ncias em sub-redes privadas acessem a internet, mantendo-se inacess�veis a partir dela.
- **Uso**:
  - **Atualiza��es e Patches**: Inst�ncias privadas podem baixar atualiza��es de seguran�a.
  - **Servi�os AWS**: Acesso a servi�os p�blicos da AWS que requerem conex�o � internet.
- **Configura��o**:
  - Criar o NAT Gateway em uma sub-rede p�blica.
  - Associar um EIP ao NAT Gateway.
  - Atualizar a tabela de rotas da sub-rede privada para direcionar o tr�fego n�o local para o NAT Gateway.

---

### **Op��es de Conectividade Avan�adas**

#### **1. Peering de VPC**

- **Defini��o**: Conex�o de rede entre duas VPCs que permite rotear tr�fego de forma privada entre elas.
- **Caracter�sticas**:
  - **Conex�o ponto a ponto**: Inst�ncias em VPCs emparelhadas podem se comunicar como se estivessem na mesma rede.
  - **Entre contas e regi�es**: Pode ser estabelecido entre VPCs na mesma conta, em contas diferentes ou at� em regi�es diferentes.
- **Restri��es**:
  - Os blocos CIDR das VPCs n�o podem se sobrepor.
  - O emparelhamento n�o � transitivo (se A est� emparelhada com B, e B com C, A n�o se comunica com C automaticamente).

#### **2. AWS Site-to-Site VPN**

- **Defini��o**: Conex�o segura entre uma VPC e uma rede remota (como um data center corporativo) atrav�s da internet p�blica.
- **Componentes**:
  - **Gateway de Cliente**: Representa o dispositivo f�sico ou software no local.
  - **Gateway Virtual Privado (VGW)**: Dispositivo virtual na VPC que estabelece a conex�o VPN.
- **Uso**:
  - Estender a rede on-premises para a nuvem.
  - Comunica��o segura entre recursos na VPC e a infraestrutura local.

#### **3. AWS Direct Connect**

- **Defini��o**: Servi�o que estabelece uma conex�o de rede dedicada e privada entre sua rede on-premises e a AWS.
- **Benef�cios**:
  - **Baixa Lat�ncia**: Conex�o direta reduz o tempo de resposta.
  - **Largura de Banda Consistente**: Melhor desempenho para transfer�ncias de dados.
  - **Confiabilidade**: Menor depend�ncia da internet p�blica.

---

### **Seguran�a na Amazon VPC**

A seguran�a � um aspecto cr�tico na configura��o da VPC. Duas ferramentas principais s�o usadas para controlar o acesso e proteger os recursos:

#### **1. Grupos de Seguran�a (Security Groups)**

- **N�vel**: Inst�ncia.
- **Fun��o**: Atua como um firewall virtual para inst�ncias, controlando tr�fego de entrada e sa�da.
- **Caracter�sticas**:
  - **Stateful**: Respostas ao tr�fego permitido s�o automaticamente permitidas.
  - **Regras**:
    - Podem permitir tr�fego (n�o podem negar).
    - Avaliadas antes de permitir ou negar o tr�fego.

#### **2. Listas de Controle de Acesso � Rede (Network ACLs)**

- **N�vel**: Sub-rede.
- **Fun��o**: Atua como uma camada adicional de seguran�a, controlando o tr�fego de entrada e sa�da de sub-redes.
- **Caracter�sticas**:
  - **Stateless**: Respostas ao tr�fego permitido devem ser explicitamente permitidas.
  - **Regras**:
    - Podem permitir ou negar tr�fego.
    - Avaliadas em ordem num�rica.

---

### **Principais Li��es da Se��o 2**

- **Amazon VPC** permite criar redes virtuais isoladas dentro da AWS, oferecendo controle total sobre o ambiente de rede.
- **VPCs e Sub-redes**:
  - VPCs pertencem a uma �nica regi�o e podem abranger m�ltiplas zonas de disponibilidade.
  - Sub-redes dividem a VPC e s�o atribu�das a zonas de disponibilidade espec�ficas.
- **Endere�amento IP**:
  - Escolha cuidadosa do bloco CIDR � crucial, pois n�o pode ser alterado ap�s a cria��o.
  - Sub-redes n�o podem ter blocos CIDR sobrepostos.
- **Gateways**:
  - **Internet Gateway** conecta sub-redes p�blicas � internet.
  - **NAT Gateway** permite que sub-redes privadas acessem a internet de forma segura.
- **Seguran�a**:
  - **Grupos de Seguran�a** controlam o tr�fego em n�vel de inst�ncia.
  - **Network ACLs** controlam o tr�fego em n�vel de sub-rede.
- **Conectividade Avan�ada**:
  - **Peering de VPC** permite comunica��o entre VPCs diferentes.
  - **AWS Site-to-Site VPN** e **AWS Direct Connect** oferecem op��es para conectar redes on-premises � nuvem AWS.

---
