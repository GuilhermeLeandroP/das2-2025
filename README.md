# das2-2025

## Aula 27/02

- Recursos são descartáveis, porque é so matar e criar um novo
- IAC = insfraestructure as a code

## 06/03

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

  
