## Sua Nuvem AWS: Um Mar de Custos e Riscos ou um Oceano de Oportunidades?

Sua empresa está crescendo na AWS, mas a conta está virando uma 'terra de ninguém'?
Durante minha vida profissional passei por varias empresas que utilizavam aws como cloud provider e muitas delas sofriam com a 'dor do crescimento'
mudar doi, crescer doi isso vale para todas as areas das nossas vidas e nas contas em nuvem nao poderia ser diferente, sempre que um produto ou 
um time cresce e muitas vezes de maneira exponencial como foi no caso da pandemia para algumas empresas tech, nossa infraestrutura e muitas vezes ate mesmo um codigo mal implementados acabam ficando em segundo plano "depois nos vemos isso" e esse tipo de negligencia pode nos dar muito mais problemas do que nos imaginamos, uma conta mal gerenciada abre margens para falhas de seguranca entre ambientes como ambientes de desenvolvimento com acessos as redes producao e ate mesmo um endurecimento a modificacoes e como todos sabemos hoje ter capacidade de reagir rapido a mudancas eh o que torna uma empresa competitiva no mundo de hoje, alem disso quem nunca sofreu pra estimar custos dentro da infrastrutura, imagina ainda se essa estimativa precisasse separar por ambiente, por produto, por tenant e assim por diante e agora imagina precisar ter esse relatorio semanalmente ou mensalmente, ja vi acontecer. Ter uma conta baguncada torna isso praticamente invavel de se fazer.

## Root nao eh producao!

Sinto lhe dizer mas conta root nao eh producao, se voce nao entende o que eu to falando muito possivelmente voce usa conta root como producao, "ah mas minha conta funciona!" Isso soa como "ah mas meu codigo compila" isso nao significa que esta certo nao eh mesmo?
Quando voce usa uma conta unica e centralizada voce pode enfrentar uma serie de problemas como:

1) Impossibilidade de rastrear custos por departamento/projeto/tenant/ambiente
- Isso impossibilita que gestores ou time de finops possa ter visibilidade de quanto custa cada fragmento da empresa em termos tecnologicos
- Impossivel de determinar ROI da empresa 
- Impacto nas estrategias para investimento da plataforma


2) Permissões excessivamente amplas ("admin para todos").
-  Se um usuario tem acesso de admin ele sera admin para tudo, nao recrimino o uso de um acesso administrativo desde que ele seja conciente



3) Dificuldade em implementar políticas de segurança consistentes
- Fica muito mais verboso segmentar pemissoes administrativas a recursos especificos, por exemplo:
o DesenvolvedorA precisa de acesso de admin nas filas a, b,c. Isso quando falamos de um unico desenvolvedor para 3 filas, mesmo com infra as code isso fica extremamente complexo de se gerenciar

4) Problemas de conformidade quando auditores pedem relatórios
- Hoje em dia eh cada vez mais comum empresas de clientes realizarem auditorias nas plataformas que contratam, sejam para executar testes de vulnerabilidades, seja para verificar o isolamento de dados ou de execao de processos e uma conta unica torna isso invavael.
- Possivel perda de novos clientes


5) Desenvolvedores interferindo nos ambientes uns dos outros
- Ambientes de desenvolvimento podem e devem ser os ambientes baguncados, afinal eh ali onde os desenvolvedores fazem seusd playgrounds, mas se um desenvolvedor por um acaso quebrar o ambiente do outro ou alterar coisas que sao compartilhadas entre eles isso pode acarretar muitas vezes em tempo ocioso do teu time devido a uma quebra de ambiente

6) Em caso de invasao o hacker tera acesso a todos os seus recursos
- Nesse ponto imagine como se vc morasse em um studio, pode ser lindo, moderno e arrojado, mas se alguem abrir a porta nao existem trancas para outros "comodos" e ai ja era ele leva tudo e faz o que quiser la dentro


7) Falta de isolamento de ambiente
- Quem nunca recebeu a seguinte ordem: "Preciso de um ambiente isolado durante os testes dessa nova release". Com uma conta unificada voce pode ateh dizer pra ele "Esta pronto" mas ca entre nos voce e eu sabemos que vc nao isolou esse ambiente


## Existe uma solucao!

Para contornar esse problema a AWS criou o Organizations que basicamente nos permite criar OrganizationsUnits e Sub Contas dentro da nossa conta na aws.
Uma OrganizationUnit basicamente serve para que possamos agrupar sub accounts dentro da nossa conta, vamos fazer algumas exemplificacoes de como ela funciona.

### Exemplo1:

Imagine que temos uma empresa que trabalha com 3 produtos diferentes:

- finnancial-tech
- annalitics-tech
- customers-tech

Cada produto possui clientes proprios, projetos proprios e sao cobrados de formas distintas dos clientes, cada um desses produtos possuem 3 fases de desenvolvimento sendo elas:
- desenvolvimento
- quality-assurance
- production

Tendo essa divisao temos uma cardinalidade de 3x3 e necessitamos de 9 ambientes diferentes, para isso podemos fazer a seguinte divisao dentro da nossa organization.

Criamos uma organization unit para cada produto e cada organization unit tera 3 subaccountas na aws:

1) Finnancial-tech:
- ft-development
- ft-qa
- ft-production

2) Annalitics-tech:
- at-development
- at-qa
- at-production

3) Customers-tech:
- ct-development
- ct-qa
- ct-production

"Ah mas voce tera que replicar custos desncessarios entre essas contas" Muitas vezes a resposta para isso eh sim, mas vai por mim antes replicar um dominio ou uma instancia de banco do que sofrer com os problemas que nao ter uma divisao dessa pode trazer, tudo na vida eh um trade-off e aqui nao seria diferente, os riscos nao valem essa "economia"

Nas proximas semanas eu irei abordar como fazer essa separacao de forma eficiente e automatizada, sem que tenha a necessidade de clicar em nenhuma tela para criar uma nova organization unit ou uma nova sub conta.

Mas quero ouvir de vcs Sua empresa já enfrenta esses desafios? Quais são os sintomas mais dolorosos da 'conta única' na sua experiência?