# Some-AWS-concepts-sumarry
In order to align all students, in the Compass Scholarship Program, our mentor asked us to sumaryse and explain step-by-step the following AWS concepst: Load Balancer, Auto Scaling Group and the Scaling up and down policys.

## Load Balancer
Um Load Balancer distribui o tráfego de entrada da web de forma uniforme entre várias instâncias EC2, o que aumenta a tolerância a falhas das suas aplicações. Ele atua como um único ponto de contato para os clientes, garantindo que o tráfego seja direcionado apenas para instâncias saudáveis, o que evita interrupções no serviço.

## Auto Scaling Group (ASG)
Um Auto Scaling Group garante que sua aplicação tenha sempre o número correto de instâncias EC2 para lidar com a demanda. Ele monitora o tráfego e a carga de trabalho, ajustando a quantidade de instâncias dinamicamente. Isso permite que você mantenha o desempenho da sua aplicação sem precisar gerenciar manualmente cada instância.

## Scaling Policies
As Scaling Policies (Políticas de Escalabilidade) definem como o Auto Scaling Group deve adicionar ou remover instâncias. As políticas mais comuns são:

- Scaling Up: Adiciona novas instâncias quando a demanda aumenta (ex: uso da CPU atinge 80%).

- Scaling Down: Remove instâncias quando a demanda diminui (ex: uso da CPU cai para 30%).

De modo informal, eu os descreveria da seguinte forma:

O Load Balancer está relacionado distribuir a carga de trabalho entre as instâncias, a fim de evitar que o sistema fique sobrecarregado e venha a falhar.

O Auto 

# Passo a Passo para Implementar
Pré-requisitos
Antes de começar, certifique-se de que você já tem:

Uma Amazon Machine Image (AMI) personalizada com a sua aplicação.

Uma Virtual Private Cloud (VPC) e subnets configuradas.

Um Security Group para suas instâncias.

Passo 1: Configurar um Load Balancer
No console da AWS, navegue até EC2 > Load Balancers.

Clique em Create Load Balancer e escolha Application Load Balancer (ALB).

Dê um nome ao seu Load Balancer e selecione a VPC e as subnets onde ele irá operar.

Crie um novo Security Group para o Load Balancer ou selecione um existente. Certifique-se de que ele permite tráfego na porta 80 ou 443 (HTTP/HTTPS).

Crie um Target Group. Este grupo irá agrupar as instâncias para onde o tráfego será direcionado.

Defina um nome para o Target Group.

Escolha Instances como tipo de alvo.

Defina o protocolo (geralmente HTTP) e a porta.

Configure a Health Check (verificação de saúde) para que o Load Balancer saiba quais instâncias estão funcionando.

Complete a criação do Load Balancer.

Passo 2: Criar um Auto Scaling Group (ASG)
No console da AWS, navegue até EC2 > Auto Scaling Groups.

Clique em Create Auto Scaling Group.

Dê um nome para o seu ASG.

Crie um template de inicialização (Launch template). Este template é a "receita" que o ASG usará para criar novas instâncias.

Escolha uma AMI.

Selecione o tipo de instância (ex: t2.micro).

Escolha o Security Group criado para as instâncias.

Adicione a sua Key Pair para acesso SSH.

Após criar o template, volte ao assistente do ASG. Selecione o template que você acabou de criar.

Defina o tamanho da rede e as subnets.

Na seção Configure group size and scaling policies, defina:

Desired capacity: O número de instâncias que você deseja ter inicialmente.

Minimum capacity: O número mínimo de instâncias.

Maximum capacity: O número máximo de instâncias.

Clique em Next para continuar.

Passo 3: Configurar as Scaling Policies
Na tela de Configure group size and scaling policies, clique em Target tracking scaling policy.

Defina a política para Scaling Up:

Escolha uma métrica, como Average CPU utilization ou Average Network Out.

Defina um valor alvo, por exemplo, 80%.

Isso significa que o ASG irá adicionar mais instâncias sempre que o uso médio da CPU do grupo atingir 80%.

Defina a política para Scaling Down:

Você pode usar a mesma métrica. O ASG irá automaticamente remover instâncias quando o uso da CPU cair abaixo do valor alvo.

Geralmente, você não precisa criar uma política separada para "scaling down" com Target tracking. O ASG ajusta o número de instâncias para se aproximar do valor alvo.

No próximo passo, adicione o Target Group criado no passo 1. Isso garante que as instâncias do ASG sejam automaticamente registradas no seu Load Balancer.

Revise as configurações e finalize a criação do Auto Scaling Group.

Seu ambiente AWS agora está configurado para distribuir o tráfego de entrada e escalar 
