# **Seção 2: Amazon VPC**

## **Introdução**

Nesta seção, varemos o **Amazon Virtual Private Cloud (Amazon VPC)**, serviço essencial da AWS que permite criar redes virtuais isoladas logicamente na nuvem. Controle total sobre o ambiente de rede, incluindo a seleção do intervalo de endereços IP, criação de sub-redes, configuração de tabelas de rotas e gateways de rede. 

---

### **O que é Amazon VPC?**

O **Amazon Virtual Private Cloud (Amazon VPC)** é um serviço que permite provisionar uma seção isolada logicamente da **Nuvem AWS**, onde você pode executar recursos da AWS em uma rede virtual definida por você. O Amazon VPC oferece controle completo sobre o ambiente de rede virtual, incluindo:

- **Seleção do intervalo de endereços IP**: Você define o bloco CIDR (Classless Inter-Domain Routing) da VPC.
- **Criação de sub-redes**: Segmentação da rede em sub-redes públicas e privadas.
- **Configuração de tabelas de rotas e gateways**: Controle sobre o roteamento de tráfego dentro e fora da VPC.
- **Segurança**: Utilização de grupos de segurança e listas de controle de acesso à rede (ACLs de rede) para gerenciar o acesso aos recursos.

**Benefícios do Amazon VPC**:

- **Isolamento Lógico**: As VPCs são isoladas umas das outras dentro da nuvem AWS.
- **Controle e Flexibilidade**: Personalize a configuração de rede para atender às necessidades específicas da sua aplicação.
- **Segurança**: Implementação de múltiplas camadas de segurança para proteger seus recursos.

---

### **Componentes Fundamentais da Amazon VPC**

#### **1. VPCs e Sub-redes**

- **VPC (Virtual Private Cloud)**:
  - Uma rede virtual isolada logicamente dentro da AWS.
  - Pertence a uma única **Região AWS**.
  - Pode abranger múltiplas **Zonas de Disponibilidade (Availability Zones)**.

- **Sub-redes**:
  - Dividem a VPC em segmentos menores.
  - Cada sub-rede está contida em uma única Zona de Disponibilidade.
  - Podem ser classificadas como **públicas** (com acesso à internet) ou **privadas** (sem acesso direto à internet).

**Exemplo de Arquitetura de VPC e Sub-redes**:

```
                Região AWS
                 |
            -----------------
            |               |
      Zona de Disp. A  Zona de Disp. B
            |               |
        Sub-rede A       Sub-rede B
```

#### **2. Endereçamento IP na VPC**

Ao criar uma VPC, você deve definir um bloco CIDR IPv4, que especifica o intervalo de endereços IP privados disponíveis na rede. Alguns pontos importantes:

- **Tamanho do Bloco CIDR**:
  - **Máximo**: `/16` (65.536 endereços IP).
  - **Mínimo**: `/28` (16 endereços IP).
- **Sub-redes**:
  - Cada sub-rede recebe um bloco CIDR que é um subconjunto do bloco CIDR da VPC.
  - Os blocos CIDR das sub-redes **não podem se sobrepor**.
- **IPv6**:
  - Opcionalmente, você pode associar um bloco CIDR IPv6 à VPC e às sub-redes.

#### **3. Endereços IP Reservados**

Em cada sub-rede, a AWS reserva cinco endereços IP que não estão disponíveis para uso:

- **Endereço de rede**: Primeiro endereço do bloco (ex.: `10.0.0.0`).
- **Endereço de roteador local**: Para comunicação interna (ex.: `10.0.0.1`).
- **Endereço para resolução DNS**: (ex.: `10.0.0.2`).
- **Endereço reservado para uso futuro**: (ex.: `10.0.0.3`).
- **Endereço de broadcast**: Último endereço do bloco (ex.: `10.0.0.255`).

**Exemplo**:

- Sub-rede: `10.0.0.0/24` (256 endereços IP).
- Endereços disponíveis para instâncias: 251 (de `10.0.0.4` a `10.0.0.254`).

