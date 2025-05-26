# das2-2025

- Recursos são descartáveis, porque é so matar e criar um novo
- IAC = insfraestructure as a code

- Melhor prática -> colocar um load balancer para balancear a carga e não cair o recurso
- LoadBalancer tem o HealthCheck -> Ele verifica a "saúde" da máquina
- O que acontece ser cair o load balancer? multiplicidade do load balancer = "Alta disponibilidade requer redundancia"
- APIGATEAY -> é colocado antes do serviço para protege-lo
- Evitar pontos únicos de falha, por exemplo: se cair o banco, então cai a aplicação

# Escolher a solução de BD correta
- Relacional || Não relacional
  
- Relacional
   - Escalabilidade horizontal ruim, chega um ponto em que não da para botar mais servidor

- Não relacional
   - Performance extrema
   - Boa escalabilidade horizontal

# Otimização de dados
- Arquiteto frugal -> arquiteto mão de vaca(preocupado com o custo da aplicação)

- Otimização de custo
  -usar o cache

# Segurança

- Utilizar serviços gerenciados, porque a AWS se vira
- O ideal é não ter apenas uma ferramenta de segurança na empresa
- Principio do privilégio minimo -> só da permissão para o cara na responsabilidade dele

# Modelo de responsabilidade compartilhada
- A responsabiidade nunca é so do usuário ou só da aws, é dividida

# Server side encryption
- SSE-S3(DEFAULT) -> A AWS cuida da criptografia
- SS3-KMS -> Modelo de segurança que um objeto tem uma chave
- SSE-C -> Modelo de segurança que o usuário passa o objeto e a chave e segurança

# Principios de segurança AWS
- Implentar uma identidade forte
- Proteger dados em transito e em descanso
  -SSL/HTTPS : Forma de proteger os dados em transação
- Aplicar segurança em todas as camadas
- Manter pessoas longe do dados
- Ter rastreabilidade
- Preparar para eventos de segurança
- Automatizar melhores práticas de segurança, Ex: não criar usuário na mão

# Permissões para acessar recursos
- dar permissão ao usuário apenas sobre o que ele pode fazer

# S3

- NÃO É POSSÍVEL EDITAR UMA ARQUIVO DENTRO DO S3, ELE NÃO É UM SISTEMA DE GERENCIAMENTO DE ARQUIVOS
- A chance de não perder o objeto é 100% -> durabilidade
- A disponibilidade é de 99.99% mas da para melhorar se replicar o s3 para outro bucket
- Para ter alta disponibilidade tem que ter copia do bucket 
- Para que usar o S3? hospedar um site estático
- Não da para hospedar um monolito no S3
- Movendo dados para o S3: Não tem limites de objeto num bucket, precisa de permissão do bucket, Objetos são encriptados por padrão
- CLI -> aws s3 cp arquivoorigem s3://bucketdestino

- O Multipart Upload do AWS S3 é um método de upload que divide arquivos grandes em várias partes menores, enviando-as paralelamente para acelerar a transferência e melhorar a resiliência.
- AWS Direct Connect -> conexão mais poderosa com a aws OBS: Não é criptografado
- Object storage classes -> forma como o S3 guarda os arquivos, afeta diretamente preço e disponibilidade

# S3 Lifecycle

- O que é? Conjunto de regras que cria para transcionar ou expirar objetos, Ex: depois de 7 anos apague, depois de 2 anos mova para o s3 glacier

# S3 versionamento

- Todo balde nasce com o versionamento desligado
- Depois que ligar o versionamento, não pode retirar, só pausar
- Algumas funcionalidades só funciona com versionamento
- Cada versão é uma cópia inteira do objeto, e isso impacta diretamente no objeto

# S3 CORS(Cross-origin resource sharing) - proteção

- é a aws que libera a permissão para o CORS
- Exemplo de permissão CORS:

    [
    {
        "AllowedHeaders": [
            "*"
        ],
        "AllowedMethods": [
            "GET",
            "PUT",
            "POST",
            "DELETE"
        ],
        "AllowedOrigins": [
            "http://127.0.0.1:5500"
        ],
        "ExposeHeaders": [
            "x-amz-server-side-encryption",
            "x-amz-request-id",
            "x-amz-id-2"
        ],
        "MaxAgeSeconds": 3000
    }
]

# EC2
- É um serviço da Amazon que permite criar e hospedar sistemas de software na nuvem

- **Instance Metadata ** -> API REST para que o seu servidor possa perguntar para a AWS coi
- sas que ele não sabe, por exemplo o ip publico

- EFS(Elastic file system)
  -Linux
  - Paga por dados consumidos

- EFx 
  - Mesma coisa do EFS so q para windows
  - Esse eu preciso supervisionar o quanto vai cobrar pelo o que eu tenho

