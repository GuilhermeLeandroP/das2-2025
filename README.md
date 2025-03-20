![image](https://github.com/user-attachments/assets/5e29bdf3-88bb-4f16-82e5-155647838ad2)# das2-2025

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

# S3

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
  