---

### **Tipos de Endereços IP Públicos**

#### **1. Endereço IPv4 Público**

- **Atribuído automaticamente**: Ao iniciar uma instância em uma sub-rede com atribuição automática de IP público habilitada.
- **Utilizado para permitir que instâncias em sub-redes públicas se comuniquem com a internet**.

#### **2. Endereço IP Elástico (Elastic IP)**

- **Endereço IPv4 público estático**.
- **Associado à sua conta AWS**.
- **Pode ser associado ou dissociado de instâncias ou interfaces de rede a qualquer momento**.
- **Uso típico**: Manter um endereço IP público fixo para uma instância, mesmo que a instância seja parada ou substituída.

**Considerações**:

- **Custos**: Podem ser cobrados se o EIP estiver alocado, mas não associado a uma instância em execução.
- **Limites**: O número de EIPs que você pode alocar é limitado por região.

---

### **Interface de Rede Elástica (Elastic Network Interface - ENI)**

- **Definição**: Interface de rede virtual que pode ser anexada ou separada de uma instância em uma VPC.
- **Funcionalidades**:
  - **Flexibilidade**: Mover uma ENI entre instâncias para redirecionar o tráfego de rede.
  - **Atributos Mantidos**: Endereços IP privados, EIPs, grupos de segurança e configurações de DNS.
- **Uso Comum**:
  - **Alta Disponibilidade**: Em caso de falha de uma instância, a ENI pode ser movida para outra instância de backup.
  - **Gerenciamento de Rede**: Segmentar funções de rede entre diferentes ENIs.

---

### **Tabelas de Rotas e Rotas**

#### **1. Tabelas de Rotas**

- **Definição**: Conjunto de regras que determinam para onde o tráfego de rede é direcionado.
- **Composição**:
  - **Destinos**: Blocos CIDR que especificam o tráfego de destino.
  - **Alvos**: O caminho ou dispositivo pelo qual o tráfego deve ser roteado (ex.: internet gateway, NAT gateway).
- **Associações**:
  - Cada sub-rede deve estar associada a uma tabela de rotas (pode ser a tabela principal ou uma personalizada).
  - Uma tabela de rotas pode ser associada a múltiplas sub-redes.

#### **2. Rotas**

- **Rota Local**:
  - Presente por padrão em todas as tabelas de rotas.
  - Permite comunicação dentro da VPC (ex.: `10.0.0.0/16` alvo `local`).
- **Rotas Personalizadas**:
  - Definidas pelo usuário para direcionar tráfego para fora da VPC.
  - **Exemplo**:
    - **Destino**: `0.0.0.0/0` (todo o tráfego não local).
    - **Alvo**: `igw-id` (Internet Gateway) ou `nat-gw-id` (NAT Gateway).

---

### **Gateways na Amazon VPC**

#### **1. Internet Gateway**

- **Definição**: Componente da VPC que permite comunicação entre instâncias na VPC e a internet.
- **Funções**:
  - **Ponto de entrada e saída**: Para tráfego de internet.
  - **Conversão de Endereços de Rede (NAT)**: Para instâncias com endereços IPv4 públicos.
- **Configuração**:
  - Anexar o Internet Gateway à VPC.
  - Atualizar a tabela de rotas da sub-rede pública para direcionar o tráfego não local (`0.0.0.0/0`) para o Internet Gateway.

#### **2. NAT Gateway**

- **Definição**: Serviço gerenciado que permite que instâncias em sub-redes privadas acessem a internet, mantendo-se inacessíveis a partir dela.
- **Uso**:
  - **Atualizações e Patches**: Instâncias privadas podem baixar atualizações de segurança.
  - **Serviços AWS**: Acesso a serviços públicos da AWS que requerem conexão à internet.
- **Configuração**:
  - Criar o NAT Gateway em uma sub-rede pública.
  - Associar um EIP ao NAT Gateway.
  - Atualizar a tabela de rotas da sub-rede privada para direcionar o tráfego não local para o NAT Gateway.