- Placement strategies
    ->Cluster
    ->Partition, nem todas as ferarmentas tem, por exemplo o RabbitM
    ->Spread

- EC2 purchase models
  - On-demand -> Tudo que quiser, a hora que quiser
  - Reserved -> Quero vir todo dia, no mesmo horario e usar o mesmo equipamento(esteira), engessado, não tem flexibilidade para mudar as configurações
  - Saving plans -> Aws, vou gastar 2 dolares por hora com voce, por 1 ano ou 3 anos, flexivel para alterar as configurações
# DATABASE

- Relacional = Escala com dor, escala vertical = aumentar cpu, memoria
- Não relacional = Schemas flexiveis, escalam normalmente e horizontalmente = copia do banco, particinamento automatico

# RDS (RELATIONAL DATABASE SERVICE)

- Serviço de banco de dados gerenciado
- Usa os outros serviços de banco por baixo
- MySQL, MariaDB, Postgress, Sqlserver, Oracle, IBM DB2, Aurora
- Aurora = banco de dados criado pela aws

# Dynamo/Neptune/Elastic cache (Non-relational database)

# Amazon VPC(rede) -> Software defined network(sdn)

- é um serviço da AWS que permite criar uma rede virtual isolada dentro da nuvem, que você pode personalizar e controlar
- Tudo dentro de um região é interconectado, porém eles nao se conectam com outras regiões a nao ser que voce queria
- toda vez que voce cria uma rede, ela fica sempre dentro de uma região
- CIDR -> Tamanho da rede definido pelo usuário
- O usuário customiza o tráfico
- Toda VPC tem uma tabela de rotas padrão, com uma regra que diz que qualquer coisa dentro da rede se comunique
- subsnets vivem dentro de uma az, quando voce cria uma subnet, voce diz que ela vai ficar em um lugar do mundo
- subnet public é uma subnet que esta publica de fora pra dentro e de dentro pra fora pra internet
- internet gateway -> responsável pelo NAT, se liga a vpc, recebe os ips que nao sao locais(da internet), e nele, tem o ip publico associado ao ip publico da subnet
- subnet privada -> não conversa com a internet ou algo fora da vpc
    - é onde vai colocar banco de dados, file share ou kafka
-Nat gateway serve para uma subnet privada se conectar com a net
- a opção de graça para o nat gateway é o gateway vpc endpoints, porem so conecta com s3 e DynamoDB
- Redes são isoldas
# Security group e Network acl
- Security group funcioona como o tio da portaria, ele libera ou nao de acordo com a identidade do dado de rede
  -se liberou a saida, a entrada ta permitida e se liberou a entrada a saida ta permitida
- Network acl ->  firewall stateless é um tipo de firewall que avalia cada pacote de rede individualmente, sem manter informações sobre o estado de uma conexão. Em vez de rastrear o fluxo de pacotes de uma sessão, ele analisa cada pacote baseado nas informações contidas no seu cabeçalho (como endereço IP, endereço MAC, etc.).

# Gateway Load balancer

- Nao consigo escrever e prestar atençap ao mesmo tempo


# Amazon VPC flow Logs
- trilha de auditoria para ver se as maquinas estao se comunicando

# VPC FULL MESH ARCHITECTURE
- nao pode ter coalisão
- Conversa com todas as redes

# SHARED VPC

- vpc central(hub) onde coloca os serviços compartilhaddos, e tem as vpcs spoke que conversam com o hub
- VPC spoke só conversa com o hub

# AWS transit gateway
- tem custo por dados processados
- Ajuda as redes a se conversar
- Serviço regional(vive dentro de uma região da aws)
- Consegue conecctar 5 mil attachments nele
- Da para conectar os ATG entre regiões
- não é toda empresa que precisa do transit gateway
- Peering transit gateway -> conectar mais de 1 transit gateway
  
# VPC Peering 
- outro metodo para subtituir o transit gateway
- Se conectar entre regioes é de graça
- puxar um cabo de rede de uma vpc para outra
- Não tem transitividade, por exemplo A -B , B - C , nesse caso aqui, A não converta com C, só se fizer um peering de A para C

# AWS DIRECT CONNECT
- Vai ser feito um circuito de rede para conectar um datacenter até a empresa

# IAM GROUPS
- Eu crio uma função, por exemplo, desenvolvedores, e associa as permissões da funçao, e associo as pessoas ao grupo
- Em conflito de permissão, o deny tem prioridade

# RBAC (Role-based-acess-control)
- Acesso temporario com determinadas permissões
- quando o usuario acessa a role, ele ganha uma credencial nova e temporaria

# ABAC (Attribute-based-acess-controll)
- Não cria policy fixa, cria police dinamica, exemplo, so pode acessar os objetos do S3 se tiver a tag do usuário

