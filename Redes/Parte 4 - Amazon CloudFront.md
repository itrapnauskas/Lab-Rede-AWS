# **Seção 4: Amazon CloudFront**

## **Introdução**

Nesta seção, aprenderemos sobre o **Amazon CloudFront**, o serviço de Content Delivery Network (CDN) da AWS. O CloudFront acelera a distribuição de conteúdo, como sites, vídeos, aplicativos e APIs, ao entregá-los a partir de localizações mais próximas do usuário final. Ele é projetado para oferecer baixa latência, alta transferência e segurança integrada, garantindo uma experiência de usuário otimizada para aplicações globais.

---

### **1. O que é Amazon CloudFront?**

O **Amazon CloudFront** é um serviço de CDN que distribui conteúdo através de uma rede global de **pontos de presença** (edge locations). Ele reduz a latência ao armazenar cópias do conteúdo em locais mais próximos aos usuários, diminuindo a distância física entre o usuário e os servidores de origem.

#### **Características Principais**

- **Rede Global**: Com centenas de pontos de presença em todo o mundo, o CloudFront garante cobertura ampla para usuários globais.
- **Baixa Latência**: Conteúdo é entregue de locais próximos ao usuário, reduzindo atrasos.
- **Compatibilidade com Diversos Tipos de Conteúdo**:
  - Arquivos estáticos (HTML, CSS, imagens, vídeos).
  - APIs dinâmicas.
  - Fluxos de vídeo em tempo real.
- **Integração com AWS**:
  - Trabalha de forma nativa com serviços como Amazon S3, EC2 e Elastic Load Balancer.
- **Segurança**:
  - Proteção contra ataques DDoS integrada através do AWS Shield.
  - Integração com AWS Web Application Firewall (WAF) para proteção adicional.

---

### **2. Componentes do Amazon CloudFront**

#### **2.1 Distribuição (Distribution)**

Uma **distribuição** é a configuração do CloudFront que define como o conteúdo será entregue aos usuários. Existem dois tipos principais:

1. **Web Distribution**:
   - Projetada para sites, APIs REST e streaming de arquivos.
2. **RTMP Distribution** (descontinuado para novas distribuições):
   - Para streaming de mídia usando o protocolo RTMP.

#### **2.2 Origem (Origin)**

O **servidor de origem** é a fonte do conteúdo entregue pelo CloudFront. Pode ser:

- **Amazon S3**: Para hospedar arquivos estáticos.
- **Amazon EC2 ou Elastic Load Balancer**: Para aplicações dinâmicas.
- **Servidores On-premises**: Para integrar conteúdo fora da AWS.

#### **2.3 Pontos de Presença (Edge Locations)**

Os **pontos de presença** são os locais físicos onde o CloudFront armazena conteúdo em cache para entrega rápida aos usuários. Eles atuam como intermediários entre o servidor de origem e o cliente.

#### **2.4 Cache e Time-to-Live (TTL)**

- **Cache**: O CloudFront armazena o conteúdo em cache nos pontos de presença.
- **TTL (Time-to-Live)**: Define quanto tempo um conteúdo permanece no cache antes de ser atualizado da origem.

---

### **3. Funcionalidades do Amazon CloudFront**

#### **3.1 Cache Dinâmico e Estático**

- **Conteúdo Estático**:
  - Arquivos como imagens, vídeos, documentos.
  - Permanece em cache por períodos definidos pelo TTL.
- **Conteúdo Dinâmico**:
  - APIs ou dados que mudam frequentemente.
  - O CloudFront pode utilizar lógica personalizada para decidir o que armazenar em cache.

#### **3.2 Suporte para HTTPS**

- **SSL/TLS Integrado**: Garante a entrega segura do conteúdo.
- **Certificados Personalizados**: Suporte para usar certificados SSL/TLS gerenciados pelo AWS Certificate Manager (ACM).

#### **3.3 Compressão Automática**

O CloudFront reduz automaticamente o tamanho de arquivos como HTML, CSS e JavaScript, utilizando compressão gzip ou Brotli.

#### **3.4 Regras de Restrição de Acesso**

- **Assinaturas de URL**: Permitem restringir o acesso ao conteúdo com base em tempo ou localização.
- **Georestrição**: Permite ou bloqueia o acesso a conteúdo com base na localização geográfica dos usuários.

