# ☁️ Infraestrutura e Alta Disponibilidade na AWS

## Princípios Fundamentais

- **Recursos descartáveis**: Prefira recriar recursos ao invés de recuperá-los
- **Infrastructure as Code (IaC)**: Gerencie toda infraestrutura através de código automatizado
- **Redundância**: Elimine pontos únicos de falha em todas as camadas

## Componentes Chave

### Load Balancer
- Distribui tráfego entre instâncias saudáveis
- Realiza health checks para monitoramento contínuo
- Requer redundância (múltiplos LBs em diferentes AZs)

### API Gateway
- Camada de proteção e gerenciamento para APIs
- Oferece throttling, caching e autenticação
- Desacoplado dos serviços backend para resiliência

## 🛢️ Estratégia de Bancos de Dados

### Bancos Relacionais (RDS)
- **Modelo**: Dados estruturados com schema rígido
- **Exemplos**: PostgreSQL, MySQL, Aurora
- **Escalabilidade**: Principalmente vertical (upgrade de instância)
- **Cenários ideais**: Transações ACID, relacionamentos complexos

### Bancos Não-Relacionais
- **Modelo**: Schemas flexíveis, alta performance
- **Tipos**:
  - DynamoDB (chave-valor)
  - Neptune (grafos)
  - Elasticache (cache in-memory)
- **Vantagens**: Escalabilidade horizontal automática

## 💰 Otimização de Custos

- **Mentalidade Frugal**: Projete pensando em custo-benefício
- **Estratégias**:
  - Cache (Reduz chamadas ao banco)
  - Lifecycle policies no S3
  - Seleção inteligente de classes de armazenamento
  - Uso de instâncias spot para workloads flexíveis

## 🔐 Arquitetura Segura

### Princípios Fundamentais
- **Serviços gerenciados**: Delegue segurança à AWS quando possível
- **Defesa em profundidade**: Múltiplas camadas de proteção
- **Menor privilégio**: Permissões mínimas necessárias
- **Modelo compartilhado**: AWS protege a infra, você protege seus dados

### Criptografia no S3 (SSE)
- **SSE-S3**: Criptografia gerenciada pela AWS (padrão)
- **SSE-KMS**: Controle granular com AWS Key Management Service
- **SSE-C**: Chaves gerenciadas pelo cliente

### Boas Práticas
- Autenticação forte (MFA obrigatório)
- Criptografia em trânsito (TLS) e em repouso
- Monitoramento contínuo com CloudTrail + Config
- Automatização de políticas de segurança

## 🗂️ Amazon S3 - Armazenamento em Nuvem

### Características Principais
- ✨ 99.999999999% de durabilidade (11 noves)
- ⚡ 99.99% disponibilidade
- 🔐 Criptografia ativada por padrão
- ∞ Armazenamento ilimitado por bucket

### Recursos Avançados
- **Versionamento**: Histórico completo de alterações
- **Lifecycle Rules**: Transição automática entre classes
- **CORS**: Controle de acesso entre origens diferentes
- **Multipart Upload**: Upload otimizado para arquivos grandes

```markdown
## 💻 EC2 - Computação Elástica

### Modelos de Instância
| Tipo | Descrição | Caso de Uso |
|------|-----------|-------------|
| On-Demand | Pago por uso | Workloads imprevisíveis |
| Reserved | Desconto por compromisso | Workloads estáveis |
| Spot | Lances por capacidade | Workloads tolerantes a falhas |

### Estratégias de Posicionamento
- **Cluster**: Alta performance (mesmo rack)
- **Spread**: Máxima disponibilidade (AZs distintas)
- **Partition**: Isolamento para workloads críticos

## 🧠 IAM - Gerenciamento de Acesso

### Modelos de Controle
- **RBAC (Role-Based)**: Permissões baseadas em funções
- **ABAC (Attribute-Based)**: Políticas dinâmicas por atributos
- **SCPs**: Restrições organizacionais globais

### Melhores Práticas
- Grupos ao invés de usuários individuais
- Políticas com mínimo privilégio necessário
- Credenciais temporárias para acesso programático

## 🌐 Arquitetura de Rede

### Componentes Essenciais
- **VPC**: Rede virtual privada na nuvem
- **Subnets**:
  - Públicas: Com acesso à Internet via IGW
  - Privadas: Acesso restrito via NAT Gateway
- **Security Groups**: Firewall stateful por instância
- **NACLs**: Filtro stateless por subnet

### Padrões de Conectividade
- **VPC Peering**: Conexão direta entre VPCs
- **Transit Gateway**: Hub central para múltiplas VPCs
- **Direct Connect**: Link dedicado ao data center

## 🛡️ Monitoramento e Governança

### Ferramentas Essenciais
- **CloudTrail**: Auditoria de chamadas API
- **Config**: Avaliação contínua de conformidade
- **CloudWatch**: Monitoramento unificado
- **GuardDuty**: Detecção inteligente de ameaças

### Governança em Escala
- **AWS Organizations**: Gestão centralizada de múltiplas contas
- **Control Tower**: Setup automatizado de landing zone bem projetado, da melhor forma possível
- **Cognito**: Gerenciamento de identidade para usuários finais

# Alta Disponibilidade

## CloudWatch

- **Logs**: ele mostra logs(pago)
- **Métrica**: Mostra as métrica(gratuito), gera gráficos e alarmes. Exemplo: Da um alerta se a CPU de um EC2 estiver acima de 70%

## EventBridge
- Barramentos de eventos em tempo real, jeito de monitor a AWS em tempo real
- Da para usar como broker de eventos

## AWS COST,



