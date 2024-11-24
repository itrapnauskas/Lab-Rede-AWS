# **Desafio**

## **Descrição do Laboratório**
Os alunos deverão projetar, implementar e testar uma **Amazon VPC** com sub-redes públicas e privadas, seguindo as diretrizes abaixo.

### **Cenário**
Você é responsável por configurar a infraestrutura de uma pequena empresa. A empresa possui um site público e um banco de dados que deve ser mantido privado. Sua tarefa é criar uma arquitetura de rede que atenda aos seguintes requisitos:
- O site deve estar em uma sub-rede pública.
- O banco de dados deve estar em uma sub-rede privada.
- Os recursos privados devem acessar a internet via NAT Gateway para atualizações de segurança.

---

### **Tarefas**
1. **Criar a Amazon VPC**
   - Bloco CIDR: `10.0.0.0/16`.
2. **Configurar Sub-redes**
   - Sub-rede Pública 1: `10.0.0.0/24`.
   - Sub-rede Privada 1: `10.0.1.0/24`.
3. **Configurar Segurança**
   - Criar grupos de segurança para:
     - Permitir tráfego HTTP (porta 80) para o servidor web.
     - Permitir comunicação interna entre instâncias.
4. **Iniciar Recursos**
   - Lançar uma instância EC2 na sub-rede pública para o servidor web.
   - Lançar uma instância EC2 na sub-rede privada para o banco de dados.
5. **Testar**
   - Acessar o servidor web pela internet.
   - Garantir que a instância privada acesse a internet para atualizações.

---