#### **3.5 Integração com AWS Shield e AWS WAF**

- **AWS Shield**: Proteção contra ataques DDoS.
- **AWS WAF**: Filtra tráfego malicioso com base em regras personalizadas.

#### **3.6 Log de Acesso e Monitoramento**

- **Logs de Acesso**: Detalham cada solicitação feita ao CloudFront.
- **Amazon CloudWatch**: Monitora métricas de desempenho, como taxas de acerto de cache e latência.

---

### **4. Configuração de uma Distribuição CloudFront**

#### **4.1 Criando uma Distribuição**

1. **Origem**:
   - Escolha o servidor de origem (ex.: bucket do Amazon S3 ou servidor EC2).
2. **Configurações do Cache**:
   - Defina políticas de cache, incluindo TTL.
3. **HTTPS**:
   - Configure SSL/TLS usando certificados do ACM ou externos.
4. **Distribuição de Tráfego**:
   - Configure restrições geográficas ou assinaturas de URL, se necessário.

#### **4.2 Integrando com o Amazon S3**

- Habilite a **opção de entrega de conteúdo estático** no bucket do S3.
- Crie uma política de cache para otimizar o desempenho.
- Configure políticas de acesso para garantir que somente o CloudFront possa acessar o S3.

---

### **5. Benefícios do Amazon CloudFront**

- **Desempenho Aprimorado**: Reduz a latência ao entregar conteúdo de pontos de presença próximos aos usuários.
- **Escalabilidade**: Lida com picos de tráfego sem comprometer o desempenho.
- **Segurança Integrada**: Protege contra ataques e tráfego malicioso.
- **Integração com Serviços AWS**: Trabalha perfeitamente com S3, EC2, WAF e outros serviços AWS.
- **Custo-Efetividade**: Reduz custos de transferência de dados ao diminuir a carga no servidor de origem.

---

### **6. Casos de Uso do Amazon CloudFront**

#### **6.1 Hospedagem de Sites Estáticos**

- **Desafio**: Acelerar o carregamento de sites com conteúdo estático.
- **Solução com CloudFront**:
  - Utilize o S3 como origem e configure uma distribuição CloudFront.
  - Ative a compressão automática para reduzir o tamanho dos arquivos.

#### **6.2 Streaming de Vídeo**

- **Desafio**: Entregar conteúdo de vídeo sem atrasos.
- **Solução com CloudFront**:
  - Configure o CloudFront para fazer cache de vídeos e otimize as configurações de TTL.
  - Use assinaturas de URL para restringir o acesso.

#### **6.3 Aplicações com APIs Globais**

- **Desafio**: Reduzir a latência para chamadas de API em múltiplas regiões.
- **Solução com CloudFront**:
  - Integre o CloudFront com seu endpoint de API.
  - Utilize o cache dinâmico para acelerar respostas comuns.

---

### **7. Preços do Amazon CloudFront**

- **Modelo de Pagamento**: Pague pelo uso com base no volume de dados transferidos, número de solicitações e invalidações de cache.
- **Componentes de Cobrança**:
  - **Transferência de Dados**: Da origem para os pontos de presença e dos pontos de presença para os usuários.
  - **Solicitações HTTP/HTTPS**: Número de requisições processadas.
  - **Invalidação de Cache**: Cobrança adicional por solicitações de invalidação de cache.
- **Detalhes**: Consulte a [página de preços do Amazon CloudFront](https://aws.amazon.com/cloudfront/pricing/) para informações atualizadas.

---

### **8. Boas Práticas com Amazon CloudFront**

- **Configuração de Políticas de Cache**: Ajuste o TTL com base na natureza do conteúdo (estático ou dinâmico).
- **Uso de HTTPS**: Garanta que todas as entregas de conteúdo utilizem HTTPS para maior segurança.
- **Monitoramento Regular**:
  - Utilize logs e o CloudWatch para acompanhar o desempenho e o uso.
- **Restrição de Acesso**:
  - Use assinaturas de URL para controlar o acesso ao conteúdo sensível.
  - Ative a georestrição para atender a requisitos legais ou de negócios.

---

