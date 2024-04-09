# CloudFormation
Repositorio para armazenar e versionar a criação de templates da AWS CloudFormation 

Em razão da pequena quantidade de conteudo sobre Cloud Formation, o unico lugar onde se encontra explicaçoes sobre o assunto é a propria documentação da AWS, basta buscar `AWS::EC2::'RESOURCE_NAME'` que encontrará um guia

## Atualização 08/04

Neste atualização consegui corrigir os erros e adaptar soluções aos problemas enfrentados anteriormente, como a necessidade de passar o Endpoint do RDS e o ID do EFS para dentro do script de inicialização, e issso foi resolvido por meio do uso da `Fn::Sub`, disponivel no CloudFormation, no formato encontrado na `UserData` do recurso `MeuLaunchTemplate` no arquivo `templateCF.yaml`, um exemplo de uso dessa solução foi encontrada no site https://docs.aws.amazon.com/pt_br/AWSCloudFormation/latest/UserGuide/cfn-init.html#cfn-init-Examples , que demonstra a utilização do cf-init.

Ao consertar este ponto do Launch Template, foi possivel configurar o Auto Scaling Group direto do arquivo yaml, assim atribuindo as instancias criadas por ele direto ao load balancer, que logo as tem funcionando para rodar o wordpress, acessivel por meio do seu DNS.

Unico recurso que não foi possivel replicar, foi a `Target Tracking Policy` do Auto Scaling Group, por eu não ter encontrado uma `property` que fizesse essa configuração.

No ultimo teste realizado a Stack levou +- 7minutos para ser concluida a partir da criação.

## Inicialização da Stack

Para iniciar a Stack basta ir em `CloudFormation > Stacks > Create stacks`, e selecionar as seguintes opções:

  - Prerequisite - Prepare template: Choose an existing template
  - Specify template: Upload a template file

Em `Choose file`, encontrar a localização do arquivo `TemplateCF.yaml` e seleciona-lo. Escolher um nome para a stack em `Stack name` e apenas clicar em `Next` e `Submit` até a Stack iniciar a criação e agardar a conclusão. 

Assim está concluido o processo de criação do template CloudFormation para o segundo projeto do programa de bolsas DevSecOps da Compass.