---

### **Opções de Conectividade Avançadas**

#### **1. Peering de VPC**

- **Definição**: Conexão de rede entre duas VPCs que permite rotear tráfego de forma privada entre elas.
- **Características**:
  - **Conexão ponto a ponto**: Instâncias em VPCs emparelhadas podem se comunicar como se estivessem na mesma rede.
  - **Entre contas e regiões**: Pode ser estabelecido entre VPCs na mesma conta, em contas diferentes ou até em regiões diferentes.
- **Restrições**:
  - Os blocos CIDR das VPCs não podem se sobrepor.
  - O emparelhamento não é transitivo (se A está emparelhada com B, e B com C, A não se comunica com C automaticamente).

#### **2. AWS Site-to-Site VPN**

- **Definição**: Conexão segura entre uma VPC e uma rede remota (como um data center corporativo) através da internet pública.
- **Componentes**:
  - **Gateway de Cliente**: Representa o dispositivo físico ou software no local.
  - **Gateway Virtual Privado (VGW)**: Dispositivo virtual na VPC que estabelece a conexão VPN.
- **Uso**:
  - Estender a rede on-premises para a nuvem.
  - Comunicação segura entre recursos na VPC e a infraestrutura local.

#### **3. AWS Direct Connect**

- **Definição**: Serviço que estabelece uma conexão de rede dedicada e privada entre sua rede on-premises e a AWS.
- **Benefícios**:
  - **Baixa Latência**: Conexão direta reduz o tempo de resposta.
  - **Largura de Banda Consistente**: Melhor desempenho para transferências de dados.
  - **Confiabilidade**: Menor dependência da internet pública.

---

### **Segurança na Amazon VPC**

A segurança é um aspecto crítico na configuração da VPC. Duas ferramentas principais são usadas para controlar o acesso e proteger os recursos:

#### **1. Grupos de Segurança (Security Groups)**

- **Nível**: Instância.
- **Função**: Atua como um firewall virtual para instâncias, controlando tráfego de entrada e saída.
- **Características**:
  - **Stateful**: Respostas ao tráfego permitido são automaticamente permitidas.
  - **Regras**:
    - Podem permitir tráfego (não podem negar).
    - Avaliadas antes de permitir ou negar o tráfego.

#### **2. Listas de Controle de Acesso à Rede (Network ACLs)**

- **Nível**: Sub-rede.
- **Função**: Atua como uma camada adicional de segurança, controlando o tráfego de entrada e saída de sub-redes.
- **Características**:
  - **Stateless**: Respostas ao tráfego permitido devem ser explicitamente permitidas.
  - **Regras**:
    - Podem permitir ou negar tráfego.
    - Avaliadas em ordem numérica.

---

### **Principais Lições da Seção 2**

- **Amazon VPC** permite criar redes virtuais isoladas dentro da AWS, oferecendo controle total sobre o ambiente de rede.
- **VPCs e Sub-redes**:
  - VPCs pertencem a uma única região e podem abranger múltiplas zonas de disponibilidade.
  - Sub-redes dividem a VPC e são atribuídas a zonas de disponibilidade específicas.
- **Endereçamento IP**:
  - Escolha cuidadosa do bloco CIDR é crucial, pois não pode ser alterado após a criação.
  - Sub-redes não podem ter blocos CIDR sobrepostos.
- **Gateways**:
  - **Internet Gateway** conecta sub-redes públicas à internet.
  - **NAT Gateway** permite que sub-redes privadas acessem a internet de forma segura.
- **Segurança**:
  - **Grupos de Segurança** controlam o tráfego em nível de instância.
  - **Network ACLs** controlam o tráfego em nível de sub-rede.
- **Conectividade Avançada**:
  - **Peering de VPC** permite comunicação entre VPCs diferentes.
  - **AWS Site-to-Site VPN** e **AWS Direct Connect** oferecem opções para conectar redes on-premises à nuvem AWS.

---
